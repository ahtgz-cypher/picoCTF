# RED
Đề bài cung cấp cho mình một file red.png, đó thực sự là một file ảnh, và mình đã thử cat file thì thấy có một đoạn nội dung của file, nhưng mình nghĩ nó không liên quan
đến flag. Sau đó mình thử test chương trình với lệnh 
```
exiftool red.png
```
Thì mình lại thấy một đoạn nội dung nữa, và mình đã vô tình thử ghép những chữ in hoa lại và nhận dòng chữ 
```
CHECKLSB
```
LSB (Least Significant Bit): bit có ý nghĩa thấp nhất trong một đơn vị dữ liệu nhị phân và kĩ thuật này thường được sử dụng trong steganography là nghệ 
thuật giấu thông tin bên trong các tệp số như hình ảnh, video hoặc âm thanh. Và mình tìm hiểu thì biết nó cũng liên quan đến zsteg nên mình đã thử:
 ```
┌──(kali㉿kali)-[~/Downloads]
└─$ zsteg red.png
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."                                                                                                                                                                                                                
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="                                                                                                                                                                                         
b1,rgba,msb,xy      .. file: OpenPGP Public Key
b2,g,lsb,xy         .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"
b2,rgb,lsb,xy       .. file: OpenPGP Secret Key
b2,bgr,msb,xy       .. file: OpenPGP Public Key
b2,rgba,lsb,xy      .. file: OpenPGP Secret Key
b2,rgba,msb,xy      .. text: "CIkiiiII"
b2,abgr,lsb,xy      .. file: OpenPGP Secret Key
b2,abgr,msb,xy      .. text: "iiiaakikk"
b3,rgba,msb,xy      .. text: "#wb#wp#7p"
b3,abgr,msb,xy      .. text: "7r'wb#7p"
b4,b,lsb,xy         .. file: 0421 Alliant compact executable not stripped
 ```
## zsteg 
- Dùng để phát hiện và trích xuất dữ liệu ẩn trong các tệp hình ảnh, đặc biệt là định dạng PNG và BMP, nó phổ biến trong steganograpgy là kĩ thuật
  giấu thông tin trong ảnh mà mắt thường không thể thấy được
  VD: zsteg -a image.png: Quét toàn bộ các phương thức giấu dữ liệu
- Khi nào nên dùng zsteg:
  + Khi nghi ngờ trong ảnh có giấu thông tin bí mật
  + Khi muốn kiểm tra xem trong ảnh có bị giấu dữ liệu hay không
Sau dó mình thử lấy đoạn base64 đó ra decode và mình đã nhận được flag:
pico{...}

