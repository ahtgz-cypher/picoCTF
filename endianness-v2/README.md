# endianness-v2
endianness-v2
Author: Junias Bonou

Description
Here's a file that was recovered from a 32-bits system that organized the bytes a weird way. We're not even sure what type of file it is.
Download it here and see what you can get out of it

Hints 
(None)

This challenge no hint, first we download file and check type file and it is file data, after check deep data of file by bless, and see it may be bit order shutffling and it could be file JFIF (file image),
i used tool cyberchef to do it

First, i add file challengefile to page and i search in page keyword "Swap endianness" afterthat i edit data format from hex to raw and i adjust word length(bytes) to 4 and i save it to file download.jpg.
I cat it and received image contain flag

picoCTF{...}
