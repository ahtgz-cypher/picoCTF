Sleuthkit Intro
Author: LT 'syreal' Jones

Description
Download the disk image and use mmls on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
Download disk image
Additional details will be available after launching your challenge instance.

This challenge launches an instance on demand.
Its current status is: NOT_RUNNING
Access checker program: nc saturn.picoctf.net 63607
Hints 
(None)

In this challenge, it think it easy, because we don't need open disk image with Autopsy or FTK image, we still can solve it.
Firstly, i wget challenge and gzip file disk.img.gz, after that i Launch instance and nc saturn.picoctf.net 63607:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Sleuthkit_Intro]
└─$ nc saturn.picoctf.net 63607
What is the size of the Linux partition in the given disk image?
Length in sectors:
```
It ask we enter length of disk image and i use command:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Sleuthkit_Intro]
└─$ file disk.img   
disk.img: DOS/MBR boot sector; partition 1 : ID=0x83, active, start-CHS (0x0,32,33), end-CHS (0xc,190,50), startsector 2048, 202752 sectors

```
And we take it and send it and received flag:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Sleuthkit_Intro]
└─$ nc saturn.picoctf.net 65329
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
picoCTF{mm15_f7w!}
```
