# Bitlocker-1
Bitlocker-1
Author: Venax
```
This problem cannot be solved in the webshell.

Description
Jacky is not very knowledgable about the best security passwords and used a simple password to encrypt their BitLocker drive. See if you can break through the encryption!
Download the disk image here
Hints 
Hash cracking
```

Đề bài cho file bitlocker-1.dd, mình dùng lệnh file thì trả về kết quả là file DOS/MBR. Và sau đó mình đọc tài liệu thì thấy bitlocker nó là:
```
I. Bitlocker là gì?
- Bitlocker là công nghệ mã hóa ổ đĩa (full disk encrytion) do Micosoft phát triển, được tích hợp trong Windows (từ Windows Vista trở đi)
- Mục đích: bảo vệ toàn bộ dữ liệu trong ổ cứng khỏi bị truy cập trái phép nếu máy tính bị mất hoặc ổ đĩa bị tháo ra

- Tức là, nếu ai đó lấy được ổ đĩa và cắm sang máy khác thì họ cũng không thể đọc được dữ liệu vì toàn bộ ổ đĩa đã bị mã hóa AES

II. Nguyên lí hoạt động (kỹ thuật cơ bản)
- Bitlocker có 3 tầng chính:
1. FVEK (Full Volume Encryption Key): Dùng để mã hóa/giải mã dữ liệu thật trong ổ, là khóa AES để mã hóa từng sector của ổ đĩa (theo chế độ AES-CBC hoặc AES-XTS)
2. VMK (Volume Master Key): Dùng để bảo vệ FVEK, VMK mã hóa FVEK để không lưu FVEK thô trên đĩa
3. Key Protectors(bộ bảo vệ khóa): Dùng để bảo vệ VMK, có thể là mật khẩu người dùng, TPM chip, khóa khôi phục (recovery key 48 số), file .BEK(file khóa lưu trong USB), ...

Khi nhập password hoặc recovery key, Bitlocker sẽ:
- Dùng nó để giải mã VMK
- Rồi dùng VMK để giải mã FVEK
- Và cuối cùng dùng FVEK để giải mã toàn bộ dữ liệu trong ổ
III. Về thuật toán mã hóa
- Dữ liệu được mã hóa bằng AES:
  + Windows 10+ thường dùng AES-XTS (128 hoặc 256 bit)
  + Phiên bản cũ dùng AES-CBC + Elephant diffuser
- Các khóa (VMK, FVEK) được bảo vệ bằng AES-CCM hoặc AES-CBC (tùy phiên bản)
- Password hoặc recovery key được xử lí qua PBKDF2-HMAC-SHA256 để tăng độ khó khi brute-force
IV. Liên quan tới forensics /CTF
- Trong các bài CTF, thường gặp:
+ Một file .dd (disk image) bị mã hóa bằng bitlocker
+ Nhiệm vụ: trích metadata, tạo hash rồi brute-force mật khẩu yếu
+ Công cụ hay dùng:
  bitlocker2john (trích hash cho John hoặc Hashcat)
  hashcat -m 22100 (crack Bitlocker)
  bde mount / dislocker (mở khóa và mount ổ sau khi có key)
``` 
sau đó mình dùng lệnh bitlocker2john -i bitlocker-1.dd > bitlocker.hash, sau đó dùng lệnh cat bitlocker.hash và chỉ lấy password của file
```
$bitlocker$0$16$cb4809fe9628471a411f8380e0f668db$1048576$12$d04d9c58eed6da010a000000$60$68156e51e53f0a01c076a32ba2b2999afffce8530fbe5d84b4c19ac71f6c79375b87d40c2d871ed2b7b5559d71ba31b6779c6f41412fd6869442d66d
```
- Sau đó dùng lệnh mv để đổi tên file từ đuôi .hash về đuôi .txt để crack. Sau đó dùng lệnh hashcat -m 22100 -a 0 bitlocker.txt /usr/share/wordlists/rockyou.txt
- Nếu bạn đã làm rồi thì bạn sẽ cần thêm --show để hiển thị password bạn đã tìm được trước đó, sau đó dùng lệnh:
``` sudo bdemount -p 'jacqueline' bitlocker-1.dd /tmp/bitlocker```
- Sau đó dùng quyền root bằng lệnh sudo su để đi đến file tmp, và dùng lệnh cd /tmp/bitlocker sau đó ls -la ra thì thấy có file bde1 và dùng strings bde1 grep -i picoCTF
và nhận được flag
picoCTF{...}

