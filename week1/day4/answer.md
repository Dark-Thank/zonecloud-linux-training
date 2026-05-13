4.2.1 
Chạy top, chụp màn hình và giải thích:
- 3 con số load average là gì?
Ví dụ load average: 0,48, 0,49, 0,49
Ba số này là mức tải trung bình của hệ thống trong
-- số thứ nhất 0.15 -> 1 phút gần nhất 
-- số thứ hai -> 5 phút gần nhất 
-- số thứ ba -> 15 phút gần nhất 
==> Máy đăng chỉ sử đụng khoảng 50% hiệu năng và điều giữ ổn định trong 15 phút vì ko có task sử dụng CPU lớn 

- %us, %sy, %id trong CPU stats là gì?
Ví dụ: %Cpu(s):  1,0 us,  0,4 sy,  98,5 id
Thông số us biểu thị CPU dùng cho ứng dụng người dùng, trong ví dụ là 1% 
Thông số sy biểu thị CPU dùng cho hệ thống Linux, trong ví dụ là 0.4% 
Thông số id biểu thị CPU đang rảnh, trong ví dụ là 98.5% 


- Tìm process dùng nhiều CPU nhất
op - 15:56:47 up 32 min,  1 user,  load average: 0,48, 0,49, 0,49
Tasks: 334 total,   2 running, 332 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1,0 us,  0,4 sy,  0,0 ni, 98,5 id,  0,1 wa,  0,0 hi,  0,0 si,  0,0 st 
MiB Mem :   7642,1 total,   2783,9 free,   3205,1 used,   2260,3 buff/cache 
MiB Swap:      0,0 total,      0,0 free,      0,0 used.   4437,1 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND 
   2758 khanh     20   0 1448,5g 496468 158420 S   5,3   6,3   1:56.44 chrome 
   3921 khanh     20   0 1450,4g 412296 166960 S   3,7   5,3   0:59.03 chrome 
   2315 khanh     20   0   49,1g 230736 142948 S   2,0   2,9   1:02.89 chrome 
   1640 khanh     20   0 4709668 217808 122336 R   1,2   2,8   0:52.68 cinnamon
==> Trong trường hợp này thì process có PID = 2758 có lượng % CPU là 5.3 là process dùng nhiều CPU nhất, ứng dụng có tên chrome 

4.2.2 
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training/week1/day4$ free -h 
               total        used        free      shared  buff/cache   available
Mem:           7,5Gi       3,6Gi       2,2Gi       530Mi       2,5Gi       3,9Gi
Swap:             0B          0B          0B
==> giải thích các cột: total, used, free, buff/cache, available
- total là tổng dung lương RAM: 7.5Gi
- used là RAM đang sử dụng: 3.6Gi
- free là RAM hoàn toàn chưa dùng tới: 2.6Gi 
- buff/cache là RAM Linux dùng để làm các tác vụ như (cache file, buffer, tăng tốc hệ thống): 2.5Gi 
- available là lương RAM thực tế còn có thể sử dụng thêm, là chỉ số quan trọng để biết máy còn đủ RAM hay không: 3.9Gi 


4.2.3
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training/week1/day4$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           765M  1,9M  763M   1% /run
efivarfs        192K  128K   60K  69% /sys/firmware/efi/efivars
/dev/nvme0n1p5  127G   11G  111G   9% /
tmpfs           3,8G   80M  3,7G   3% /dev/shm
tmpfs           5,0M  8,0K  5,0M   1% /run/lock
/dev/nvme0n1p1  296M   38M  259M  13% /boot/efi
tmpfs           765M  192K  765M   1% /run/user/1000
/dev/nvme0n1p6   40G   26G   14G  67% /media/khanh/Học Tập
/dev/nvme0n1p4   54G   21G   34G  38% /media/khanh/Disk

- Partition nào đang dùng nhiều nhất?
Nhìn vào thông tin thấy được /dev/nvme0n1p6 có partition /media/khanh/Học Tập dùng nhiều nhất vì có Use% đến 67% 
Đặc biết ở chỗ ở filesystem efivarfs có user% đến 69% nhưng vì do đây không phải là partition lưu dữ liệu bình thường nền không tính khi phân tích dung lượng ổ đĩa 

- Partition / còn bao nhiêu dung lượng?
partition / là /dev/nvme0n1p5 ở cột Avail có 111G, chứng tỏa còn 111GB dung lượng trống 

4.2.4 
khanh@khanh-GF63-Thin-11UD:/media/khanh/Disk/ZoneCloudTraining/zonecloud-linux-training/week1/day4$ du -sh /var/log/* | sort -rh | head -10
du: cannot read directory '/var/log/private': Permission denied
du: cannot read directory '/var/log/speech-dispatcher': Permission denied
168M	/var/log/journal
4,0M	/var/log/syslog
2,6M	/var/log/installer
1,5M	/var/log/kern.log
336K	/var/log/lightdm
156K	/var/log/apt
148K	/var/log/auth.log
124K	/var/log/boot.log
96K	/var/log/dmesg.0
92K	/var/log/dpkg.log
==> Nhìn vào thông tin ta thấy được 168M /var/log/journal là thư mục lớn nhất trong /var/log 


