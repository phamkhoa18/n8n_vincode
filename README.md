# n8n Vincode - Local & Production Setup

Dự án này cung cấp cấu hình Docker chuẩn để chạy [n8n](https://n8n.io/) (Nền tảng tự động hóa Workflow) ở cả môi trường Local và dễ dàng public lên Internet.

## 🚀 Hướng dẫn chạy Local

### 1. Yêu cầu hệ thống
- Đã cài đặt [Docker](https://docs.docker.com/get-docker/) và Docker Compose (hoặc Docker Desktop).
- Đảm bảo Docker đang chạy trên máy của bạn.

### 2. Thiết lập môi trường
Dự án đã có sẵn file `.env.example`, nếu chưa có file `.env`, bạn hãy tạo bằng lệnh sau:
```bash
cp .env.example .env
```
File `.env` mặc định đã được cấu hình chạy ở cổng **7100**. Bạn có thể tuỳ chỉnh nếu muốn.

### 3. Khởi động n8n
Mở terminal tại thư mục này và chạy lệnh sau:
```bash
docker compose up -d
```

### 4. Sử dụng
Truy cập vào trình duyệt với đường dẫn:
👉 **[http://localhost:7100](http://localhost:7100)**

Lần đầu tiên truy cập, n8n sẽ yêu cầu bạn tạo tài khoản Admin.

---

## 🌍 Hướng dẫn Public lên Internet (Deploy lên VPS)

Cấu hình hiện tại đã được thiết kế sẵn sàng cho việc deploy lên Production.

1. **Chuẩn bị server/VPS**: Cài đặt Docker và Docker Compose trên Server.
2. **Clone source code**: Đưa toàn bộ thư mục này lên Server.
3. **Cấu hình Domain**:
   - Trỏ tên miền (ví dụ: `n8n.yourdomain.com`) về IP của Server.
   - Sửa file `.env` trên server:
     ```env
     DOMAIN_NAME=yourdomain.com
     SUBDOMAIN=n8n
     ```
   - *Lưu ý*: Trong môi trường thực tế, bạn nên sử dụng thêm một Reverse Proxy (như Nginx, Traefik, hoặc Caddy) để bọc cấu hình SSL (HTTPS) cho n8n.
4. **Khởi động**:
   ```bash
   docker compose up -d
   ```

## 🛠 Các lệnh quản lý Docker thường dùng

- **Xem log hệ thống n8n**:
  ```bash
  docker compose logs -f
  ```
- **Dừng n8n**:
  ```bash
  docker compose down
  ```
- **Khởi động lại n8n**:
  ```bash
  docker compose restart
  ```
- **Xóa toàn bộ data (CẢNH BÁO)**:
  ```bash
  docker compose down -v
  ```
