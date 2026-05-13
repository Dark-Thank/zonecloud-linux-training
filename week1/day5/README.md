Sau ngày 5 mình học được kiến thức như sau
+ Tạo được keypair để truy cập vào server bằng lệnh "ssh-keygen -t ed25519 -C "trainee@zonecloud" trong đó ed25519 loại SSH muốn tạo còn "trainee@zonecloud" là comment để biết key này do ai tạo 
+ lệnh ssh-copy-id localhost để copy ssh mới tạo vào trong file authorized_keys của server  
+ hiểu được cách vận hành của private key và public key: khi tạo xong ssh ta của có 2 key private và public public ta sẽ đưa vào trong server còn public key mình sẽ để ở client để cho client có thể truy cập vào server 
+ Kiểm tra IP máy bằng lệnh ip addr show và biết được IP interface chính nằm đâu
+ Ping đến DNS để check xem DNS có hoạt động hay không, vào thực tế mình có thể ping tới DNS của server để check server có hoạt động hay không 
+ gửi request HTTP đến để kiểm tra header của WEB 
+ Để kiểm tra port nào đang LISTEN (đang hoạt động) bằng lệnh ss -tulnp 
