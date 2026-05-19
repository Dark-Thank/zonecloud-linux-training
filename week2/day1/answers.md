day1 - 1.3 - Câu hỏi lý thuyết 

- apt remove khác apt purge ở điểm gì? Khi nào dùng purge?
+ Cả đều là gỡ bỏ chường trình nhưng khác nhau những điểm sau 
+ REMOVE là gỡ binary, là các file máy tính dùng để chạy trực tiếp, những đối với file cấu hình thì không gỡ để khi tải lại thì có thể tái sử dụng 
+ PURGE là gỡ bở hết kể cả config, và khi tải lại thì cài lại từ đầu hoàn toàn 

- apt update khác apt upgrade ở điểm gì?
+ update chỉ tải về danh sách package mới nhất từ repo nó không đụng vào thứ gì đang cài trên máy, kiểu như là kiểu thêm món mới còn món cũ thì cứ để đó 
+ upgrade là nâng cấp các package đang cài lên phiên bản mới nhất, cái file nào cần mới nó sẽ chỉnh sửa cho mới hết  

- Repository là gì? Tại sao cần thêm repo bên ngoài?
+ Repository đơn giản là một kho phần mềm trên internet, mới thứ mới sẽ được nhà phát triển để vào kho đó, và người dùng khi cần thì có thể apt install để tải phiên bản mới nhất về 

- Tại sao nên verify GPG key khi thêm repo bên ngoài?
vì Linux là một hệ điều hành mã nguồn mở nên ai cũng có thể chỉnh sửa, việc chúng ta thêm repo vào là bạn đã tin tưởng code của người khác, nếu như code có mã đọc là một vấn đề lớn 
--> vì vậy GPG key là cơ chế xác minh danh tính, repo chính thức nginx ký tên lên tất cả package của họ bằng private key, khi bạn import GPG key của họ vào máy apt sẽ kiểm tra chữ ký đó mõi lần tải package về, sẽ đảm bảo phần mềm là của phát triển chính thức
--> Nói cho dễ hiểu nó giống như là tem chống giả của nhà sản xuất
