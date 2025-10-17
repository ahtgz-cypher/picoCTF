# DISKO3
Description
Can you find the flag in this disk image? This time, its not as plain as you think it is!
Download the disk image here.
Hints 
How will you search and extract files in a partition?

Sau khi tải file disko-3.dd.gz và giải nén nó ra thì ta nhận được một file disko-3.dd, và trước hết mình kiểm tra nó bằng lệnh file và sau
đó tìm chuỗi flag bằng lệnh grep thì nhận được kết quả sau:
```
└─$ strings disko-3.dd|grep -i picoCTF
MESSAGE=[system] Activating via systemd: service name='org.bluez' unit='dbus-org.bluez.service' requested by ':1.81' (uid=1000 pid=12105 comm="/usr/share/code/code Desktop/picoctf-2025")

MESSAGE=[system] Activating via systemd: service name='org.bluez' unit='dbus-org.bluez.service' requested by ':1.66' (uid=1000 pid=43129 comm="/usr/share/code/code Desktop/picoctf-2025")
MESSAGE=[system] Activating via systemd: service name='org.bluez' unit='dbus-org.bluez.service' requested by ':1.65' (uid=1000 pid=2141 comm="/usr/share/code/code Desktop/picoctf-2025")
MESSAGE=[system] Activating via systemd: service name='org.bluez' unit='dbus-org.bluez.service' requested by ':1.65' (uid=1000 pid=2584 comm="/usr/share/code/code Desktop/picoctf-2025")
```
Thấy không tìm thấy được gì nên mình đã thử phân tích disk layout bằng lệnh:
```
fdisk -l disko-3.dd
```
Và nhận được kết quả:
```
└─$ fdisk -l disko-3.dd
Disk disko-3.dd: 100 MiB, 104857600 bytes, 204800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000
```
Không thấy có phân vùng rõ ràng, điều này có nghĩa là file system được ghi trực tiếp vào hình ảnh.
Sau dó mình đã thử Mount the Disk image
```
sudo mkdir /tmp/disko-3
sudo mount -o loop disko-3.dd /tmp/disko-3
```
Sau khi mount, mình đã thử list nội dung ở đó:
```
ls /tmp/disko-3
```
Sau dó mình thấy file có tên log và mình thử đi sâu thêm nữa:
```
ls -la /tmp/disko-3/log
```
Thì mình quan sát 1 lượt và thấy có file flag.gz, sau dó mình copy file và unzip nó ra:
```
cp /tmp/disko-3/log/flag.gz .
unzip flag.gz
cat flag
```
Và mình đã nhận được flag:
picoCTF{...}

- fdisk -l: liệt kê bảng phân vùng của một thiết bị hoặc một file ảnh đĩa, liệt kê tất cả các ổ đĩa và ảnh có thể đọc được, fdisk -l /dev/sdb: liệt kê tất cả các phân vùng của /dev/sdb
-> Kết quả: Cho biết có bao nhiêu partition, bắt đầu, kết thúc ở sector nào, kích thước, kiểu (Linux, NTFS,...). Dùng để biết cần mount offset bao nhiêu khi mount ảnh đĩa

- sudo mount -o loop,ro disko-3.dd /tmp/disko-3
- 
  Trong đó:

  ```
  là để mount(gắn kết) file disko-3.dd - vốn là 1 image(ảnh đĩa) - vào thư mục /tmp/disko-3 để có thể duyệt nội dung của nó như một ổ đĩa thật
  mount: là lệnh dùng để gắn kết hệ thống tập tin
  -o loop: cho phép mount một file image (vd: .dd, .iso, .img,...) như thể nó là một thiết bị đĩa thật

  Quy trình thường dùng:
  mkdir /tmp/disko-3
  sudo mount -o loop disko-3/.dd /tmp/disko-3
  ls /tmp/disko-3
  
  - Nếu file .dd có nhiều phân vùng, thì sẽ cần xác định offset của phân vùng rồi mount thủ công, ví dụ:
  fdisk -l disko-3.dd #Xem thông tin phân vùng
  và sau đó mount
  sudo mount -o loop, offset=$((sector_offset)*512) disko-3.dd /tmp/disko-3
  trong đó sector_offset là giá trị Start sector lấy từ fdisk -l
  ```
  -o loop: o là option, gắn file như một block device ảo
  
  ro: read-only

  Xem partition table dùng: mmls disko-3.dd
  hoặc
  fdisk -l disko-3.dd
  
  offset = start sector + sector size
  VD: 2048 * 512 = 1048576

  sudo mount -o loop,offset=1048576 disko-3.dd /tmp/disko-3

  - Lưu ý:
    + Luôn mount read-only (ro) để tránh làm thay đổi evidence
    + Trước khi mount, tốt nhất dùng mmls/fdisk -l để xác định offset chính xác
    + dd hay losetup có thể dùng để trích partition riêng ra
