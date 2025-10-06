# Can you see
Đề bài cho 1 file zip, sau khi unzip thì mình nhận được file ảnh có đuôi .jpg và sau đó mình thử kiểm tra ảnh với lệnh:
```
strings ukn_reality.jpg
```
Thì có rất nhiều kí tự được hiện ra, và mình đã thử đọc những dòng đầu của file bằng lệnh:
```
head -n 10 ukn_reality.jpg
```
Thì mình đã thấy có đoạn base 64 trong đó:
```
┌──(kali㉿kali)-[~/Downloads]
└─$ head -n 10 ukn_reality.jpg 
����JFIFHH��
            7http://ns.adobe.com/xap/1.0/<?xpacket begin='' id='W5M0MpCehiHzreSzNTczkc9d'?>
<x:xmpmeta xmlns:x='adobe:ns:meta/' x:xmptk='Image::ExifTool 11.88'>
<rdf:RDF xmlns:rdf='http://www.w3.org/1999/02/22-rdf-syntax-ns#'>

 <rdf:Description rdf:about=''
  xmlns:cc='http://creativecommons.org/ns#'>
  <cc:attributionURL rdf:resource='cGljb0NURntNRTc0RDQ3QV9ISUREM05fZGVjYTA2ZmJ9Cg=='/>
 </rdf:Description>
</rdf:RDF>
</x:xmpmeta>

```
Thử lấy nó để giải mã thì mình đã nhận được flag:
picoCTF{...}
