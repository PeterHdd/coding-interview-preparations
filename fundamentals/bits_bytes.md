# Bits And Bytes

----

- Bits are 1 and 0. 
- 8 bit is equal to 1 byte, the 8 bit can have a value from 0 to 255 decimal because 2^8 is equal to 255.
- ASCII is an encoding representing each typed character by a number, each number is stored in one byte so between (0 to 255)
- One byte = collection of 8 bits
- e.g. 0 1 0 1 1 0 1 0
- One byte can store one character, e.g. 'A' or 'x' or '$'
- Computers have have bits with two possible values *0 and 1*. So they use base 2 numbers. (Base 10 is called decimal. Base 2 is called binary)
- In binary (base 2) are sequential powers of 2:
    - 2^0 = 1
    - 2^1 = 2
    - 2^2 = 4
    - 2^3 = 8

So if we have 101 binary number, then we go from right to left ((1 * 2^2) + (0 * 2^1) + (1 * 2^0)) = 4 + 0 + 1 = 5 decimal number.

|Decimal|	Binary|	Interpretation|
|----|----|---|
|0|	0000	|0 + 0 + 0 + 0|
|1|	0001|	0 + 0 + 0 + 1|
|2	|0010|	0 + 0 + 2 + 0|
|3	|0011|	0 + 0 + 2 + 1|
|4	|0100|	0 + 4 + 0 + 0|
|5	|0101|	0 + 4 + 0 + 1|
|6	|0110|	0 + 4 + 2 + 0|
|7	|0111|	0 + 4 + 2 + 1|
|8	|1000|	8 + 0 + 0 + 0|
|9	|1001	|8 + 0 + 0 + 1|
|10|	1010	|8 + 0 + 2 + 0|

- If you have a negative number, then in binary number the left most digit will be 1, while in postive number the leftmost digit will be 0. so -5 decimal number is 1101 (1 * 2^2) + (0 * 2^1) + (1 * 2^0)) = 4 + 0 + 1 = 5 since there is "1" in the end then it's -5.

### Bitwise operations

- Bitwise operators work on binary digits or bits of input values. We can apply these to the integer types – long, int, short, char, and byte.
- To preform bitwise operations, then the numbers are transformed to binary and the operation is done and later on they are transformed to decimal again. Example:

```
int value1 = 6;
int value2 = 5;
//Binary number of value1 = 0110
//Binary number of value2 = 0101

int result = 6 | 5;
//0110
//0101
//-----
//0111
//result = 7
```

- **Bitwise OR Operator (|)**: The OR operator compares each binary digit of two integers and gives back 1 if either of them is 1.
- **Bitwise AND Operator (&)**: The AND operator compares each binary digit of two integers and gives back 1 if both are 1, otherwise it returns 0.
- **Bitwise XOR operator (^)**: The XOR operator compares each binary digit of two integers and gives back 1 if both the compared bits are different. This means that if bits of both the integers are 1 or 0 the result will be 0; otherwise, the result will be 1.
- **Bitwise Complement (~)**: Bitwise Not or Complement operator simply means the negation of each bit of the input value. It takes only one integer and it's equivalent to the ! operator. Basically if you have 1 binary then it will be transformed to 0 and if you have 0 binary then it will be transformed to 1.

```
int value1 = 6;
int result = ~value1;

// value1 = 0000 0110
// 0000 0110 -> 1111 1001 //now to get this decimal number we have to do the following:
1. invert 1 to 0 and 0 to 1
2. 1111 1001 -> 0000 0110 
3. add + 1
4. 0000 0110 + 1 -> 0000 0111 -> -7 decimal number
//0+0 = 0, with no carry,
//1+0 = 1, with no carry,
//0+1 = 1, with no carry,
//1+1 = 0, and you carry a 1.
//to add 1, you need to convert 1 to binary and add it.
//we add 1 because it is 1 complement so with +1 it will become 2 complement
//answer is -7 since when we inverted the binaries, we had 1 bit at the left most
```

### Bit Shifting

- A bit shift moves each digit in a number's binary representation left or right. The syntax is 
```
<value> <operator> <number_of_times>
```
- There are three main types of shifts:

    1. The left shift operator shifts the bits to the left by the number of times specified by the right side of the operand. After the left shift, the empty space in the right is filled with 0. Another important point to note is that shifting a number by one is equivalent to multiplying it by 2, or, in general, left shifting a number by n positions is equivalent to multiplication by 2^n:
    ```
    0010 << 1  →  0100
    0010 << 2  →  1000
    ```
    - A single left shift multiples a binary number by 2:
    ```
    0010 << 1  →  0100

    0010 is 2
    0100 is 4
    ```
    2. Logical or unsigned Right Shifts **>>>** When shifting right with a logical right shift, the least-significant bit is lost and a 0 is inserted on the other end. Example:
    ```
    1011 >>> 1  →  0101
    1011 >>> 3  →  0001

    //For positive numbers, a single logical right shift divides a number by 2, throwing out any remainders.

    0101 >>> 1  →  0010
    0101 is 5
    0010 is 2
    ```
    3. Signed Right Shift **>>** The right shift operator shifts all the bits to the right. The empty space in the left side is filled depending on the input number:
        - When an input number is negative, where the leftmost bit is 1, then the empty spaces will be filled with 1
        - When an input number is positive, where the leftmost bit is 0, then the empty spaces will be filled with 0
        ```
        1011 >> 1  →  1101 //negative
        1011 >> 3  →  1111 //negative

        0011 >> 1  →  0001
        0011 >> 2  →  0000
        ```
