- Disk_image là một bản sao chính xác (bit by bit) của toàn bộ nội dung trên một thiết bị lưu trữ
VD: ổ cứng, USB, thẻ nhớ, hoặc CD, DVD
- Nó lưu lại mọi thứ có trên thiết bị thật từ dữ liệu, phân vùng, hệ thống tệp(file system), đến các vùng chưa sử dụng (unlocated), và cả phần bị xóa
* Cấu trúc bên trong của một disk image
  Một file ảnh đĩa có thể chứa:
  + MBR/GPT: Bảng phân vùng (partition table), lưu thông tin về các phân vùng trên ổ
  + Phân vùng(Partition): Các khu vực chứa hệ điều hành, dữ liệu người dùng,...
  + File system: Cấu trúc tổ chứa file(FAT32, NTFS, ext4,...)
  + Unallocated space: Vùng trống hoặc đã bị xóa nhưng vẫn còn dữ liệu thô

* Định dạng thường gặp của disk image:
  - .dd: Ảnh đĩa dạng raw, bản sao từng bit(do lệnh dd tạo)
  - .img: Giống .dd, chỉ khác phần mở rộng
  - .E01: Ảnh forensic(EnCase), có metadata và hash bảo toàn
  - .iso: Ảnh đĩa CD/DVD, chứa hệ thống file ISO9660
* Mục đích sử dụng trong Forensics
  Trong digital forensics việc tạo disk image giúp:
  + Bảo toàn chứng cứ gốc: bạn không can thiệp trực tiếp vào ổ thật (đảm bảo tính toàn vẹn)
  + Phân tích an toàn: làm việc trên bản sao (image), không làm thay đổi dữ liệu bạn đầu
  + Tìm flag hoặc file bị xóa: dùng công cụ để khám phá, khôi phục, tìm kiếm dấu vết
  VD:
    - mmls disko.dd: Xem cấu trúc phân vùng
    - fls -o 2048 disko.dd: Liệt kê file trong phân vùng Linux
    - icat -o 2048 disko.dd 128: Trích xuất file theo inode
* Cách tạo một disk image:
  - Tạo từ thiết bị thật(vd: /dev/sdb): sudo dd if=/dev/sdb of=usb_copy.dd bs=4M conv=noerror,sync
    Giải thích:
    bs=4M: đọc ghi 4MB/lần
    noerror,sync: bỏ qua lỗi đọc nhưng vẫn giữ kích thước đúng
    * Có thể dùng strings, binwalk, photorec để khôi phục dữ liệu ẩn

* Tóm lại:
  - Bản sao: Bit-by-bit của ổ đĩa hoặc thiết bị
  - Dạng file: .dd, .img, .E01, .iso,...
  - Dùng để: Phân tích, phục hồi, bảo toàn chứng cứ
  - Không chỉ chứa file: mà cả MBR, phân vùng, vùng trống, vùng xóa
  - Tạo bằng: dd, dc3dd,...
