# Operation Orchid
Author: LT 'syreal' Jones

Description
Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
Download compressed disk image

Firstly i wget challenge, after that i use commmand mmls to see paths of disk image:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)
```
I try test one by one path by command:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ fls -o 2048 disk.flag.img      
d/d 11: lost+found
r/r 12: ldlinux.sys
r/r 13: ldlinux.c32
r/r 15: config-virt
r/r 16: vmlinuz-virt
r/r 17: initramfs-virt
l/l 18: boot
r/r 20: libutil.c32
r/r 19: extlinux.conf
r/r 21: libcom32.c32
r/r 22: mboot.c32
r/r 23: menu.c32
r/r 14: System.map-virt
r/r 24: vesamenu.c32
V/V 25585:      $OrphanFiles
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ fls -o 206848 disk.flag.img 
Cannot determine file system type
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ fls -o 411648 disk.flag.img    
d/d 460:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 81: proc
d/d 82: dev
d/d 83: tmp
d/d 84: lib
d/d 87: var
d/d 96: usr
d/d 106:        bin
d/d 120:        sbin
d/d 466:        media
d/d 470:        mnt
d/d 471:        opt
d/d 472:        root
d/d 473:        run
d/d 475:        srv
d/d 476:        sys
d/d 2041:       swap
V/V 51001:      $OrphanFiles
```
As you can see, in 411648, it has path root, and we will focus it:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ fls -o 411648 disk.flag.img 472
r/r 1875:       .ash_history
r/r * 1876(realloc):    flag.txt
r/r 1782:       flag.txt.enc

┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ icat -o 411648 disk.flag.img 1875               
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt

```
In 1875, we see line openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567, file flag.txt has been encrypted into flag.txt.enc by AES-256 with key unbreakablepassword1234567
and it has been -salt to hard in lookup, we will restore file flag.txt by flag.txt.enc and key, and first we have to save file flag.txt.enc:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ icat -o 411648 disk.flag.img 1782 > flag.txt.enc
```
And then we restore file flag.txt
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ openssl aes256 -d -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
bad decrypt
40B7C79FC67F0000:error:1C800064:Provider routines:ossl_cipher_unpadblock:bad decrypt:../providers/implementations/ciphers/ciphercommon_block.c:107:
```
And cat flag:
```
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ ls
disk.flag.img  flag.txt  flag.txt.enc
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~/Downloads/pico2022/Operation_Orchid]
└─$ cat flag.txt
picoCTF{h4un71ng_p457_0a710765}
```
