# Bản Văn Nói: Những Gì Tôi Đã Học Được Về NGINX

---

## 1. NGINX Là Gì?

NGINX là một phần mềm máy chủ web mạnh mẽ, có thể đóng nhiều vai trò khác nhau trong hệ thống. Nó có thể hoạt động như một **web server** — tức là phục vụ các file tĩnh như HTML, CSS, hình ảnh trực tiếp từ ổ cứng. Nó cũng có thể hoạt động như một **application gateway** — tức là cầu nối giữa người dùng và các ứng dụng backend như PHP, Python, Node.js thông qua các giao thức FastCGI, uWSGI. Và cuối cùng, nó có thể là một **reverse proxy** — nhận request từ người dùng, chuyển tiếp đến các server khác, đồng thời hỗ trợ caching và load balancing.

---

## 2. Cài Đặt NGINX

Tôi đã học được rằng NGINX có hai phiên bản chính:

- **Mainline** — phiên bản được phát triển tích cực, cập nhật thường xuyên mỗi 4-6 tuần với tính năng mới. Đây là phiên bản được khuyến nghị cho hầu hết các môi trường.
- **Stable** — phiên bản chỉ được cập nhật khi có lỗi nghiêm trọng hoặc lỗ hổng bảo mật.

Trên Ubuntu/Debian, cài đặt bằng cách thêm repo chính thức của NGINX vào hệ thống, sau đó chạy `apt-get install nginx`. Trên CentOS/Red Hat, tạo file repo trong `/etc/yum.repos.d/` rồi chạy `yum install nginx`.

---

## 3. Các Lệnh và File Quan Trọng

Sau khi cài đặt, có một số lệnh quan trọng cần nhớ:

- `nginx -t` — kiểm tra cú pháp file cấu hình có lỗi không
- `nginx -s reload` — reload NGINX mà không làm gián đoạn traffic
- `nginx -T` — in toàn bộ cấu hình hiện tại ra màn hình
- `nginx -V` — xem thông tin chi tiết về phiên bản và các module đã cài

Về cấu trúc thư mục, tất cả cấu hình nằm trong `/etc/nginx/`. File cấu hình chính là `/etc/nginx/nginx.conf`, còn cấu hình cho từng website thường đặt trong `/etc/nginx/conf.d/` hoặc `/etc/nginx/sites-available/`.

---

## 4. Cấu Hình Web Server Cơ Bản

Cấu hình cơ bản nhất của NGINX bao gồm một block `server` với các thành phần:

- `listen 80 default_server` — lắng nghe trên cổng 80, và đây là server mặc định nếu không có hostname nào khớp
- `server_name` — tên miền của virtual server
- `location /` — xử lý tất cả request
- `root` — thư mục chứa file tĩnh
- `index` — file mặc định trả về khi truy cập thư mục

Ví dụ, nếu `root` là `/usr/share/nginx/html`, thì khi người dùng truy cập `www.example.com`, NGINX sẽ trả về file `/usr/share/nginx/html/index.html`.

---

## 5. Cấu Hình SSL (HTTPS)

Để bảo mật website, tôi học được cách cấu hình SSL với hai server block:

- Block đầu tiên lắng nghe cổng 80 (HTTP) và tự động redirect tất cả traffic sang HTTPS bằng `return 301`
- Block thứ hai lắng nghe cổng 443 với `ssl` và chỉ định file certificate (`ssl_certificate`) và private key (`ssl_certificate_key`)

Việc force tất cả traffic sang HTTPS không chỉ tốt cho bảo mật mà còn cải thiện SEO. Trong môi trường thực tế, nên dùng **Let's Encrypt** để có certificate miễn phí và được tin cậy.

---

## 6. Reverse Proxy với PHP-FPM

NGINX không tự xử lý được code PHP. Thay vào đó, nó chuyển các request PHP sang **PHP-FPM** (FastCGI Process Manager) để xử lý. Cấu hình này dùng `fastcgi_pass` để chỉ định socket của PHP-FPM, và `fastcgi_param SCRIPT_FILENAME` để PHP-FPM biết file nào cần chạy.

---

## 7. Load Balancing

NGINX có khả năng phân phối traffic đến nhiều server backend thông qua block `upstream`. Tôi đã học về các thuật toán:

- **Round Robin** — mặc định, phân phối lần lượt đều nhau
- **Least Connections** (`least_conn`) — gửi request đến server đang có ít kết nối nhất, phù hợp khi các request có thời gian xử lý khác nhau
- **IP Hash** — cùng một IP luôn vào cùng một server

Ngoài ra, `proxy_set_header Host $host` rất quan trọng để giữ nguyên tên miền gốc của client khi chuyển tiếp request đến backend.

---

## 8. Caching

Caching giúp NGINX lưu kết quả của các request trước đó, và trả về ngay lập tức cho các request tương tự mà không cần hỏi backend, giúp tăng tốc độ và giảm tải server.

Cấu hình caching bao gồm:
- `proxy_cache_path` — định nghĩa vị trí lưu cache trên ổ cứng, kích thước tối đa, thời gian giữ cache
- `proxy_cache` — bật caching cho context hiện tại
- `proxy_cache_lock` — khi nhiều client cùng cache miss cho cùng một file, chỉ gửi một request đến backend, các client khác chờ kết quả, tránh hiện tượng "thundering herd"
- `proxy_cache_revalidate` — thay vì tải lại hoàn toàn, NGINX hỏi backend xem file có thay đổi không trước, tiết kiệm băng thông

---

## 9. Tối Ưu Hiệu Suất

### Keepalive Connections
Mặc định, mỗi HTTP request tạo một kết nối TCP mới rồi đóng lại — rất tốn kém. **Keepalive** cho phép tái sử dụng kết nối:

- `keepalive_timeout 300s` — giữ kết nối idle tối đa 300 giây
- `keepalive_requests 100000` — một kết nối có thể xử lý tối đa 100,000 request

### Keepalive đến Upstream
Mặc định NGINX dùng HTTP/1.0 với `Connection: Close` khi giao tiếp với backend — nghĩa là đóng kết nối sau mỗi request. Bằng cách nâng lên HTTP/1.1 và xóa header `Connection: Close`, NGINX có thể tái sử dụng kết nối đến backend, tăng hiệu suất đáng kể.

### SSL Session Caching và HTTP/2
SSL Handshake tốn thời gian. `ssl_session_cache shared:SSL:10m` lưu session SSL vào cache chung cho tất cả worker processes — 1MB có thể lưu khoảng 4,000 session. Khi client kết nối lại, họ có thể tái sử dụng session cũ, bỏ qua handshake.

HTTP/2 cho phép nhiều request chạy song song trên cùng một kết nối TCP, thay vì tuần tự như HTTP/1.1.

### Worker Processes
`worker_processes auto` tự động tạo số lượng worker process bằng với số CPU core — tận dụng tối đa phần cứng.

---

## 10. Health Checks và Monitoring

### Health Checks (NGINX Plus)
NGINX Plus có tính năng tự động kiểm tra sức khỏe của backend server mỗi 5 giây. Nếu server không trả về response 2xx hoặc 3xx, nó bị đánh dấu là failed và loại khỏi pool. Khi server hồi phục, `slow_start=30s` giúp tăng dần traffic trong 30 giây thay vì đổ ào vào ngay.

### Stub Status Module (Miễn phí)
`stub_status` cung cấp thống kê cơ bản của NGINX gồm số kết nối đang hoạt động, tổng số kết nối đã xử lý, và trạng thái Reading/Writing/Waiting. Quan trọng là phải giới hạn truy cập bằng `allow/deny` để không lộ thông tin nội bộ.

---

## 11. Logging

NGINX có hai file log chính:

- `/var/log/nginx/access.log` — ghi lại mọi request: IP client, thời gian, URL, status code, user agent
- `/var/log/nginx/error.log` — ghi lại các lỗi của NGINX

Log format có thể tùy chỉnh bằng directive `log_format`.

---

## 12. Tổng Kết

Qua toàn bộ bài học, tôi hiểu được rằng NGINX không chỉ là một web server đơn giản mà là một công cụ đa năng. Những best practice quan trọng gồm:

- Luôn dùng phiên bản **Mainline** cho môi trường production
- Đặt cấu hình từng site trong file riêng tại `/etc/nginx/conf.d/`
- Force tất cả traffic sang **HTTPS** để bảo mật và SEO
- Bật **Keepalive** để tái sử dụng kết nối, tăng hiệu suất
- Dùng **SSL session caching** và **HTTP/2** để cải thiện hiệu suất SSL
- Dùng **stub_status** kết hợp Prometheus + Grafana để monitor NGINX miễn phí
- Kiểm tra log thường xuyên để phát hiện và xử lý sự cố kịp thời
