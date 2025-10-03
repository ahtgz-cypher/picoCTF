# DISKO 1
Khi mình tải file về và extract file ra thì thấy nó có dạng .dd và khi mình thử bằng lệnh để xem nó là file gì thì nhận được kết quả nó 
là file DOS, MBR và khi mình đọc Hint challenge cung cấp là sử dụng strings để làm thì mình đã thử nó với lệnh
```
strings disko-1.dd| grep -i picoCTF{
```
Và mình đã nhận được flag
picoCTF{...}

* MBR (Master Boot Record) là sector đầu tiên của một ổ đĩa (thường có kích thước 512 byte).

* Nó được BIOS đọc đầu tiên khi máy tính khởi động.

* MBR gồm 3 phần chính:

  - Boot code (446 byte đầu)
    → chứa đoạn mã máy nhỏ, nhiệm vụ: tìm phân vùng active rồi nạp boot sector của phân vùng đó để tiếp tục khởi động hệ điều hành.
    → trong CTF/forensics, người ta có thể giấu dữ liệu hoặc flag vào đây.

  - Partition table (64 byte tiếp theo)
      → gồm 4 entry (mỗi entry 16 byte), mô tả tối đa 4 phân vùng chính:

    + Loại phân vùng (NTFS, FAT32, Linux, …)

    + Sector bắt đầu, sector kết thúc

    + Trạng thái active/bootable
      → nếu bạn phân tích phần này, sẽ thấy phân vùng nào tồn tại, có bị ẩn hay không.

* Signature (2 byte cuối = 0x55AA)
  → đánh dấu đây là sector khởi động hợp lệ.

* DOS (Disk Operating System) là hệ điều hành đời đầu của Microsoft (MS-DOS).

* Khi dùng lệnh fdisk /mbr trong DOS, hệ thống sẽ ghi một bản MBR chuẩn của DOS lên ổ đĩa.

* Vì vậy, "DOS MBR" thường ám chỉ một MBR chuẩn được tạo ra bởi DOS.

* MBR không phải là 1 file ảnh bình thường(không có định dạng jpg, txt, ...)
* Nó là ảnh Image(raw) của sector đầu tiên của ổ đĩa
* 
