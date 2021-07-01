# MicroCTF Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Level: New Orleans

## Walkthrough
upon starting in main , It is visible that the main function just calls the `check_password` 
function and unlocks door only for non zero return value.
Inspecting the function:
`
44bc <check_password>
44bc:  0e43           clr	r14
44be:  0d4f           mov	r15, r13
44c0:  0d5e           add	r14, r13
44c2:  ee9d 0024      cmp.b	@r13, 0x2400(r14)
44c6:  0520           jne	#0x44d2 <check_password+0x16>
44c8:  1e53           inc	r14
44ca:  3e92           cmp	#0x8, r14
44cc:  f823           jne	#0x44be <check_password+0x2>
44ce:  1f43           mov	#0x1, r15
44d0:  3041           ret
44d2:  0f43           clr	r15
44d4:  3041           ret
` 
upon seeing how it works we can see that the function returns 1 if the password entered 
matches with the data stored at memory adress `0x2400` .
Setting breakpoint in the function and cheking the memory dump we can see the value of the 
string.
`2400:   3378 4770 384d 3000 0000 0000 0000 0000   3xGp8M0.........`
Therefore, `3xGp8M0` is the required password which will unlock the door. 
## Password
`3xGp8M0`
