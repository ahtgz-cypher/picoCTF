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
sudo mount -o  disko-3.dd /tmp/disko-3
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
