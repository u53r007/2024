#### TITLE
>Cards
#### DESCRIPTION
> "Người không chơi là người không bao giờ thắng, Người thua là người chưa thắng, Người bỏ cuộc là thất bại, Còn chơi là còn gỡ." - Nhà cái đến từ Tâu Âu. Flag format: FUSec{...}

>nc challenge.fuctf.com 8006
#### CATEGORY
>Pwn
#### SCORE
>100
#### HINT
>None
#### DIFFICULTY
>easy
#### FLAG
>FUSec{th1s_1s_3x4ctly_h0w_my_pwn2own_l00k_l1k3!!}
##### SOLVED
Tiếp cận với đề bài sẽ cho mn 2 files: 1 là file cardg và cái còn lại là file code C cardg.c. Ta bắt đầu khai thác file code C trước, ta sẽ tập trung vào các vị trí sử dụng để nhận input từ người dùng như scanf, fgets, đặc biệt là gets vì nó rất dễ bị buffer overflow. Nhưng trong file code này hơi lắc léo hơn một chút, nó không dùng gets hay scanf để nhận giá trị input trực tiếp mà sử dụng hàm get_int(). Đọc hiểu sơ qua hàm get_int() như sau:
- Nó sử dụng hàm read() từ libC để đọc input vào buf chứa được 16 bytes kí tự.
- Kí tự cuối cùng của buf được cắt bằng null bytes terminator '\0'.
- Hàm atoi() chuyển chuỗi trong buf thành dãy số nguyên.

Qua đó ta sẽ thấy file này không thể thực hiện buffer overflow được bởi nó được cắt bằng '\0' nên nếu có điền số dài quá 16 bytes thì cũng như không, để ý kĩ trong hàm play() cũng thấy, ở phần cược vàng khi nhập số vào thì hàm if sẽ chỉ kiểm tra xem ta có nhập số quá lớn hơn số vàng hiện có hay không thôi. Âu!! Vậy thì ta nhập thử số âm xem sao :)))
![image](https://github.com/uS3rR00t05/2024/assets/165979681/e82332a9-e506-4f9f-9d29-2efcf384bf8e)

Chạy file cardg để thử giả thuyết hoặc netcat lên server để thử nuôn cho phẻ. Nhập một số âm cực lớn, bam tỷ phú trong một nốt nhạc! :)))
![image](https://github.com/uS3rR00t05/2024/assets/165979681/6d0556fa-5753-467d-90e3-9c3a7b99e099)

Xong chúng ta chỉ cần chọn 2 để mua flag thôi.

>[!NOTE]
>Tại sao nhập số âm mà lại trả ra số dương??!! Chương trình bị lỗi tràn số học (arithmetic overflow) mà trong đây là integer overflow.
>![image](https://github.com/uS3rR00t05/2024/assets/165979681/d5b9cd57-a836-4c6c-b82d-43abfa4179e3)

>Source tham khảo: [Integer overflow](https://www.youtube.com/watch?v=Dbbh_lrbgAU)
### END!!
