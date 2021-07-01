# MicroCTF Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Level: Sydney

## Walkthrough
Going through the main function we can see that if r15 after the function call is non zero 
then we can unlock the door.
Inspecting `check_password`
`
448a <check_password>
448a:  bf90 446f 0000 cmp	#0x6f44, 0x0(r15)
4490:  0d20           jnz	$+0x1c
4492:  bf90 772d 0200 cmp	#0x2d77, 0x2(r15)
4498:  0920           jnz	$+0x14
449a:  bf90 2c7b 0400 cmp	#0x7b2c, 0x4(r15)
44a0:  0520           jne	#0x44ac <check_password+0x22>
44a2:  1e43           mov	#0x1, r14
44a4:  bf90 333f 0600 cmp	#0x3f33, 0x6(r15)
44aa:  0124           jeq	#0x44ae <check_password+0x24>
44ac:  0e43           clr	r14
44ae:  0f4e           mov	r14, r15
44b0:  3041 
`
Clearly we can see that 
-first 2 bytes are being compared to 0x6f44
-next 2 bytes are being compared to 0x2d77
-next 2 bytes are being compared to 0x7b2c
-last 2 bytes are being compared to 0x3f33
so in order to avoid the line
`44ac:  0e43           clr	r14`
we need all these conditions to be true.
hence we ned to input the password (as hex) `6f442d777b2c3f33`.
But in since assembly little endian storage is used we must reverse the alternate bytes.
Hence the payload in hex should look like 
`446f772d2c7b333f`
This will unlock the door.
## Password
`446f772d2c7b333f`