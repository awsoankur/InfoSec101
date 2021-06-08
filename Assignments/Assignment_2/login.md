# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [login](login.mars.picoctf.net)

## Walkthrough
seeing the js file "index.js" and beutifying it on [here](jsnice.org) , we see that it is 
using the function btoa and also cheking the usrename's equality to "YWRtaW4" which is base64
of "admin". so clearly the data is sent in encrypted form and the encrytion in base64 .
upon decryting the password string in the index.js we get the flag .


## Flag
`picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}`
