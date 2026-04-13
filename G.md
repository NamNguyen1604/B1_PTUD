G. Triển khai ứng dụng đến End-user
Trong Cloudflare: Tạo tunnel (đường hầm), chọn loại triển khai cho docker
Convert lệnh docker run ... sang dạng docker compose
Khai báo kết quả convert vào trong file docker-compose.yml
Chạy lại docker compose
Public ứng dụng bằng cách thêm 1 router trỏ tới container đang chạy trong docker, dữ liệu sẽ đi qua tunnel, url dạng sub-domain
Kiểm tra url sub-domain đã hoạt động public cho mọi end-user
Cấu trúc thư mục:
myapp/
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
├── myweb/
│   └── index.html
└── nodered/ (sẽ tự sinh dữ liệu)
│   └── (có nhiều file tự sinh)
│   └── settings.js (file này cần edit để bắt nodered login)

G. Câu hỏi về bài làm?
Tại sao phải dùng Nginx làm Reverse Proxy mà không trỏ thẳng Tunnel vào Node-RED?
- Để làm cổng tập trung điều hướng (Port 80) cho nhiều dịch vụ (Web, API, Node-RED) và tăng tính bảo mật.
Sự khác biệt giữa việc Mount file và Mount thư mục trong Docker là gì?
- Mount file vs Thư mục: Mount thư mục giúp đồng bộ toàn bộ dữ liệu (như code web); Mount file dùng để áp đặt cấu hình cố định (như nginx.conf).
Nếu thay đổi file index.html ở máy Ubuntu, nội dung trên web có thay đổi ngay không? Tại sao?
- Nội dung thay đổi ngay lập tức vì Docker Bind Mount liên kết trực tiếp file từ Ubuntu vào Container.
docker-compose.yml khai báo các services có phần restart: always hoặc restart: unless-stopped : chúng để làm gì?
- Đảm bảo dịch vụ tự khởi động lại khi server bị reboot hoặc container bị lỗi.
Cách khai báo để tất cả các services đều dùng chung 1 network? lợi ích của việc khai báo này là gì? Sửa đổi file docker-compose để tất cả các service đều dùng chung 1 network.
- Lợi ích dùng chung Network: Các container gọi nhau bằng tên (ví dụ http://myapi:9630) mà không cần mở port ra ngoài, tăng bảo mật tuyệt đối.
Tìm cách đưa Cloudflare Token vào trong file .env rồi sau đó thêm .env vào file .gitignore trước khi push code lên github. Tại sao nói đây là điều quan trọng về bảo mật mã nguồn?
- Để tránh lộ thông tin nhạy cảm khi đẩy code lên GitHub.
Tại sao chúng ta nên thêm hậu tố :ro khi mount file cấu hình Nginx?
- Là Read-only, ngăn container sửa đổi file cấu hình gốc trên máy Ubuntu.
Khi dùng Cloudflare Tunnel: có cần thiết phải mở cổng cho các service nữa không?
- Không cần, vì nó tạo kết nối Outbound an toàn từ trong máy ra Cloudflare.
