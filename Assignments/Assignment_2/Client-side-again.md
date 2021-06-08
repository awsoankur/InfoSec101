# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Client-side-gain](http://jupiter.challenges.picoctf.org:60786)

## Walkthrough
examining the page source we find a snippet containg some js code.
using [this](jsnice.org) to beautify it we get a similar code as dont-use-client-side.
we get that the flag must be`_0x4b5b("0x3")`,`_0x4b5b("0x4")`,`_0x4b5b("0x6")`,`_0x4b5b("0x5")` in order.
To get these values we can use the browser console and simply type in these values.



## Flag
`picoCTF{not_this_again_ef49bf}`
