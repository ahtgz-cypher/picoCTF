# Secret_of_the_Polyglot
Description
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?

Đề bài cho một link dẫn đến một file PDF, và có một đoạn mã ở trong file PDF đó:
```
1n_pn9_&_pdf_2a6a1ea8}
```
Và sau đó mình thử tải file PDF đó về để phân tích sâu hơn, sau khi tải xong thì mình thử kiểm tra file bằng lệnh:
```
file flag2of2-final.pdf
```
Thì mình phát hiện nó là file PNG, chứ không phải file PDF, sau đó mình đã thử đổi tên của file lại:
```
mv flag2of2-final.pdf flag2of2-final.png
```
và mở file lại:
```
xdg-open flag2of2-final.png
```
Thì mình đã nhận được đoạn flag còn lại
picoCTF{...}
