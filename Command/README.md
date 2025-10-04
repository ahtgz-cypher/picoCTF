# Các lệnh thường dùng trong Digital Forensics
## Nhóm lệnh phân tích file và dữ liệu:
```
file: dùng để kiểm tra loại file dựa trên header (rất hữu ích để phát hiện các file bị đổi đuôi

strings: dùng để trích xuất các chuỗi ASCII có thể đọc được từ file nhị phân

xxd: Hiển thị nội dung file dưới dạng hex (hexdump)

binwalk: Phân tích các file nhị phân để tìm phần nhúng (như ảnh, firmware,...)

foremost: Dùng để khôi phục file bị xóa hoặc bị ẩn trong ảnh đĩa

exiftool: Trích xuất metadata từ ảnh, video, tài liệu (rất hữu ích trong phân tích ảnh)

hashdeep: Tạo và so sánh hash của 2 file để kiểm tra tính toàn vẹn

md5sum, sha256sum: Tính toán hash md5 hoặc sha256 của file
```
## Nhóm lệnh phân tích hệ thống tập tin:
```
mount, unmount: Gắn hoặc tháo ổ đĩa, ảnh đĩa

df, du: Kiểm tra dung lượng ổ đĩa và thư mục

find, grep: Tìm kiếm file hoặc nội dung trong file

stat: Xem thông tin chi tiết về file (thời gian tạo, sửa, quyền,...)
```
## Các tùy chọn thường gặp và ý nghĩa
```
-d: Directory (thư mục) hoặc Debug
VD: ls -d */: Hiển thị chỉ thư mục thay vì nội dung bên trong, và /* dùng để biểu thị rằng câu lệnh đã kết thúc 
để máy hiểu

-c: Count, check, color
VD: grep -c "flag" file.txt: đếm số dòng chứa flag

-r: Recursive(đệ quy)
VD: grep -r "flag" /home/: Tìm flag trong toàn bộ thư mục

-i: ignore case(không phân biệt hoa thường)
VD: grep -i "flag" file.txt: Tìm "flag", "Flag", "FLAG",...

-n: number, hiển thị số dòng
VD: grep -n "flag" file.txt: hiển thị số dòng chứa từ khóa

-v: invert match(loại trừ kết quả khớp)
VD: grep -v "flag" file.txt: Hiển thị dòng không chứa flag

-a: Treat binary as text
VD: grep -a "flag" image.jpg: Tìm chuỗi trong file nhị phân

-t: Time hoặc Tab
VD: ls -lt: Sắp xếp theo thời gian sửa đổi

-l: Long format hoặc list
VD: ls -l: Hiển thị chi tiết file

-f: force hoặc file
VD: rm -f file.txt: Xóa file không cần xác nhận

-p: Preserve hoặc path
VD: mkdir -p a/b/c: Tạo thư mục lồng nhau

-s: Silent hoặc size
VD: du -sh folder/: Hiển thị dung lượng thư mục

-u: User hoặc update
VD: chown -u hoang file.txt: Thay đổi chủ sở hữu file

-x: Execute hoặc Exclude
VD: chmod +x script.sh: Cho phép thực thi file
```
Một số ví dụ:
```
grep -r -i "flag": Tìm từ flag không phân biệt chữ hoa chữ thường trong toàn bộ thư mục hiện tại
grep -a "password" memory.dump: Tìm chuỗi trong file nhị phân như RAM, dump

ls -l: Hiển thị chi tiết file
ls -lt: Sắp xếp theo thời gian sửa đổi
ls -d */: Chỉ hiển thị thư mục

rm -rf folder/: Xóa thư mục và toàn bộ nội dung bên trong mà không hỏi lại

chmod +x script.sh: Cho phép file thực thi
chmod -R 755 folder/: Gán quyền cho toàn bộ thư mục và file bên trong
```
Mẹo hay khi dùng tùy chọn:
- Dùng man tên_lệnh để xem tất cả các tùy chọn: man grep
- Dùng --help để xem nhanh: grep --help
- Kết hợp nhiều tùy chọn: ls -lh(Hiển thị chi tiết + dung lượng dễ đọc)
