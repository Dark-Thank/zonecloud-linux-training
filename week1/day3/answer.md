3.2.5
Đọc được file config.txt vì trainee02 thuộc group webteam, file có permission 640 và group có quyền r-- 

3.2.6
Không đọc được file vì outsider ko thuộc group webteam nên ko có quyền truy tập vào file config.txt

3.3.5 
khi ta gõ bash ./hello.sh
lúc này linux xem file như một chương trình executable muốn chạy thì file phải có quyền x nếu không sẽ bị "permission denied"

3.4 
- Tại sao private key SSH cần permission 600, không được để 644?
-- Tại vì 600 nghĩa là rw------- chỉ owner được đọc và ghi người khác không có quyền gì sẽ giúp bảo mật thông tin 
-- Còn đối với 644 = rw-r--r-- thì user khác trên máy có thể đọc private key của mình, rất nguy hiểm nếu có ssh có thể sẽ vào được server của bạn 

- Permission 777 nguy hiểm ở điểm gì?
-- Tại vì 777 = rwxrwxrwx tức là owner group other điều có full quyền điều này rất nguy hiểm đặc biệt là quyền ghi, hệ thống không được kiểm soát và mất tính bảo mật vì ai cũng có thể đọc, nếu gặp người xấu dễ bị chèn mã đọc vào chương trình hoặc tệ hơn là xóa dữ liệu 

- www-data là user gì, mục đích dùng để làm gì?
-- www-data là hệ thống thường dùng cho web server
-- mục đích để cho phép user có thể truy câp hệ thống mà không cần quyền root phòng tránh các hacker hoặc người tấn công có toàn quyền hệ thống  

- Sự khác nhau giữa adduser và useradd?
-- adduser và useradd đều dùng để tạo user trong Linux, nhưng cách dùng khác nhau 
-- adduser là bản dễ dùng thân thiện với người mới, còn useradd là bản thô, low-level hơn 
-- khi dùng adduser hệ thống sẽ tự hỏi password, tên user, home directory, còn đối với useradd tự làm nhiều hơn, hệ thống ko tự hỏi password, và ko tạo home directory phải thêm option thủ công 
-- đối với adduser ubuntu hay dùng còn đối với useradd CentOS/RHEL hay dùng 

