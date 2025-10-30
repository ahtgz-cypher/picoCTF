# Mob Psycho
Mob psycho
Author: NGIRIMANA Schadrack

Description
Can you handle APKs?
Download the android apk here.

Hints 
Did you know you can unzip APK files?

Now you have the whole host of shell tools for searching these files.

First we upzip file dowloaded, after we cd to file and use command:
```
┌──(kali㉿kali)-[~/Downloads/Psycho]
└─$ find| grep "flag"
./app.apk/res/color/flag.txt                      
```
And we try cd to file flag.txt and received code:
```
7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f61336562356163327d
```
Decode it with CyberChef and we will receive the flag:
```
Recipe (click to load)	Result snippet	Properties
From_Hex('None')
picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_a3eb5ac2}	Matching ops: From Base85
Valid UTF8
Entropy: 4.64
7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f61336562356163327d	Matching ops: From Base64, From Base85, From Hex, From Hexdump
Valid UTF8
Entropy: 3.37
```
