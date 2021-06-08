# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Cookies](http://mercury.picoctf.net:21485/)

## Walkthrough
upon seeing the name cookies , first checked the cookies section of the inspect . Noticed the value of the cookie as -1 .
Tried changing the HttpOnly and other field values but nothign happened.  
Entering the word "snickerdoodle" in the field required , it says not a special cookie :( ,
opened the cookie again noticed the value change to 0 ( sus )
tried changeing the value of the cooke to 1 and refreshed page and :0 the cookie changed ,
well now upon going throught every value of the cookie the cookie value of 18 gives us the flag (the "special" cookie).


## Flag
`picoCTF{3v3ry1_l0v3s_c00k135_94190c8a}`


