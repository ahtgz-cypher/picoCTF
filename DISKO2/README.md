# Disko 2
Description
Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!
Download the disk image here.
Hints 
How can you extract/isolate a partition?

Mình copy đường dẫn đó và dùng lệnh để tải file:
```
wget https://artifacts.picoctf.net/c/540/disko-2.dd.gz
```
Sau khi tải file về, mình đã unzip file bằng lệnh:
```
gunzip disko-2.dd.gz
```
Sau đó mình đã nhận được file disko-2.dd và thử kiểm tra file bằng lệnh:
```
mmls disko-2.dd
```
Thì kết quả trả về là:
```
└─$ mmls disko-2.dd   
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000053247   0000051200   Linux (0x83)
003:  000:001   0000053248   0000118783   0000065536   Win95 FAT32 (0x0b)
004:  -------   0000118784   0000204799   0000086016   Unallocated
```
Và vì challenge gợi ý là The right one is Linux nên mình sẽ chỉ tập trung vào Linux, mình thử tìm kiếm flag bằng lệnh:
```
strings disko=2.dd| grep -i picoctf
```
Sau đó có rất nhiều flag được in ra và mình cũng nghĩ là 1 trong số đó là flag đúng, có thể bruteko 2
Description
Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!
Download the disk image here.
Hints 
How can you extract/isolate a partition?

Mình copy đường dẫn đó và dùng lệnh để tải file:
```
wget https://artifacts.picoctf.net/c/540/disko-2.dd.gz
```
Sau khi tải file về, mình đã unzip file bằng lệnh:
```
gunzip disko-2.dd.gz
```
Sau đó mình đã nhận được file disko-2.dd và thử kiểm tra file bằng lệnh:
```
mmls disko-2.dd
```
Thì kết quả trả về là:
```
└─$ mmls disko-2.dd   
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000053247   0000051200   Linux (0x83)
003:  000:001   0000053248   0000118783   0000065536   Win95 FAT32 (0x0b)
004:  -------   0000118784   0000204799   0000086016   Unallocated
```
Và vì challenge gợi ý là The right one is Linux nên mình sẽ chỉ tập trung vào Linux, mình thử tìm kiếm flag bằng lệnh:
```
strings disko-2.dd| grep -i picoctf
```
Sau đó có rất nhiều flag được in ra và mình cũng nghĩ là 1 trong số đó là flag đúng, có thể brute force để làm, nhưng ở đây mình sẽ sử dụng lệnh:
```
dd if=disko-2.dd of=Linuxresult.img bs=512 skip=2048 count=51200
```
Và thử kiểm tra bằng lệnh cat thì thấy có rất nhiều dữ liệu được in ra, và mình thử tìm flag bằng grep và kết quả là flag xuất hiện:
picoCTF{...}
