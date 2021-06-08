# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Who are you?](http://mercury.picoctf.net:52362/)

## Walkthrough
using the same procedure for the q picobrowser we bypass this condition.
using Referer to link the website to itself we can get rid of the second problem.
using Date we can change the date to somewhere in 2018.
using DNT: 1 we can stop being tracked.
using X-Forwarded-For: we can use an ip from sweden to fool the website.
editing the Accept-Language to sv we can speak swedish :).




## Flag
`picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_0c0db339}`
