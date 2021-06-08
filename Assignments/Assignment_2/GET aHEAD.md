# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Get aHEAD](http://mercury.picoctf.net:15931/)

## Walkthrough
after spending a lot of time looking for a third option from the hint , i noticed the name of the q "GET aHEAD", thought of the get request searched a bit about different requests , found out there exists a HEAD request . then upon resending the html header request we get the flag in the response headers

## Flag
`picoCTF{r3j3ct_th3_du4l1ty_82880908}`

