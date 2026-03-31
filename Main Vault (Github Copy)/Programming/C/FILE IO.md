### There are a few steps to perform when reading/writing a file 
1. *Create a variable of type FILE to represent the file
2. *Open the file
3. *Use C functions to read/write to and from the file*
4. *Close the file*
### These are the C language function files to read/write from a file
- *fopen()* - create a new file or open a existing file
- *fclose()* - close the file
- *getc()* - reads a character from the file
- *putc()* - writes a character to a file
- *getw()* - reads an integer from a file
- *putw()* - writes an integer to a file
- *fscanf()* - reads a set of data from a file
- *fprintf()* - writes a set of data to a file
- *fseek()* - set the position to desire point
- *ftell()* - gives current position in the file
- *rewind()* - set the position to the beginning point

```
FILE *fopen(const char *filename, const char *mode);
```
*fopen() call returns a reference to a value of type FILE, thats why we must use asterisk

```
FILE *my_data = fopen("in_info.dat", "r");
```
*my_data*  file pointer variable name
*in_info.dat* the file name to open
*"r"* the open mode

```
if (my_data == NULL) {
	//print an error message, can include global variable "errno"
	//exit, or recover from the error
}
```
*after each open attempt, its best to check for any errors so that the program doesn't bomb*
*a return of NULL from fopen() indicates an error, you can use errno to check for the specific error*
![[Screenshot 2024-10-29 at 11.56.54 PM.png|600]]
