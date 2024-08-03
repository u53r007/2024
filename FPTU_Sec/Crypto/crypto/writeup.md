## TITLE
>Crypto
## DESCRIPTION
>Flag format: FUSec{...}

>Hãy phân tích chương trình mã hóa sau để giải mã chuỗi sau: ['159.96.34.204', '136.182.188.58', '155.20.31.30', '12.234.113.15', '153.170.118.69', '189.152.240.17', '180.27.111.161', '87.205.101.118', '45.1.136.2', '122.3.3.3']
## CATEGORY
>Crypto
## SCORE
>100
## HINT
>None
## DIFFICULTY
>Super easy
## FLAG
>FUSec{howdyiamnowinyourhanddecrypted}
## SOLVED
Tiếp cận đề bài ta thấy bài đã cho đoạn script để mã hóa đoạn mã trên (encrypt.py). Phân tích đoạn script đó ta thấy nó sử dụng thuật toán mã hóa luồng (stream cipher) để mã hóa plaintext thành các địa chỉ IPv4. Phân tích sâu hơn vào đoạn script ta hiểu sơ đoạn script như sau:

Cách mã hóa của hàm này là:

##### (Hàm cipher):

+ Khởi tạo: Tạo hoán vị ban đầu của mảng 256 bytes S.
+ Key Scheduling Algorithm (KSA): Trộn hoán vị bằng khóa __k__.
+ Pseudo-Random Generation Algorithm (PRGA): Tạo một khóa luồng và XOR nó với dữ liệu __d__ để tạo ra đầu ra được mã hóa và giải mã.

##### (Hàm encr):
+ Chuyển đổi plaintext __pt__  thành byte và mã hóa nó bằng hàm cipher.
+ Thêm phần đệm (padding) để đảm bảo độ dài dữ liệu được mã hóa là bội số của 4 bytes.
+ Chuyển đổi dữ liệu được mã hóa thành danh sách các địa chỉ IPv4 bằng hàm d2ip.

##### (Hàm d2ip):
+ Chia dữ liệu được mã hóa thành các phần 4 bytes.
+ Chuyển đổi mỗi đoạn 4 bytes thành một địa chỉ IPv4.


+ Khóa: __bytearray ('supersecretkey', 'utf-8')__ - Khóa được sử dụng để mã hóa.

Từ kiến thức đó craft file decrypt và giải thôi!

Chạy file decrypt.py và ta sẽ có flag.

> Source tham khảo: [Stream Cipher Algo](https://www.geeksforgeeks.org/stream-ciphers/)

#### END!!
