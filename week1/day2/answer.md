2.2.1
2026-05-11T22:29:29.346738+07:00 khanh-GF63-Thin-11UD systemd[1271]: Starting blueman-manager.service - Bluetooth Manager...
=> hệ thống đang khởi động bluemen-manager.service là chương trình quản lý bluetooth



2026-05-11T22:29:46.862476+07:00 khanh-GF63-Thin-11UD bluetoothd[719]: src/service.c:btd_service_connect() a2dp-sink profile connect failed for 41:42:70:B2:61:C9: Device or resource busy
=> Bluetoothd là triến trình Bluetooth daemon, máy đang cố kết nối thiết bị Bluetooth 

 
2026-05-11T22:30:01.903877+07:00 khanh-GF63-Thin-11UD CRON[5449]: (root) CMD ([ -x /etc/init.d/anacron ] && if [ ! -d /run/systemd/system ]; then /usr/sbin/invoke-rc.d anacron start >/dev/null; fi)
=> CRON đang chạy một tác vụ tự động theo lịch, kiểm tra và chạy anacron, anacron giúp chạy các job định kỳ bị bỏ lỡ khi máy tắt trước đó 


2.2.3
cat /var/log/syslog | grep -i "error" | tail -20
giải thích 
cat dùng để đọc và in nội dung file ra terminal
/var/log/syslog là file log hệ thống Linux
| pipe này dùng để chuyển output của lệnh bên trái thành input cho lệnh bên phải, kết quả của cat sẽ được gửi sang grep 
grep dùng để tìm kiếm text  
-i giúp không phân biệt hoa/thường 
"error" là từ khóa cần tìm kiếm, tìm từ error 
tail -20 lấy 20 dòng cuối 

2.3 
- less khác cat ở điểm gì? Khi nào dùng less thay vì cat?
-- đối với less là xem file theo từng trang có thể cuộn lên cuộn xuống tìm kiếm 
-- đối với cat là in toàn bộ nội dung file ra terminal một lần và không có cuộn trang 
-- nếu file ngắn thì nên dùng cat còn nếu file dài thì dùng less và sử dụng less nếu muốn tìm kiếm keyword 

- Tại sao tail -f hữu ích hơn tail khi troubleshoot?
-- nếu sử dụng tail thì chỉ hiện các dòng cuối chạy xong là kết thúc luôn 
-- còn đối với tail -f là theo dõi realtime nếu có thay đổi là hiển thị ngay
-- đối với troubleshoot kiểm tra log, tìm lỗi, xác định nguyên nhân... nên khi dùng tail -f thì có thế phát hiện ngay sao khi bấm một lệnh test bất kì 

- Giải thích: command > file.txt 2>&1 (từng phần)
-- command > file.txt 2>&1 câu lệnh này dùng để chuyển output bình thường và lỗi vào cùng 1 file 
-- phần command là lệnh bạn muốn chạy ví dụ như ls /abc 
-- phần > file.txt dấu > dùng để redirect output tức là chuyển ra file.txt 
-- phân 2>&1 2> tức là chuyển lỗi đi nơi khác &1 nghĩa là đến cùng nơi với stdout 



