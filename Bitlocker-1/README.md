# Bitlocker-1
Bitlocker-1
Author: Venax

This problem cannot be solved in the webshell.

Description
Jacky is not very knowledgable about the best security passwords and used a simple password to encrypt their BitLocker drive. See if you can break through the encryption!
Download the disk image here
Hints 
Hash cracking

Đề bài cho file bitlocker-1.dd sau đó mình dùng lệnh bitlocker2john bitlocker-1.dd > bitlocker.hash, sau đó dùng lệnh cat bitlocker.hash và chỉ lấy password của file, sau đó dùng lệnh hashcat -m 22100 -a 0 bitlocker.txt /usr/share/wordlists/rockyou.txt, sau đó dùng lệnh sudo bdemount -p 'jacqueline' bitlocker-1.dd /tmp/bitlocker sau đó dùng quyền root bằng lệnh sudo su để đi đến file tmp, và dùng lệnh cd /tmp/bitlocker sau đó ls -la ra thì thấy có file bde1 và dùng strings bde1 grep -i picoCTF
và nhận được flag
picoCTF{...}

