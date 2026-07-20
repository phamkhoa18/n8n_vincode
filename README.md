# n8n Vincode - Production & Local Setup

Dự án này cung cấp cấu hình Docker chuẩn để chạy [n8n](https://n8n.io/) (Nền tảng tự động hóa Workflow) ở cả môi trường Local và hoàn chỉnh cho **Production** (Có sẵn Nginx làm Reverse Proxy và tự động cấp phát SSL miễn phí từ Let's Encrypt).

## 🚀 Tính năng nổi bật
- **n8n** chạy ngầm ổn định qua Docker.
- **Tự động gia hạn SSL (HTTPS)** bằng Let's Encrypt Companion (Không cần cấu hình tay).
- **Nginx Reverse Proxy** tự động nhận diện traffic và forward về đúng port của n8n.
- Giữ nguyên Port mapping `7100` để có thể test độc lập nếu cần.

---

## 🌍 Hướng dẫn Deploy lên Production (VPS)

Cấu hình này đã được thiết kế sẵn sàng 100% để chạy thật ở domain: **n8n.vincode.xyz**

### 1. Yêu cầu hệ thống
- Server/VPS đã cài đặt [Docker](https://docs.docker.com/get-docker/) và Docker Compose.
- Đã trỏ tên miền (Record A) `n8n.vincode.xyz` về IP của Server VPS này.

### 2. Thiết lập môi trường
Clone mã nguồn về VPS và vào thư mục dự án:
```bash
git clone https://github.com/phamkhoa18/n8n_vincode.git
cd n8n_vincode
```

Copy file `.env.example` thành file `.env` (nếu chưa có):
```bash
cp .env.example .env
```
File `.env` mặc định đã được cấu hình chuẩn:
- `DOMAIN_NAME=vincode.xyz`
- `SUBDOMAIN=n8n`
- `SSL_EMAIL=admin@vincode.xyz` (Hãy sửa thành email thật của bạn nếu muốn).
- `N8N_PORT=7100`

### 3. Khởi động hệ thống
Mở terminal tại thư mục này và chạy lệnh sau:
```bash
docker compose up -d
```

### 4. Sử dụng
- Let's Encrypt sẽ mất khoảng 1-2 phút ở lần đầu tiên để verify và cấp phát SSL.
- Truy cập vào trình duyệt với đường dẫn an toàn:
👉 **[https://n8n.vincode.xyz](https://n8n.vincode.xyz)**

Lần đầu tiên truy cập, n8n sẽ yêu cầu bạn tạo tài khoản Admin.

---

## 🛠 Hướng dẫn chạy Local (Để Test)

Nếu bạn chỉ muốn chạy trên máy tính cá nhân để test (không có domain thật):
1. Đảm bảo Docker Desktop đang chạy.
2. Chạy lệnh: `docker compose up -d`
3. Lúc này SSL sẽ báo lỗi vì Let's Encrypt không verify được domain localhost, nhưng n8n vẫn sẽ chạy.
4. Bạn có thể truy cập qua: **[http://localhost:7100](http://localhost:7100)** 

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
