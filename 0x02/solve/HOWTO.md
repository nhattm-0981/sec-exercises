# Bài 2

Source code cho thấy web sẽ đọc input và so sánh với password lưu trên server bằng hàm strcasecmp.

Flag thì có dạng FLAG_???????????????? với mỗi dấu '?' tương ứng với 1 ký tự trong khoảng A-Za-z.<br>
Brute flag thì không thể vì sẽ có 16^52 flag 
-> Tìm cách khác để  strcasecmp($_POST['password'], $password) trả về 0.<br>

Các hàm so sánh string trong php có một lỗi khi tham số truyền vào là 1 mảng.<br>
```php
$fields = array(
    'id' => '127.0.0.1',
    'ps' => 'bar'
);
$a="danux";
 if (strcmp($a,$fields) == 0){
        echo " This is zero!!";
 }
 else{
       echo "This is not zero";
}
```
Lúc này sẽ có warning về việc strcmp nhận string nhưng tham số thứ 2 lại là mảng.<br>
Tuy nhiên, biểu thức trong if vẫn trả về **true**.

Tận dụng lỗi này, có thể dùng burpsuite để bắt request lên server và đổi input thành mảng rồi gửi lên.<br>

![bắt request](/0x02/solve/b2-1.png)

![sửa request](/0x02/solve/b2-2.png)

Click forward để gửi request đã sửa lên server.<br>
Lúc này **strcasecmp($_POST['password'], $password) == 0** trả về true, s

Flag: **FLAG_VQcTWEK7zZYzvLhX**
