# NGINX Basics & Best Practices

Sau khi hoàn thành bài tập thực hành với slide **NGINX: Basics and Best Practices**, em đã học được những kiến thức sau:

---

## Những Gì Đã Học

### 1. NGINX là gì
- Web server: phục vụ file tĩnh trực tiếp từ ổ cứng
- Application gateway: cầu nối đến backend PHP, Python, Node.js qua FastCGI, uWSGI
- Reverse proxy: nhận request từ client, chuyển tiếp đến server backend, hỗ trợ caching và load balancing

### 2. Cài đặt
- **Mainline** — phiên bản được khuyến nghị, cập nhật thường xuyên với tính năng mới
- **Stable** — chỉ cập nhật khi có lỗi nghiêm trọng hoặc lỗ hổng bảo mật
- Cài đặt trên Ubuntu qua repo chính thức của NGINX

### 3. Lệnh và file quan trọng
- `nginx -t` — kiểm tra cú pháp cấu hình
- `nginx -s reload` — reload không làm gián đoạn traffic
- `nginx -T` — in toàn bộ cấu hình hiện tại
- `/etc/nginx/nginx.conf` — file cấu hình chính
- `/etc/nginx/sites-available/` — cấu hình từng website

### 4. Web server cơ bản
- `server` block — định nghĩa virtual server
- `listen` — cổng lắng nghe
- `server_name` — tên miền
- `root` — thư mục chứa file tĩnh
- `index` — file mặc định trả về

### 5. SSL/HTTPS
- Redirect HTTP → HTTPS bằng `return 301`
- Cấu hình certificate với `ssl_certificate` và `ssl_certificate_key`
- Dùng **Let's Encrypt** để có certificate miễn phí

### 6. PHP-FPM
- NGINX không tự xử lý PHP, chuyển qua PHP-FPM bằng `fastcgi_pass`
- Cấu hình `fastcgi_param SCRIPT_FILENAME` để PHP-FPM biết file cần chạy

### 7. Load Balancing
- **Round Robin** — mặc định, phân phối lần lượt đều nhau
- **Least Connections** (`least_conn`) — gửi đến server ít kết nối nhất
- **IP Hash** — cùng IP luôn vào cùng một server

### 8. Caching
- `proxy_cache` — bật caching
- `proxy_cache_lock` — tránh thundering herd khi nhiều client cùng cache miss
- `proxy_cache_revalidate` — kiểm tra file có thay đổi trước khi tải lại

### 9. Tối ưu hiệu suất
- **Keepalive** — tái sử dụng kết nối TCP thay vì mở/đóng mỗi request
- **HTTP/2** — nhiều request chạy song song trên một kết nối
- **SSL session cache** — lưu session SSL để bỏ qua handshake lần sau
- **worker_processes auto** — tận dụng tối đa số CPU core

### 10. Health Checks & Monitoring
- **stub_status** — theo dõi thống kê cơ bản của NGINX (miễn phí)
- **Prometheus + Grafana** — dashboard monitoring trực quan, miễn phí
- **NGINX Plus** — health check chủ động, extended status (trả phí)

---

## Cấu hình thực hành

File `mysite` cuối cùng sau toàn bộ bài tập:

```nginx
proxy_cache_path /var/cache/nginx
                 levels=1:2
                 keys_zone=my_cache:10m
                 max_size=10g
                 inactive=60m
                 use_temp_path=off;

upstream my_upstream {
    server 127.0.0.1:8080 max_fails=3 fail_timeout=30s;
    server 127.0.0.1:8081 max_fails=3 fail_timeout=30s;
    least_conn;
    keepalive 32;
}

server {
    listen 80 default_server;
    server_name localhost;

    location /basic_status {
        stub_status;
        allow 127.0.0.1;
        deny all;
    }

    location / {
        return 301 https://$server_name$request_uri;
    }
}

server {
    listen 443 ssl http2 default_server;
    server_name localhost;

    ssl_certificate     /etc/nginx/cert.crt;
    ssl_certificate_key /etc/nginx/cert.key;
    ssl_session_cache   shared:SSL:10m;
    ssl_session_timeout 10m;

    root  /usr/share/nginx/html;
    index index.php index.html index.htm;

    location / {
        proxy_cache my_cache;
        proxy_cache_lock on;
        proxy_cache_revalidate on;
        proxy_set_header Host $host;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
        proxy_pass http://my_upstream;
    }

    location ~ [^/]\.php(/|$) {
        fastcgi_split_path_info ^(.+?\.php)(/.*)$;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location /basic_status {
        stub_status;
        allow 127.0.0.1;
        deny all;
    }
}
```

---

## Stack Monitoring (Miễn phí)

```
NGINX (stub_status)
       ↓
nginx-prometheus-exporter  :9113
       ↓
Prometheus                 :9090
       ↓
Grafana                    :3000
```
