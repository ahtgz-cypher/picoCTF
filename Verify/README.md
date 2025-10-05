# Verify
Đề bài lần này cho một đường dẫn để kết nối đến máy chủ ssh 
```
ssh -p 58640 ctf-player@rhea.picoctf.net
```
Và sau khi kết nối và kiểm tra với lệnh ls và ls -la thì mình thấy có 3 files là checksum.txt, decrypt.sh và files, mình thử kiểm tra file checksum để đảm bảo 
mình đã kết nối tới đúng server:
```
cat checksum.txt
```
Và để tính mã SHA256 của tất cả các file trong thư mục files và so sánh với mã hash trong check_sum.txt để đảm bảo đúng:
```
sha256sum files/* |grep -f checksum.txt
```
Và mình đã nhận được file và đoạn mã sha256 trùng khớp với sha ở trong checksum.txt, sau dó thử đọc file mình vừa nhận được bằng lệnh: 
```
cat files/451fd69b
```
Sau đó mình thấy ở đầu đoạn mã được in ra có chữ Salted, điều này chứng tỏ file đã được mã hóa bằng OpenSSL.
Và rồi mình chạy script để giải mã file:
```
./decrypt.sh files/451fd69b
```
Và mình đã nhận được flag:
picoCTF{trust_but_verify_451fd69b}


