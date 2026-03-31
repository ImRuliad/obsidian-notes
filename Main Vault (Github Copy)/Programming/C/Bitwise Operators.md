
### *To understand how to perform Bitwise Operators we must first learn how to convert between #Hex, #Octal, and #Binary* 

--- start-multi-column: ExampleRegion2  
```column-settings  
number of columns: 2
Column Spacing: 10px
```
## #Hex 
### Each *Hex* digit is defined by *4-bits in Binary*

| Binary | Hex | Binary | Hex |
| ------ | --- | ------ | --- |
| 0000   | 0   | 1000   | 8   |
| 0001   | 1   | 1001   | 9   |
| 0010   | 2   | 1010   | A   |
| 0011   | 3   | 1011   | B   |
| 0100   | 4   | 1100   | C   |
| 0101   | 5   | 1101   | D   |
| 0110   | 6   | 1110   | E   |
| 0111   | 7   | 1111   | F   |


--- end-column ---

## #Octal 
### Each *Octal* digit is defined by *3-bits in Binary*
![[Screenshot 2024-10-29 at 7.23.16 PM.png]]


---end-multi-column
## So, the Decimal number *30132 in Hex is 75B4*, in *Binary is 0111010110110100, in Octal is 72664*


# #BitwiseOperators in C

--- start-multi-column: ExampleRegion2  
```column-settings  
number of columns: 2
Column Spacing: 10px
```

### There are *4 Logical Operators* in C
- ( **~** ) Bitwise Compliment (unary) *Inverts bit string representation (All 0s become 1s and all 1s become 0s*
- ( **&** ) Bitwise AND *Returns a "1" if both bits have "1" returns 0 otherwise*
- ( **^** ) Bitwise Exclusive OR *Returns a "1" if both bits have opposing values e.g. 0 and 1 or a 1 and 0. If both bits the same it will return 0.*
- ( **|** ) Bitwise Inclusive OR *Returns a "1" if EITHER bit has "1" returns 0 otherwise*

--- end-column ---

### There are *2 Shifting Operators* in C
- *<<* left Shift - *Shifts bit to the left by 1*
- *>>* Right Shift *Shifts bit to the right by 1*

![[Screenshot 2024-10-29 at 7.39.21 PM.png]]





---end-multi-column






--- start-multi-column: ExampleRegion4  

```column-settings  
number of columns: 2
Column Spacing: 10px
```

![[Screenshot 2024-10-29 at 7.45.05 PM.png]]






---end-column---







![[Screenshot 2024-10-29 at 7.45.21 PM.png]]


---end-multi-column






--- start-multi-column: ExampleRegion5  


```column-settings  
number of columns: 2
Column Spacing: 10px
```
![[Screenshot 2024-10-29 at 7.45.59 PM.png]]





---end-column---






![[Screenshot 2024-10-29 at 7.45.31 PM.png]]






---end-multi-column




## Masking using #bitwise AND

--- start-multi-column: ExampleRegion5  


```column-settings  
number of columns: 2
Column Spacing: 10px
```

### Suppose *a* is an unsigned 16-bit integer variable whose value is *0x6db7*
### Extract the *right* most *6 bits* of the value using AND (*&*)
### A = *0x6db7*
### MASK = *0x3f*
#### Assign them to unsigned integer variable *b*
##### b = a & MASK (0x3f)
*we use 0x3f because 0x3f = 0000 0000 0011 1111*




---end-column---





![[Screenshot 2024-10-29 at 11.11.14 PM.png]]




---end-multi-column

## Masking using the AND
*This time were are masking using the same logical operator just with a different mask to get the extract the LEFT MOST 6 bits.*

![[Screenshot 2024-10-29 at 11.17.12 PM.png]]



# THIS IS NOT FINISHED, COME BACK AND FINISH THIS (SLIDE 15)

