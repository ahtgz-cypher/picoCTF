# Information
Sau khi tải file về thì mình nhận được file ảnh cat.jpg, mình thử test với lệnh 
```
exiftool cat.jpg
```
Thì có một đoạn base64 trong kết quả mình nhận được:
```
                                                                                                                                                                                                                                           
┌──(kali㉿kali)-[~/Downloads]
└─$ exiftool cat.jpg           
ExifTool Version Number         : 13.00
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2025:09:30 09:53:20-04:00
File Access Date/Time           : 2025:10:06 08:53:54-04:00
File Inode Change Date/Time     : 2025:09:30 09:53:20-04:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1

```
Sau khi decode nó thì mình đã nhận được flag
picoCTF{...}
