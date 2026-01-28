## <u> Overview </u> 
*64 Rows of bit cells & 64 Cols of bit cells.*
- We need a wire connecting clock.
- We need a wire connecting reset.
- We need a wire connecting to each of the bit cells in each row.
- We need a wire connecting to each of the bit cells in each col.
- We need a wire for data input.
- We need a wire for data output.
```verilog
module cell_array #(
	parameter ROWS = 64,    //defines 64 word lines (horizontal rows) in the memory array
	parameter COLS = 64     //defines 64 bit lines (vertical columns) in the memory array
)(
	input wire clk,         //clock signal for synchronous operations (all cells update on clock edges)
	input wire rst,         //Reset signal to reset state of memory cells
	input wire[$clog2(ROWS)-1:0] row_select,    //6 bit address input to select which row to access. 2^6 = 64
	input wire[COLS-1:0] write_enable, //Write enable for each column (64 bits wide)
	input wire[COLS-1:0] data_in,      //data to write to the selected cells. Each bit corresponds to one col
	input wire[COLS-1:0] data_out //data read from the selected row, one bit from each col of selected row.
);
```

*The following below may need to change.*
## <u> How Row Activation Works </u>
*Only one row is being activated at a particular point in time (requires less power) this is called `row activation` or `wordline activation`*

When a particular row is activated...
1. All cells in that row become accessible `row_select[ROW]` signal activates the entire word line.
2. Columns signals control individual bit operations. Each cell's write enable is controlled by `row_select[ROW] & write_enable[COL]`
		Only when `row_select[ROW]` and `write_enable[COL]` are both active high will that `ROW` and `COL` be written.
		E.g. if row 5 is selected and only column 10's write_enable is high, only `cell[5][10]` will be written.
3. Reading happens across the entire row, when a row is selected, all 64 cells in that row output their data, then column multiplexing selects which bits you actually read.
---
## <u> Internal Signals </u>
```verilog
wire [ROWS-1:0][COLS-1:0] total_data_out;
wire [ROWS-1:0] row_decoder;
```

`wire [ROWS-1:0][COLS-1:0] total_data_out;`
- This is a 2D array holding outputs from ALL cells (64x64)
- This is the complete memory state - every bit from every cell
- It stores all cell outputs, then selects the desired row.

`wire [ROWS-1:0] row_decoder;`
- One-hot encoded row decoder output (64 bits)
- Only ONE bit is high at a time, selecting exactly one row.
- Converts binary address to one-hot row selection.
---
## <u> Row Decoder Logic </u>
```verilog
genvar r;
generate
	for(r = 0; r < ROWS; r = r + 1) begin : gen_decoder
		assign row_decoder[r] = (row_select == r);
	end
endgenerate
```

`assign row_decoder[r] = (row_select == r);`
- Compares the input address to each row number.
- Only the matching row gets `1`, all others get `0`
- One-hot encoding ensures only one word line activates
---
## <u> Memory Cell Array Instantiation </u>
```verilog
genvar curr_row;
genvar curr_col;
generate
	for (curr_row = 0; curr_row < ROWS; curr_row = curr_row + 1) begin : gen_rows
		for (curr_col = 0; curr_col < COLS; curr_col = curr_col + 1) begin : gen_cols
			bit_cell bit_cell_inst (
				.clk(clk),
				.rst(rst),
				.write_enable(row_decoder[curr_row] & col_write_enable[curr_col]),
				.data_in(col_data_in[curr_col]),
				.data_out(total_data_out[curr_row][curr_col])
			);
		end
	end
endgenerate
```
*Nested `generate` loops create a 64x64 grid of bit cells. Outer loop iterates through ROWS. Inner loop iterates through COLS. Instantiate one `bit_cell` per position*

`.clk(clk)`
- Clock shared by all cells.
`.rst(rst)` 
- Reset shared by all cells.
`.write_enable(row_decoder[curr_row] & col_write_enable[curr_rol])`
- Write only happens when BOTH:
	- Current row is selected (`row_decoder[curr_row] is 1`)
	- Current col has write enabled (`col_write_enabled[curr_col] is 1`)
	- This is the AND gate between word line and write enable.
`.data_in(col_data_in[curr_col])`
- Connects the input data for this column to the bit cell.
`.data_out(total_data_out[curr_row][curr_col]`
- Stores this cell's output in the 2D array.`
---


> [!NOTE] Title
> Contents
