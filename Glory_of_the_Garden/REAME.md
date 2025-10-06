# Glary_of_the_Garden
Sau khi tải file về thì mình nhận được một file ảnh garden.jpg, và mình đã thử tìm flag với lệnh grep:
```
strings garden.jpg |grep -i picoCTF{
```
thì mình đã nhận được flag:
```
┌──(kali㉿kali)-[~/Downloads]
└─$ strings garden.jpg|grep -i picoCTF 
Here is a flag "picoCTF{more_than_m33ts_the_3y3657BaB2C}"
```
