# COA-Lab_task-4


# Assembly Code for Multiplication and ASCII Conversion
---
## Description
Write an assembly language program to perform multiplication of 8-bit and 16-bit data

## 8bit_multiplication
This assembly program multiplies two 8-bit hexadecimal numbers (13h and 05h), converts the resulting product into its ASCII representation (hexadecimal format), and displays the digits using DOS interrupts.

## How the Code Works

1. **Set Starting Address**:
   - `org 100h` sets the code to start at memory address 100h, which is standard for COM files.

2. **Load Numbers to Multiply**:
   - `mov al, 13h` loads the first number (13h) into register AL.
   - `mov bl, 05h` loads the second number (05h) into register BL.

3. **Multiply the Numbers**:
   - `mul bl` multiplies the values in AL and BL, storing the result in AX (low byte in AL, high byte in AH).

4. **Prepare the Result for ASCII Conversion**:
   - The multiplication result (in AL) is moved to BL for later use.
   - `mov ah, al` moves AL to AH to start the conversion process.

5. **Convert the Upper Nibble of the Result to ASCII**:
   - `and ah, 0F0h` masks the lower nibble, keeping the upper.
   - `shr ah, 4` shifts the upper nibble into the lower position.
   - `add ah, 30h` converts the nibble to its ASCII equivalent.
   - If the result is greater than '9', it adjusts to convert to a hexadecimal character ('A'-'F').

6. **Print the First Digit**:
   - `mov dl, ah` moves the converted ASCII value to DL.
   - `mov ah, 02h` sets up the DOS interrupt 21h for character output.
   - `int 21h` outputs the first digit.

7. **Convert the Lower Nibble of the Result to ASCII**:
   - `mov ah, bl` moves BL back to AH to handle the lower nibble.
   - `and ah, 0Fh` masks the upper nibble, keeping the lower.
   - `add ah, 30h` converts to ASCII, and if necessary, converts to 'A'-'F'.

8. **Print the Second Digit**:
   - `mov dl, ah` moves the second ASCII character to DL.
   - `mov ah, 02h` sets up for character output.
   - `int 21h` prints the second digit.

9. **Terminate the Program**:
   - `mov ah, 4Ch` prepares for program termination.
   - `int 21h` ends the program.

## Requirements

- An x86 emulator or DOS environment (e.g., DOSBox, TASM, MASM) to assemble and run the code.
- The code must be compiled as a `.COM` executable since it starts at address 100h.

## Usage

1. Assemble the code using an assembler like MASM or TASM.
2. Run the resulting executable in a DOS environment or emulator.
3. The output will display the hexadecimal representation of the product of 13h and 05h.

## Output
![image](https://github.com/user-attachments/assets/80610f77-88cd-4041-8470-4d8c89508ea3)


- The program multiplies 13h (19 in decimal) by 05h (5 in decimal), resulting in 5Fh (95 in decimal).
- The output will be displayed as two hexadecimal digits on the screen, which should appear as `5F`.

## Notes

- The program uses DOS interrupts for displaying output, which may not be supported in modern environments without an emulator.
- Make sure to run the code in an environment that supports 16-bit DOS applications.
---

## 16bit_multiplication
This assembly program multiplies two 16-bit hexadecimal numbers, converts the result into hexadecimal ASCII format, and prints each nibble (half-byte) of the result using DOS interrupts.

## How the Code Works

1. **Set Starting Address**:
   - `org 100h` sets the starting address at 100h, standard for COM files.

2. **Load 16-bit Values**:
   - `mov ax, 0012h` loads the first 16-bit value into AX.
   - `mov bx, 0102h` loads the second 16-bit value into BX.

3. **Multiply the Values**:
   - `mul bx` multiplies the value in AX by BX, storing the result in DX:AX (DX holds the high 16 bits, AX holds the low 16 bits).

4. **Store the Result**:
   - `mov bx, ax` moves the lower 16 bits of the result (in AX) to BX for further manipulation and display.

5. **Convert and Print Each Nibble of the Result**:
   
   **High Byte of BX (BH)**:
   - The high nibble of BH is isolated, converted to ASCII, and printed.
   - The low nibble of BH is then isolated, converted to ASCII, and printed.

   **Low Byte of BX (BL)**:
   - The high nibble of BL is isolated, converted to ASCII, and printed.
   - The low nibble of BL is then isolated, converted to ASCII, and printed.

6. **Conversion Process for Each Nibble**:
   - The code isolates each nibble, shifts or masks as necessary, and converts it to ASCII.
   - If the nibble value is greater than 9, it is adjusted to print as a hexadecimal letter ('A' to 'F').

7. **Print Nibble**:
   - `int 21h` is used with DOS interrupt function 02h to output each converted nibble to the screen.

8. **Terminate the Program**:
   - `mov ah, 4Ch` followed by `int 21h` terminates the program.

## Requirements

- An x86 assembler (TASM, MASM) and a DOS environment or emulator (like DOSBox) are required to assemble and run the code.
- Ensure the environment supports 16-bit assembly and DOS interrupts.

## Usage

1. Assemble the code using a compatible assembler.
2. Run the compiled executable in an appropriate environment.
3. The program will display the result of multiplying 0012h and 0102h in hexadecimal format.

## Output
![image](https://github.com/user-attachments/assets/1d3bb19b-de12-4de9-bc0c-5f3442d70d23)

- The multiplication of 0012h and 0102h results in a hexadecimal value.
- Each nibble of the result is printed sequentially in hexadecimal format.

## Example Calculation

For `0012h * 0102h`:
- The multiplication results in 01224h.
- The program prints the hexadecimal representation of this result as `01224` which is same as '4c8'.

## Notes

- This program uses DOS interrupts for character output, making it suitable for DOS environments or emulators.
- The code is set to start at address 100h, so it must be assembled as a `.COM` executable.
- The printed nibbles will be displayed as ASCII characters directly corresponding to their hexadecimal values.

---
