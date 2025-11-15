Operation Oni
Author: LT 'syreal' Jones

Note: you must launch a challenge instance in order to view your disk image download link.

Description
Download this disk image, find the key and log into the remote machine.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
Additional details will be available after launching your challenge instance.

debug info: [u:723551 e: p: c:284 i:294827]

This challenge launches an instance on demand.
Its current status is: NOT_RUNNING

Hints 
(None)

First we wget challenge and gzip file, after that we use command mmls to see paths of files:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)

```
and we use command fls to see file of paths:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ fls -o 206848 disk.img     
d/d 458:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 79: proc
d/d 80: dev
d/d 81: tmp
d/d 82: lib
d/d 85: var
d/d 94: usr
d/d 104:        bin
d/d 118:        sbin
d/d 464:        media
d/d 468:        mnt
d/d 469:        opt
d/d 470:        root
d/d 471:        run
d/d 473:        srv
d/d 474:        sys
V/V 33049:      $OrphanFiles

```
we see root in this, and we focus it:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ fls -o 206848 disk.img 470 
r/r 2344:       .ash_history
d/d 3916:       .ssh
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ fls -o 206848 disk.img 3916
r/r 2345:       id_ed25519
r/r 2346:       id_ed25519.pub
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ icat -o 206848 disk.img 2345      
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLAAAAJgxpYKDMaWC
gwAAAAtzc2gtZWQyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLA
AAAECItu0F8DIjWxTp+KeMDvX1lQwYtUvP2SfSVOfMOChxYGCtd7hso2E7OQItY6aTjMMy
KZb1FVmeBfnVjyHcGYosAAAADnJvb3RAbG9jYWxob3N0AQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ icat -o 206848 disk.img 2345 > key   
```
And if you take this key to connect sever, server will require you enter password
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$  ssh -i key -p 61629 ctf-player@saturn.picoctf.net
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for 'key' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "key": bad permissions
ctf-player@saturn.picoctf.net's password: 
Permission denied, please try again.
ctf-player@saturn.picoctf.net's password: 
Permission denied, please try again.
ctf-player@saturn.picoctf.net's password: 
ctf-player@saturn.picoctf.net: Permission denied (publickey,password).
```
And you just need authorization rm to file private key, you will connect with sever:
As you can see, we had private key, and now we will launch instance and take flag:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ ls -la                    
total 235540
drwxrwxr-x  2 kali kali      4096 Nov 15 09:59 .
drwxrwxr-x 10 kali kali      4096 Nov 13 03:49 ..
-rw-rw-r--  1 kali kali 241172480 Aug  4  2023 disk.img
-rw-rw-r--  1 kali kali       411 Nov 15 09:59 key
-rw-rw-r--  1 kali kali        96 Nov 15 09:59 keypl

┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ chmod 600 key                                                                                                                                                                                                                               
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ ls -la
total 235540
drwxrwxr-x  2 kali kali      4096 Nov 15 09:59 .
drwxrwxr-x 10 kali kali      4096 Nov 13 03:49 ..
-rw-rw-r--  1 kali kali 241172480 Aug  4  2023 disk.img
-rw-------  1 kali kali       411 Nov 15 09:59 key
-rw-rw-r--  1 kali kali        96 Nov 15 09:59 keypl

ssh -i key_file -p 49741 ctf-player@saturn.picoctf.net
we have to edit key_file to key which we saved
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Oni]
└─$ ssh -i key -p 49741 ctf-player@saturn.picoctf.net
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.8.0-1035-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt
picoCTF{k3y_5l3u7h_339601ed}ctf-player@challenge:~$ ^C
ctf-player@challenge:~$ exit
logout
Connection to saturn.picoctf.net closed.
```
