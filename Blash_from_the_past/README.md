# Blash from the past
Blast from the past
Author: syreal

As of March 13th, the last check now accepts more formats.

Description
The judge for these pictures is a real fan of antiques. Can you age this photo to the specifications?
Set the timestamps on this picture to 1970:01:01 00:00:00.001+00:00 with as much precision as possible for each timestamp. In this example, +00:00 is a timezone adjustment. Any timezone is acceptable as long as the time is equivalent. As an example, this timestamp is acceptable as well: 1969:12:31 19:00:00.001-05:00. For timestamps without a timezone adjustment, put them in GMT time (+00:00). The checker program provides the timestamp needed for each.
Use this picture.
Additional details will be available after launching your challenge instance.

This challenge launches an instance on demand.
Its current status is: NOT_RUNNING

Hints 
Exiftool is really good at reading metadata, but you might want to use something else to modify it.

After read challenge, i try Launch Instance, i wget file image and use command exiftool to see more infomation. I pay attention for time of:
```
Date/Time Original              : 1970:01:01 00:00:00
Create Date                     : 1970:01:01 00:00:00
and
Create Date                     : 1970:01:01 00:00:00.001
Date/Time Original              : 1970:01:01 00:00:00.001
Modify Date                     : 1970:01:01 00:00:00.001
```
and i try run command:
```
Submit your modified picture here:
nc -w 2 mimas.picoctf.net 57607 < original_modified.jpg
Check your modified picture here:
nc mimas.picoctf.net 61506
```
and server display 
```
┌──(kali㉿kali)-[~/Downloads]
└─$ nc mimas.picoctf.net 61506
MD5 of your picture:
06783ef2aa4460a3d267002a28ff12c6  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 2023:11:20 15:46:23
Oops! That tag isn't right. Please try again.
```
Target is we have to edit file, edit 2023:11:20 15:46:23 become 1970:01:01 00:00:00, i use bless to edit file:
```
sudo apt install bless
bless image.jpg &
```
and i edit line that and after a while i edited all and received flag:
```
┌──(kali㉿kali)-[~/Downloads]
└─$ nc mimas.picoctf.net 52171                             
MD5 of your picture:
0af320dcbce8237243e5441975bd48d5  test.out

Checking tag 1/7
Looking at IFD0: ModifyDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 2/7
Looking at ExifIFD: DateTimeOriginal
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 3/7
Looking at ExifIFD: CreateDate
Looking for '1970:01:01 00:00:00'
Found: 1970:01:01 00:00:00
Great job, you got that one!

Checking tag 4/7
Looking at Composite: SubSecCreateDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 5/7
Looking at Composite: SubSecDateTimeOriginal
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 6/7
Looking at Composite: SubSecModifyDate
Looking for '1970:01:01 00:00:00.001'
Found: 1970:01:01 00:00:00.001
Great job, you got that one!

Checking tag 7/7
Timezones do not have to match, as long as it's the equivalent time.
Looking at Samsung: TimeStamp
Looking for '1970:01:01 00:00:00.001+00:00'
Found: 1970:01:01 00:00:00.001+00:00
Great job, you got that one!

You did it!
picoCTF{71m3_7r4v311ng_p1c7ur3_3e336564}
```
