# PicoGym Web Exploitation Writeup


Author: [Ankur Kumar](https://github.com/awsoankur) 

Challenge Page: [Web Gauntlet](http://jupiter.challenges.picoctf.org:54319/)

## Walkthrough
in round 1 we cant use `or` in our sqli.
let try username as `admin';` and an arbritary password and it works.
in round 2 we cant use `or`,`and`,`like`,`=`,`--` but we already used none of these.
lets try the same credentials again, and we get it !
the new filters are `<` and `>`.
same thing as round 2, well lmao we got in ez.
for round 3 we cant use `admin` (pain).
so we try splitting admin as ad+min or putting the username as `ad'+'min';`
guess it did not work.
searching on sqlite concatenation we find the `||` operator , so now replace that with our +
and retrying.
DONE!
new filter => `union`,
retrying the same for round 5.
we find the flag in the filter file .



## Flag
`picoCTF{y0u_m4d3_1t_a5f58d5564fce237fbcc978af033c11b}`
