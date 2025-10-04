# Ph4nt0m 1ntrud3r
Bài cho một file pcap và sau khi mở file lên thì mình thấy có những giao thức TCP và Time thậm chí còn bị âm, mình ấn vào từng giao thức thì thấy chúng có các đoạn mã 
base64, sau đó mình thử copy đoạn base64 ở No.1 và decode nó ra thì thấy kí tự 1t_w4s và sau đó mình đã dùng lệnh này để lấy tất cả các base64 ở đó theo thứ tự đúng theo 
thời gian:
```
tshark -r (file) -Y "tcp.len==4||tcp.len==8||tcp.len==12" -T fields -e tcp.segment_data -e frame.time| sort -k2|awk '{print $1}'|xxd -p -r|base64 -d
```
Và mình đã nhận được flag
pico{...}

## Thành phần
-Y: lọc các gói tin
-T fields: Xuất dữ liệu dưới dạng các trường cụ thể (thay vì toàn bộ gói tin)
-e tcp.segment_data: Trích xuất phần dữ liệu TCP(payload)
-e frame.time: Trich xuất thời gian bắt gói tin(để sắp xếp sau này)
## Chức năng
-sort -k2: Sắp xếp các dòng theo cột thứ 2(thời gian), đảm bảo thứ tự gói tin đúng theo thời gian
-awk '{print $1}': Chỉ lấy cột đầu tiên(tcp.segment_data), bỏ phần thời gian
-xxd -p -r: Chuyển dữ liệu hex sang nhị phân(raw bytes)

