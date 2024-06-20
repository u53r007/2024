#### TITLE
>Basic Steganography
#### DESCRIPTION
> Flag format: FUSec{...}

> During the process of collecting digital evidence, you (a member of the digital investigation team) suspect that an image file (fictory.jpg) is obtained that has hidden information inside. Let's try to find that information.
#### CATEGORY
>Forensic
#### SCORE
>100
#### HINT
>None
#### DIFFICULTY
>Easy
#### FLAG
>FUSec{70VictoryDienBienPhu}
#### SOLVED
Tiếp cận đề bài ta được cho một bức hình (fictory.jpg). Việc đầu tiên nên làm tất nhiên là mở bức hình xem nó là cái gì đã. Bức hình thì quá nổi tiếng rồi nhưng cũng không có gì đặc sắc liên quan tới flag chúng ta cần. Sau đó chúng ta nên extract metadata:

> exiftool fictory.jpg

![image](https://github.com/u53r007/2024/assets/165979681/874ad9ea-7cf0-452a-acbe-0ff5d2599ebe)

Ta phát hiện ra extension .jpg chỉ là giả 🤡. Extension thật sự của bức hình là .webp. Sau đó mình có thực hiện các cách để thử các cách để tìm data ẩn trong bức hình như steghide, binwalk, extract LSB các kiểu,... nhưng hoàn toàn vô vọng. Cuối cùng mình thử extract hex của bức hình.

> xxd fictory.jpg

![image](https://github.com/u53r007/2024/assets/165979681/31c07384-3f37-491d-aaa9-e676663bf635)

Và nó ra luôn :)) Ảo thật đấy!!

### END!!
