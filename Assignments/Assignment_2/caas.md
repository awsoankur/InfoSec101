# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [caas](https://caas.mars.picoctf.net/)

## Walkthrough
tried some sql injection but
upon examining the file we got in the q sqli doesnt seem like the way to go .
instead the terminal commands seem like the solutions .
trying `;ls;` as the cowsay message ,we get the list of files and we notice  
a file named "falg.txt" so doing `;cat falg.txt;` we get our flag. 

## Flag
`picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}`
