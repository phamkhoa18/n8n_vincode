# n8n Vincode - Setup với Nginx có sẵn trên Host

Dự án này cung cấp cấu hình Docker chạy **n8n** độc lập và hướng dẫn proxy qua Nginx đã cài đặt sẵn trên máy chủ của bạn (VPS).

Vì máy chủ của bạn đã có Nginx chạy ở port 80/443 phục vụ các web khác, chúng ta sẽ chỉ chạy n8n trên port `7100` (Localhost) và dùng Nginx của máy chủ để trỏ domain `n8n.vincode.xyz` về port `7100` này.

## 🚀 Hướng dẫn Deploy lên VPS

### 1. Khởi động n8n bằng Docker
Vào thư mục dự án trên VPS và chạy lệnh:
```bash
docker compose up -d
```
Lúc này n8n đã chạy ngầm và lắng nghe ở địa chỉ `127.0.0.1:7100`. Nó hoàn toàn không đụng chạm đến port 80/443 của bạn.

### 2. Cấu hình Nginx trên Host
Trong dự án đã có sẵn file mẫu `nginx.conf.example`. Bạn hãy copy nội dung file này và tạo một file cấu hình Nginx mới trên VPS của bạn:

1. Tạo file cấu hình:
   ```bash
   sudo nano /etc/nginx/sites-available/n8n.vincode.xyz
   ```
2. Dán nội dung từ file `nginx.conf.example` vào.
3. Kích hoạt file cấu hình:
   ```bash
   sudo ln -s /etc/nginx/sites-available/n8n.vincode.xyz /etc/nginx/sites-enabled/
   ```
4. Kiểm tra cấu hình và khởi động lại Nginx:
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

### 3. Cài đặt SSL tự động bằng Certbot (Let's Encrypt)
Vì Nginx nằm trên máy thật, bạn sẽ dùng `certbot` trực tiếp trên máy chủ để cài SSL cho n8n:
```bash
sudo certbot --nginx -d n8n.vincode.xyz -m phamkhoa3092003@gmail.com --agree-tos --redirect
```
Certbot sẽ tự động sửa file Nginx của bạn, thêm SSL và tự động chuyển hướng HTTP sang HTTPS.

Sau bước này, bạn có thể truy cập ngay vào: **[https://n8n.vincode.xyz](https://n8n.vincode.xyz)**

---

## ⚙️ Các lệnh quản lý Docker thường dùng

- **Xem log hệ thống n8n**:
  ```bash
  docker compose logs -f n8n
  ```
- **Dừng hệ thống**:
  ```bash
  docker compose down
  ```
- **Xóa toàn bộ data (CẢNH BÁO)**:
  ```bash
  docker compose down -v
  ```
