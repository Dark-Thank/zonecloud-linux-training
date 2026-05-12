Sau ngày 3 em học được những thứ như sau
+ Tạo user:  adduser khanh sẽ tạo user tên là khanh 
+ Tạo group: groupadd webteam sẽ tạo group tên là webteam 
+ Thêm user vào group: usermod -aG webteam khanh sẽ thêm được user khanh vao webteam 
+ Để xác nhận coi user tồn tại như thế nào thì gõ id khanh sẽ biết được user khanh đang có trạng thái gì 
+ Để coi group đó có bao nhiêu user thì gõ cat /etc/group | grep webteam 
+ Để đặt owner cho một thư mục thì gõ 
-- chown -R khanh:webteam /opt/zonecloud sao lệnh này thì user khanh là owner của /opt/zonecloud 
+ Để đặt permission cho user thì gõ 
-- chown 750 /opt/zonecloud thì /opt/zonecloud sẽ có permisstion 750 
+ Đăng nhặp vào user t gõ 
su - khanh sẽ đăng nhập vào user khanh sao đó ghi mật khẩu, mật khẩu đúng sẽ đăng nhập vào, nếu user đó có permisstion đủ để vào folder hoặc thư mục thì sẽ mở được 
+ Để thêm quyền execute thì gõ  
-- chmod +x file.sh sau khi gõ các user có thể đọc file này với quyền execute 

