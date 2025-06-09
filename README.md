
# Self-Hosted Odoo trên AWS EC2

## 📌 Thông tin hệ thống
- ✅ **Phiên bản Odoo:** Community 17.0 (miễn phí)
- ✅ **Server:** AWS EC2 (Ubuntu 22.04, t2.micro)
- ✅ **Docker:** Dùng để deploy `odoo-app`, `odoo-db`, `traefik` (reverse proxy + HTTPS)
- ✅ **Domain:** `https://odoo.odoominhai.xyz`

---

## 🔧 Các bước triển khai

### 1. Chuẩn bị môi trường EC2
- Mở port 22 (SSH), 80 (HTTP), 443 (HTTPS)
- Gán Elastic IP & domain

### 2. Cài Docker + Docker Compose
```bash
sudo apt update && sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER
```

### 3. Deploy Traefik với HTTPS
- File `~/traefik/docker-compose.yml`
- Reverse proxy port 80/443 -> Odoo
- Cấu hình TLS với Let's Encrypt và DNS: `websecure`

### 4. Deploy Odoo
- Thư mục `~/odoo-t2micro`
- File `docker-compose.yml` gồm:
  - `odoo-db` (PostgreSQL)
  - `odoo-app` (Odoo Community)
  - `traefik` label để routing

### 5. Gắn Docker network `web` giữa Traefik và Odoo

### 6. Kiểm tra kết nối HTTPS + giao diện tạo database

---

## 🔐 Bảo mật & Sao lưu
- [x] Đổi SSH sang IP cố định
- [x] HTTPS đầy đủ (Traefik + Let's Encrypt)
- [x] Backup định kỳ `odoo-db` và `odoo-web-data` lên Amazon S3
- [x] Có script `restore_odoo.sh` để khôi phục

---

## 📦 App cài được trong Odoo Community

| Nhóm chính     | Ứng dụng miễn phí |
|----------------|--------------------|
| CRM & Bán hàng | Sales, Invoicing   |
| Kho & Mua hàng | Inventory, Purchase|
| Dự án          | Project, Tasks     |
| Marketing      | Email Marketing    |
| Website        | Website, Blog      |

---

## ⚠️ Rủi ro và khuyến nghị

| Vấn đề          | Giải pháp                            |
|------------------|--------------------------------------|
| Bảo mật           | Dùng HTTPS + Authelia/Basic Auth     |
| Mất dữ liệu       | Thiết lập backup định kỳ lên S3      |
| Downtime server   | Cấu hình restart: always             |
| Không hỗ trợ Odoo| Cần tự support hoặc thuê kỹ thuật     |

---

## ✅ Link hệ thống
- Trang quản trị Odoo: https://odoo.odoominhai.xyz

## 🧠 Tác giả
- Quản trị viên: `MinhAI`
- Email: lequangminh.1373@gmail.com
- Ngày triển khai: 2025-06-09
