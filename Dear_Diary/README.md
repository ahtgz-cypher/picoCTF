# Dear Diary
Dear Diary
Author: syreal

Description
If you can find the flag on this disk image, we can close the case for good!
Download the disk image here.

Hints 
If you're observing binary data raw in the terminal you may be misled about the contents of a block.
First, i wget file disk image of challenge and i gzip it, i test it by command file to check type file, after that i try further analysis by command:
```
mmls disk.flag.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000616447   0000614400   Linux (0x83)
003:  000:001   0000616448   0001140735   0000524288   Linux Swap / Solaris x86 (0x82)
004:  000:002   0001140736   0002097151   0000956416   Linux (0x83)
```
It seperated three partition, and i try open it by AutoPsy and i find something important

<img width="1175" height="684" alt="image" src="https://github.com/user-attachments/assets/317a1466-918c-4414-9475-f885fe2624ac" />
 After that i try open file disk.flag.img by bless to find strings innocuous and i observe it carefully and i realize flag seperated many partiton and i try copy it and put them together and i reveived the flag picoCTF{...}
