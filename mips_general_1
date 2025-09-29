.data
prompt1:    .asciiz "Enter the number of rows and columns for the first matrix (n m): "
prompt2:    .asciiz "Enter the number of columns for the second matrix (k): "
prompt3:    .asciiz "Enter the elements of matrix1: "
prompt4:    .asciiz "Enter the elements of matrix2: "
result_msg: .asciiz "The resulting matrix is:\n"
newline:    .asciiz "\n"
space:      .asciiz " "

.text
.globl main

main:
    # Print prompt for the dimensions of the first matrix
    li $v0, 4
    la $a0, prompt1
    syscall

    # Read number of rows (n) for the first matrix
    li $v0, 5
    syscall
    move $t0, $v0       # n (rows)
    
    # Read number of columns (m) for the first matrix
    li $v0, 5
    syscall
    move $t1, $v0       # m (columns)

    # Print prompt for the number of columns of the second matrix
    li $v0, 4
    la $a0, prompt2
    syscall

    # Read number of columns (k) for the second matrix
    li $v0, 5
    syscall
    move $t2, $v0       # k (columns)

    # Calculate the size of the matrices in bytes
    mul $t3, $t0, $t1   # n * m
    sll $t3, $t3, 2     # (n * m) * 4 (since each word is 4 bytes)

    # Allocate space for matrix1
    li $v0, 9           # sbrk syscall
    move $a0, $t3
    syscall
    move $s0, $v0       # address of matrix1

    # Calculate size for the second matrix (m * k)
    mul $t3, $t1, $t2   # m * k
    sll $t3, $t3, 2     # (m * k) * 4

    # Allocate space for matrix2
    li $v0, 9           # sbrk syscall
    move $a0, $t3
    syscall
    move $s1, $v0       # address of matrix2

    # Allocate space for result matrix (n * k)
    mul $t3, $t0, $t2   # n * k
    sll $t3, $t3, 2     # (n * k) * 4
    li $v0, 9           # sbrk syscall
    move $a0, $t3
    syscall
    move $s2, $v0       # address of result

    # Print prompt for matrix1 elements
    li $v0, 4
    la $a0, prompt3
    syscall

    # Read elements of matrix1
    move $t4, $s0
    mul $t3, $t0, $t1   # Total number of elements in matrix1
read_matrix1:
    li $v0, 5
    syscall
    sw $v0, ($t4)
    addi $t4, $t4, 4
    addi $t3, $t3, -1
    bnez $t3, read_matrix1

    # Print prompt for matrix2 elements
    li $v0, 4
    la $a0, prompt4
    syscall

    # Read elements of matrix2
    move $t4, $s1
    mul $t3, $t1, $t2   # Total number of elements in matrix2
read_matrix2:
    li $v0, 5
    syscall
    sw $v0, ($t4)
    addi $t4, $t4, 4
    addi $t3, $t3, -1
    bnez $t3, read_matrix2
    
    
    addi $s4, $s1, 0
    addi $s5, $s2, 0
    # Matrix multiplication
    li $t3, 0               # row counter for matrix1
outer_loop:
    li $t4, 0               # column counter for result matrix
inner_loop:
    li $t5, 0               # Reset the sum to 0
    li $t6, 0               # column counter for matrix2

    mul $t7, $t3, $t1       # calculate offset for matrix1 row start
    mul $t7, $t7, 4	    # word size is 4
    add $t7, $s0, $t7       # base address of current row in matrix1

    mul_loop:
    
    	lw $t7, ($s0)       # Load element from matrix1
        lw $t8, ($s1)       # Load element from matrix2
        mul $t9, $t7, $t8   # Multiply elements
        add $t5, $t5, $t9   # Accumulate sum

        addi $s0, $s0, 4    # Move to next element in matrix1
        mul $s3, $t2, 4
        add $s1, $s1, $s3   # Move to next row in matrix2
        addi $t6, $t6, 1    # Increment column counter for matrix2
        bne $t6, $t1, mul_loop  # Loop until column counter == m
        
    
    sw $t5, ($s2)        # Store the sum in the result matrix
    addi $s2, $s2, 4     # Move to next element in result matrix
    addi $t4, $t4, 1     # Increment column counter for result matrix
    mul $s3, $t1, 4
    sub $s0, $s0, $s3     # reset the point of to the starting point of row in matrix1
    
    mul $s3, $t1, $t2
    mul $s3, $s3, 4
    sub $s3, $s3, 4
    sub $s1, $s1, $s3     # move to next column in matrix2
    bne $t4, $t2, inner_loop  # Loop until column counter == k
    
   
   
    addi $t3, $t3, 1     # Increment row counter for matrix1
    addi $s1, $s4, 0	# move the the first row of matrix2
    mul $s3, $t1, 4
    add $s0, $s0, $s3   # move to next row in matrix1
    bne $t3, $t0, outer_loop  # Loop until row counter == n

    
    # Print the resulting matrix
    li $v0, 4
    la $a0, result_msg
    syscall
    
    addi $t3, $0, 0
    addi $t5, $0, 0
    addi $s2, $s5, 0
    
    mul $t4, $t0, $t2

    
    nextline_print:
    	
    	bne $t5, $t2, print
    	li $v0, 4
    	la $a0, newline
    	syscall
    	
    	addi $t5, $0, 0
    	
    
    print:
    	lw $t6, ($s2)           # Load element from result matrix
    	li $v0, 1               # Print integer syscall
    	move $a0, $t6
    	syscall
    	
    	li $v0, 4
    	la $a0, space
    	syscall
    	
    	addi $t3, $t3, 1
    	addi $t5, $t5, 1
    	addi $s2, $s2, 4
    	bne $t3, $t4, nextline_print
    	
    	
    	
    
    
    
    


    li $v0, 10              # Exit the program
    syscall
