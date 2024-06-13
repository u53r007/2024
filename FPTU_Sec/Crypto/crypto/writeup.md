#### TITLE
>Crypto
#### DESCRIPTION
>Flag format: FUSec{...}

>Hãy phân tích chương trình mã hóa sau để giải mã chuỗi sau: ['159.96.34.204', '136.182.188.58', '155.20.31.30', '12.234.113.15', '153.170.118.69', '189.152.240.17', '180.27.111.161', '87.205.101.118', '45.1.136.2', '122.3.3.3']
#### CATEGORY
>Crypto
#### SCORE
>100
#### HINT
>None
#### DIFFICULTY
>Super easy
#### FLAG
>FUSec{howdyiamnowinyourhanddecrypted}
#### SOLVED
Tiếp cận đề bài ta thấy bài đã cho đoạn script để mã hóa đoạn mã trên (encrypt.py). Phân tích đoạn script đó ta thấy nó sử dụng thuật toán mã hóa luồng (stream cipher) để mã hóa plaintext thành các địa chỉ IPv4. Phân tích sâu hơn vào đoạn script ta chỉ cần chú ý đến hàm encr() thực hiện chức năng mã hóa:

![image](https://github.com/u53r007/2024/assets/165979681/b54dbc76-e573-458f-870b-14557b464098)

Cách mã hóa của hàm này là:

+ __pt.encode('utf-8')__:  plaintext (__pt__) được mã hóa thành UTF-8 bytes.

+ __ed = cipher(k, pt.encode('utf-8'))__: plaintext được mã hóa UTF-8 được chuyển đến hàm cipher() mã hóa cùng với khóa (__k__). Hàm cipher() áp dụng thuật toán mã hóa luồng (tương tự như RC4) cho plaintext, tạo ra dữ liệu được mã hóa (__ed__).

+ __padding_length = (4 - len(ed) % 4) % 4__: Tính toán độ dài chuỗi đệm cần thiết để làm cho độ dài của plaintext được mã hóa là bội số của 4 do địa chỉ IP dài 4 bytes.

+ __ed += bytes([padding_length] * padding_length)__: Dữ liệu được thêm giá trị chiều dài chuỗi đệm vào. Điều này đảm bảo rằng khi giải mã, lớp đệm có thể được xác định và loại bỏ.

+ __ipa = d2ip(ed)__: Dữ liệu được mã hóa xong xuôi được chuyển đến hàm d2ip() để chuyển dữ liệu thành danh sách các địa chỉ IP. Mỗi nhóm 4 bytes được chuyển đổi thành một địa chỉ IP.

Bây giờ ta thực hiện đảo ngược hàm encr() từ mã hóa thành giải mã và hàm d2ip() (sử dụng hàm ip2d() tìm hiểu thêm dùng chat gờ bê tê) để phân giải ngược IPv4 lại thành bytearray. Ta có thể nhờ sự trợ giúp của Chat gờ bê tê để thực hiện đảo ngược các hàm đó. (decrypt.py)

![image](https://github.com/u53r007/2024/assets/165979681/15a711fd-7f76-4b62-81fd-d3f7423bd070)

+ __d = ip2d(ipa)__: hàm ip2d() chuyển đổi danh sách địa chỉ IP (__ipa__) trở lại thành bytearray (__d__).

+ __padding_length = d[-1]__: Byte cuối cùng của bytearray được sử dụng để xác định chiều dài đệm.

+ __d[:-padding_length]__: Xóa chuỗi đệm.

+ __ed = decipher(k, d[:-padding_length])__:  Hàm decipher() được gọi bằng khóa (__k__) và dữ liệu được mã hóa không đệm UTF-8 được truyền vào để giải mã UTF-8.

Chạy file decrypt.py và ta sẽ có flag.

> Source tham khảo: [Stream Cipher Algo](https://www.geeksforgeeks.org/stream-ciphers/)

### END!!
