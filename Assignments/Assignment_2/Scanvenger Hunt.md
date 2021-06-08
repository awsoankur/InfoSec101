# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Scanenger Hunt](http://mercury.picoctf.net:27393/)

## Walkthrough
this page as similarity to the Insp3ct0r q , so upon scanning the html and css page we get the 2 part of flags .
in the js file it says about indexing of websites by google and to prevent this , so the robots.txt file can tell us about this and there we fing the 3rd part.
it say the server is an Apache server and has the werd "Access" with a capital A so, upon digging in about the apace server , i found out something calles .htacess exists for such servers . 
Going in this file we find the 4th part of the flag. In there it says Mac and Store with a capital letter including in the hints.
With a lot of time and research about this and soome functioning of macs , i found out that the mac use a DS_Store file to store configurations which satisfies our hint.
In the file we finally get the last part of the flag. phew too much work 


## Flag
`picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_d375c750}`