MIPS Assembly Implementation of Matrix Multiplication

💡 Project Overview

This project provides a low-level implementation of the Matrix Multiplication algorithm in MIPS Assembly Language. 
The program is designed to run on MIPS simulators (such as MARS or SPIM) and demonstrates core assembly programming concepts, 
including dynamic memory allocation, precise register management, and nested loop control flow for complex mathematical operations.

The program handles the multiplication of two matrices, A(n×m) and B(m×k), to produce a result matrix C(n×k).

⚙️ Key Technical Features

1. Dynamic Memory Allocation (sbrk System Call)

The program dynamically allocates the necessary memory on the heap for all three matrices (A, B, and the Result C) using the MIPS sbrk system call (code 9). 
This ensures efficient memory usage based on user-defined dimensions n,m, and k.

3. Register Management

Registers are strictly used to store base addresses, loop counters, temporary calculation results, and offsets:

$s0, $s1, $s2: Base addresses for Matrix A, Matrix B, and Result C, respectively.

$t0 (n), $t1 (m), $t2 (k): Dimensions of the matrices.

$t3, $t4: Loop counters for rows and columns.

3. Core Algorithm: Triple Nested Loop

The multiplication is achieved using the standard triple nested loop structure optimized for row-major order:

Outer Loop (outer_loop): Iterates through rows of Matrix A (i from 0 to n−1).

Inner Loop (inner_loop): Iterates through columns of Matrix B (j from 0 to k−1).

Dot Product Loop (mul_loop): Calculates the dot product of row i of A and column j of B.

🚀 How to Run

This program requires a MIPS simulator (MARS or SPIM) to execute.

Load the Script: Load the matrix_multiplier.asm file into your MIPS simulator.

Run: Execute the program.

Input: The program will prompt the user to enter the dimensions (n,m,k) followed by the individual integer elements for Matrix A and Matrix B.

Output: The resulting matrix C(n×k) will be printed to the console, with elements separated by a space and rows separated by a newline character.

Required Input Format:

Enter n (rows of A)

Enter m (columns of A / rows of B)

Enter k (columns of B)

Enter the n×m elements for Matrix A (one per line).

Enter the m×k elements for Matrix B (one per line).

✒️ Author

Melika Jebeli

GitHub: https://github.com/Melika-Jebeli

Email: Melika.hj8@gmail.com
