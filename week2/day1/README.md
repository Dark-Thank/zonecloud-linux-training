Kiến thức học được trong tuần 2 - ngày 1 

apt update                          # Cập nhật danh sách package
-> Lệnh này giúp người dùng cập nhật package mới nhất từ nhà phát triển nhưng không làm thay đổi các package đang sử dụng 

apt upgrade -y                      # Nâng cấp tất cả package
-> Lệnh này giúp người dùng nâng cấp package mới từ nhà phát triển, nói dễ hiểu nó là nâng cấp liên phiên bản mới nhất 

apt install nginx curl wget -y      # Cài nhiều package cùng lúc
-> Lệnh này giúp người dùng cài nhiều package cùng lúc hoặc cài package mới 

apt remove nginx                    # Gỡ cài đặt (giữ config)
-> Lệnh này giúp người dùng gỡ bỏ chường trình trên máy, nhưng chỉ là gỡ chương trình thôi còn các file tài nguyên của chương trình vẫn giữ lại, có thể tái sử dụng khi người dùng cài chương trình lại 

apt purge nginx                     # Gỡ hoàn toàn (xóa cả config)
-> Lênh này cũng là lệnh để gỡ bỏ chương trình khác với remove, nó sẽ xóa hết tất cả những tài liệu của chương trình luôn, và khi cài lại sẽ phải cài lại toàn bộ
Note: Nếu bạn muốn tiết kiệm bộ nhớ thì nên chọn purge để tái ưu hóa tài nguyên máy 

apt autoremove                      # Xóa package không còn dùng
-> Lệnh này sẽ giúp xóa đi các package còn sót lại của các chương trình không dùng tới 

apt search keyword                  # Tìm kiếm package
-> Giúp tìm kiếm package của chương trình: ví dụ muốn tìm kiếm các package của chương trình nginx thì gõ apt search nginx, sẽ ra các package của nginx 

apt show nginx                      # Xem thông tin package
-> sẽ giúp xem thông tin ứng package mình đã cài gồm có các thông tin tiêu biểu như:
+ version -- phiên bản package 
+ package -- tên package 
+ section -- loại package 
+ homepage -- link nhà phát triển 
+ download-size -- dung lượng package tải về 
+ priority: mức độ quan trọng với hệ thống 
+ Depends: các dependices của package 


apt list --installed                # Danh sách package đã cài
-> Danh sách package đã cài có thể kết hợp, grep đễ thấy được thư mục cần coi: apt list --installed | grep python

apt list --installed | grep nginx   # Kiểm tra package đã cài chưa
-> Kiểm tra chính xác package cần, coi có cài đặt chưa 

dpkg -l nginx                       # Kiểm tra bằng dpkg
--> câu lệnh ngày cũng gần giống với câu lệnh apt list --installed | grep nginx có điểu câu lệnh này tuy là nằm ở dpkg là, tầng thấp hơn so với apt nhưng lại chi tiết hơn, đặc biệt là nó có thể coi rc (đã gỡ nhưng còn config), un (chưa cài bao giờ) 


dpkg -L nginx                       # Xem file nào được cài bởi package
--> câu lệnh này giúp chúng ta biết được nginx đã cài những file nào vào máy 
