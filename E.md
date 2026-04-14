E. Triển khai (level test) ứng dụng
Chuyển vào trong thư mục ~/myapp
Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
<img width="944" height="224" alt="image" src="https://github.com/user-attachments/assets/43fb3e40-674a-4a1c-8da4-bc1202a1ce3b" />

Lợi ích: Chỉ cần docker-compose up -d là toàn bộ hệ thống (Web + Node-RED + Tunnel) tự chạy,

Kiểm tra các container đang chạy trong docker, nếu có cái nào bị restart cần tìm lỗi rồi edit lại docker-compose.yml
Kiểm tra kiểm thử các service đang chạy độc lập thông qua ip và port của nó: ví dụ mở trình duyệt ip_ubuntu:1880 để check nodered đã chạy chưa
<img width="952" height="1013" alt="image" src="https://github.com/user-attachments/assets/22f73840-def4-4722-b6bc-adb8821675b5" />
<img width="1920" height="1018" alt="image" src="https://github.com/user-attachments/assets/1262c3fd-8bfb-4e13-ae2d-d85707c732f9" />

Sử dụng nodered: kéo nodered http_in , http_response, function : để tạo api get đơn giản (dùng cho /api proxy_pass của nginx)
<img width="946" height="1015" alt="image" src="https://github.com/user-attachments/assets/b8389f51-c14c-4f81-b21d-cb70070f6b73" />

Sửa file ./myweb/index.html : thêm code html+js để sử dụng được api đã khai báo proxy_pass (thực ra là sử dụng nodered http_in hoặc sử dụng service myapi)

<img width="967" height="1013" alt="image" src="https://github.com/user-attachments/assets/151c53c1-f338-48ad-bc2f-1f94ba1da0b0" />
