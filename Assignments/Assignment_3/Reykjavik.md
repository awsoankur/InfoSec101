# MicroCTF Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Level: Reykjavik

## Walkthrough
On seeing the `main` function , we see calss of 2 functions .
one is named `enc` and the other is unnamed ( sus ).
```
4438 <main>
4438:  3e40 2045      mov	#0x4520, r14
443c:  0f4e           mov	r14, r15
443e:  3e40 f800      mov	#0xf8, r14
4442:  3f40 0024      mov	#0x2400, r15
4446:  b012 8644      call	#0x4486 <enc>
444a:  b012 0024      call	#0x2400
444e:  0f43           clr	r15
```
setting break point in `enc` function and goin in we can see some bytes being copied.
```
4486 <enc>
4486:  0b12           push	r11
4488:  0a12           push	r10
448a:  0912           push	r9
448c:  0812           push	r8
448e:  0d43           clr	r13
4490:  cd4d 7c24      mov.b	r13, 0x247c(r13)
4494:  1d53           inc	r13
4496:  3d90 0001      cmp	#0x100, r13
449a:  fa23           jne	#0x4490 <enc+0xa>
449c:  3c40 7c24      mov	#0x247c, r12
44a0:  0d43           clr	r13
44a2:  0b4d           mov	r13, r11
44a4:  684c           mov.b	@r12, r8
44a6:  4a48           mov.b	r8, r10
44a8:  0d5a           add	r10, r13
44aa:  0a4b           mov	r11, r10
44ac:  3af0 0f00      and	#0xf, r10
44b0:  5a4a 7244      mov.b	0x4472(r10), r10
44b4:  8a11           sxt	r10
44b6:  0d5a           add	r10, r13
44b8:  3df0 ff00      and	#0xff, r13
44bc:  0a4d           mov	r13, r10
44be:  3a50 7c24      add	#0x247c, r10
44c2:  694a           mov.b	@r10, r9
44c4:  ca48 0000      mov.b	r8, 0x0(r10)
44c8:  cc49 0000      mov.b	r9, 0x0(r12)
44cc:  1b53           inc	r11
44ce:  1c53           inc	r12
44d0:  3b90 0001      cmp	#0x100, r11
44d4:  e723           jne	#0x44a4 <enc+0x1e>
44d6:  0b43           clr	r11
44d8:  0c4b           mov	r11, r12
44da:  183c           jmp	#0x450c <enc+0x86>
44dc:  1c53           inc	r12
44de:  3cf0 ff00      and	#0xff, r12
44e2:  0a4c           mov	r12, r10
44e4:  3a50 7c24      add	#0x247c, r10
44e8:  684a           mov.b	@r10, r8
4ea:  4b58           add.b	r8, r11
44ec:  4b4b           mov.b	r11, r11
44ee:  0d4b           mov	r11, r13
44f0:  3d50 7c24      add	#0x247c, r13
44f4:  694d           mov.b	@r13, r9
44f6:  cd48 0000      mov.b	r8, 0x0(r13)
44fa:  ca49 0000      mov.b	r9, 0x0(r10)
44fe:  695d           add.b	@r13, r9
4500:  4d49           mov.b	r9, r13
4502:  dfed 7c24 0000 xor.b	0x247c(r13), 0x0(r15)
4508:  1f53           inc	r15
450a:  3e53           add	#-0x1, r14
450c:  0e93           tst	r14
450e:  e623           jnz	#0x44dc <enc+0x56>
4510:  3841           pop	r8
4512:  3941           pop	r9
4514:  3a41           pop	r10
4516:  3b41           pop	r11
4518:  3041           ret
```
upon running it and observing what happens we notice this code just plays around with bytes and copies them to other locations
so its not much use to see this function .
then we got to the function at 2400 in live code.
there to see the function we need to see the memory storage at 2400 and see the next 256 bytes.
we then copy the bytes and put them in a assembler  to assemble the code to inspect it.
```
0b12 0412 0441 2452 3150 e0ff 3b40 2045
073c 1b53 8f11 0f12 0312 b012 6424 2152
6f4b 4f93 f623 3012 0a00 0312 b012 6424
2152 3012 1f00 3f40 dcff 0f54 0f12 2312
b012 6424 3150 0600 b490 db01 dcff 0520
3012 7f00 b012 6424 2153 3150 2000 3441
3b41 3041 1e41 0200 0212 0f4e 8f10 024f
32d0 0080 b012 1000 3241 3041
```
which converts to
```
2400:    0b12           push	r11
2402:    0412           push	r4
2404:    0441           mov	sp, r4
2406:    2452           add	#0x4, r4
2408:    3150 e0ff      add	#0xffe0, sp
240c:    3b40 2045      mov	#0x4520, r11
2410:    073c           jmp	$+0x10
2412:    1b53           inc	r11
2414:    8f11           sxt	r15
2416:    0f12           push	r15
2418:    0312           push	#0x0
241a:    b012 6424      call	#0x2464
241e:    2152           add	#0x4, sp
2420:    6f4b           mov.b	@r11, r15
2422:    4f93           tst.b	r15
2424:    f623           jnz	$-0x12
2426:    3012 0a00      push	#0xa
242a:    0312           push	#0x0
242c:    b012 6424      call	#0x2464
2430:    2152           add	#0x4, sp
2432:    3012 1f00      push	#0x1f
2436:    3f40 dcff      mov	#0xffdc, r15
243a:    0f54           add	r4, r15
243c:    0f12           push	r15
243e:    2312           push	#0x2
2440:    b012 6424      call	#0x2464
2444:    3150 0600      add	#0x6, sp
2448:    b490 11ab dcff cmp	#0xad06, -0x24(r4)
244e:    0520           jnz	$+0xc
2450:    3012 7f00      push	#0x7f
2454:    b012 6424      call	#0x2464
2458:    2153           incd	sp
245a:    3150 2000      add	#0x20, sp
245e:    3441           pop	r4
2460:    3b41           pop	r11
2462:    3041           ret
2464:    1e41 0200      mov	0x2(sp), r14
2468:    0212           push	sr
246a:    0f4e           mov	r14, r15
246c:    8f10           swpb	r15
246e:    024f           mov	r15, sr
2470:    32d0 0080      bis	#0x8000, sr
2474:    b012 1000      call	#0x10
2478:    3241           pop	sr
247a:    3041           ret
```
Clearly 
```
2450:    3012 7f00      push	#0x7f
2454:    b012 6424      call	#0x2464
```
this peice of code will open the door 
so in order to execute this line we need the condition `cmp	#0xad06, -0x24(r4)` to be true
so we go in this function and do `b 2448` to observe the value of r4 which comes out to be
`r04 43fe` .
which is the memory address of the first byte of the entered password.
so in order to clear the level we need to enter `ad06` minding the endiness.

## Password
`06ad`