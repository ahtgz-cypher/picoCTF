# Bitlocker-2
```
Bitlocker-2
Author: Venax

This problem cannot be solved in the webshell.

Description
Jacky has learnt about the importance of strong passwords and made sure to encrypt the BitLocker drive with a very long and complex password. We managed to capture the RAM while this drive was opened however. See if you can break through the encryption!
Download the disk image here and the RAM dump here
Hints 
Try using a volatility plugin
```
Đề bài cho 2 file là memdump.mem.gz và file bitlocker-2.dd, mình gzip -d memdump.mem.gz và nhận được file memdump.mem sau đó mình dùng file memdump.mem thì thấy là kiểu file Windows Event Trace Log
, và mình thử grep thì nhận được flag luôn
picoCTF{...}
```
Volatility là một công cụ mã nguồn mở được dùng trong Digital Forensics (giám định só),
chuyên để phân tích bộ nhớ RAM (memory dump)

Khi trích xuất được ảnh bộ nhớ (memory image) của một máy tính bị nghi nhiễm malware hoặc bị tán công, Volatility giúp "mổ xẻ"' bộ nhớ đó để tìm:
- Tiến trình đang chạy
- File đang mở
- Kết nối mạng
- Mã độc (malware) ẩn
- Lệnh người dùng từng gõ
- Tên người dùng, session, registry, password,v.v.

Trong Volatility, mỗi “chức năng” như pslist, netscan, malfind… đều là một plugin.
Plugin = mô-đun phân tích riêng biệt.
pslist	Liệt kê tiến trình
pstree	Cây tiến trình cha-con
dlllist	Liệt kê DLL đang nạp
handles	Các handle (file, socket, mutex, registry)
cmdline	Xem lệnh đã chạy
malfind	Phát hiện mã độc trong tiến trình
netscan	Quét kết nối mạng
filescan	Quét vùng nhớ tìm file
hashdump	Lấy hash mật khẩu từ SAM
shimcache	Trích xuất ứng dụng đã từng chạy
clipboard	Lấy dữ liệu clipboard của người dùng

Volatility thường được dùng để:
Điều tra malware chạy trong RAM
Tìm mật khẩu, session, key còn lưu trong bộ nhớ
Xác định hành vi hacker
Phục hồi file hoặc tiến trình ẩn
Kết hợp với Autopsy, The Sleuth Kit, Wireshark trong các bài CTF hoặc thực tế.
