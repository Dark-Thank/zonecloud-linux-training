/etc chứa gì? /var/log chứa gì? /tmp có gì đặc biệt?
+ /etc dùng để chứa các file cấu hình của hệ thống 
+ /var/log dùng để chưa các file log hay còn gọi là file nhật ký, nó ghi lại các thao tác mình đã làm 
+  /tmp dùng để chưa các file tạm thời, nó đặc biệt ở chỗ ai cũng có thể ghi vào, dùng cho dữ liệu tạm thời 

Sự khác nhau giữa /usr/bin và /sbin?
+  Giống nhau là cả 2 điều
- chứa các file thực thi
- chứa các câu lệnh của Linux 
- dùng để chạy chương trình từ terminal 
+ Khác nhau 
- /usr/bin 
-- chứa lệnh cho user bình thường 
-- ai cũng thường dùng 
-- không nhất thiết cần quyền root 
- /sbin
-- chứa lệnh quản trị hệ thống 
-- chủ yếu admin/root dùng  

absolute path và relative path khác nhau thế nào? Cho ví dụ.
+ Absolute đường dẫn đầy đủ bắt đầu từ / , dù đang ở đâu vẫn truy cập đúng file đó 
Ví Dụ 
đang đứng ở /home/khanh và gõ /home/khanh/Documents/test.txt thì vẫn có thể mở file test.txt 

+ Relative path là đường dẫn tính từ thư mục hiện tại 
Ví dụ 
đang đứng ở /home/khanh mà muốn ở /home/khanh/Documents/test.txt thì ghi là Document/test.txt 

==> Nói chùng là Absolute chỉ cần cho đường dẫn bắt đầu từ / dù đang đứng đâu cũng mở được nhưng relative thì chỉ tính từ chỗ đúng mà chỉ mở được các thành phần con trong chỗ đứng đó 




