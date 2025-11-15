Lookey here
Author: LT 'syreal' Jones / Mubarak Mikail

Description
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it.
Download the data here.
debug info: [u:723551 e: p: c:279 i:294817]

Hints 
Download the file and search for the flag based on the known prefix.

In this challenge, you just need use command grep picoCTF, it basic
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Lookey_here]
└─$ strings anthem.flag.txt| grep -i picoCTF         
      we think that the men of picoCTF{gr3p_15_@w3s0m3_58f5c024}
```
