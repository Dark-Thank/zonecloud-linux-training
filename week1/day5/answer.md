5.1.4 
public key và private key đang ở trong /home/khanh/.ssh 
vì khi tạo mình chọn nơi này để lưu 

5.2.1
IP của interface chính
3: wlo1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether f4:26:79:c5:37:d0 brd ff:ff:ff:ff:ff:ff
    altname wlp0s20f3
    inet 192.168.50.99/24 brd 192.168.50.255 scope global dynamic noprefixroute wlo1
       valid_lft 72731sec preferred_lft 72731sec
    inet6 fe80::b985:c06f:8a9:1d97/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

5.2.3
khanh@khanh-GF63-Thin-11UD:~$ ss -tulnp
Netid   State    Recv-Q   Send-Q     Local Address:Port      Peer Address:Port  Process 
udp     UNCONN   0        0             127.0.0.54:53             0.0.0.0:* 
udp     UNCONN   0        0          127.0.0.53%lo:53             0.0.0.0:* 
udp     UNCONN   0        0            224.0.0.251:5353           0.0.0.0:*      users:(("chrome",pid=2270,fd=437)) 
udp     UNCONN   0        0            224.0.0.251:5353           0.0.0.0:*      users:(("chrome",pid=2318,fd=107)) 
udp     UNCONN   0        0                0.0.0.0:5353           0.0.0.0:* 
udp     UNCONN   0        0                0.0.0.0:34364          0.0.0.0:*
udp     UNCONN   0        0                   [::]:40526             [::]:*
udp     UNCONN   0        0                   [::]:5353              [::]:* 
tcp     LISTEN   0        511              0.0.0.0:80             0.0.0.0:*
tcp     LISTEN   0        4096             0.0.0.0:22             0.0.0.0:* 
tcp     LISTEN   0        4096          127.0.0.54:53             0.0.0.0:* 
tcp     LISTEN   0        4096           127.0.0.1:631            0.0.0.0:*
tcp     LISTEN   0        4096       127.0.0.53%lo:53             0.0.0.0:*
tcp     LISTEN   0        511                 [::]:80                [::]:* 
tcp     LISTEN   0        4096                [::]:22                [::]:* 
tcp     LISTEN   0        4096               [::1]:631               [::]:* 
==> mình thấy được out tcp LISTEN 0 511 0.0.0.0:80 có port 80 đang ở trạng thái LISTEN điều này nghĩa là Nginx đang chạy và chờ request web
mình thầy được out tcp LISTEN 0 4096 0.0.0.0:22 có port 22 đang ở trạng thái LISTEN điều này nghĩa là SSH server đang chạy và máy cho phép kết nối SSH 

5.2.4 
khanh@khanh-GF63-Thin-11UD:~$ curl -I http://localhost
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
Date: Wed, 13 May 2026 12:20:47 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Tue, 12 May 2026 11:41:07 GMT
Connection: keep-alive
ETag: "6a0311d3-267"
Accept-Ranges: bytes

==> HTTP status có code là 200 
Ý nghĩa là 
request thành công 
web server hoạt động bình thường 
nginx trả về trang web thành công 



