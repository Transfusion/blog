---
title: First Foray into MIPS Assembly
url: 451.html
id: 451
categories:
  - Programming
  - Unix
date: 2014-09-30 23:26:28
tags:
---

Task: Print Hello World 10 times.

	.data
hello_str: .asciiz "Hello World!n"
	.text
	.globl main
main:
	subu $sp, $sp, 4 # create a word on the stack
	sw $ra, 4($sp) # store the return address
\# put main function code here

	li $t0, 10 #the number at which we want to end our loop.
	li $t1, 0 #start counting from 0; we are going to increment this counter 10 times.
	li $v0, 4 # set $v0 to print_string; http://courses.missouristate.edu/kenvollmar/mars/Help/SyscallHelp.html
	la $a0, hello_str # load the string
	loop:
		beq $t1, $t0, end # if t1 == 10 we are done
		syscall # execute the function described by
		addi $t1, $t1, 1 # add 1 to t1
		j loop # jump back to the top
	end:
		li $v0, 10
		syscall

[![recorded_compressed](/wp-content/uploads/2014/09/recorded_compressed1-300x214.gif)](/wp-content/uploads/2014/09/recorded_compressed1.gif)