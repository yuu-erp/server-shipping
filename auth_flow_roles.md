# 🔐 Luồng Đăng ký / Đăng nhập - User, Shipper, Admin
> Ngày tạo: 2025-04-11

---

## 🔁 Luồng hoạt động xác thực người dùng (Authentication Flow)

mermaid
graph TD

A1[Người dùng: Chọn vai trò (User / Shipper / Admin)] --> A2[Người dùng: Điền thông tin đăng ký]
A2 --> A3[Hệ thống: Xác thực thông tin đầu vào]
A3 --> A4{{Vai trò là gì?}}

A4 -->|User| A5[Hệ thống: Lưu thông tin User vào DB]
A4 -->|Shipper| A6[Hệ thống: Yêu cầu thêm thông tin xác minh (giấy tờ, ảnh, bằng lái)]
A6 --> A7[Admin: Duyệt hồ sơ Shipper]
A7 --> A8[Hệ thống: Lưu thông tin Shipper vào DB]
A4 -->|Admin| A9[Hệ thống: Kiểm tra quyền tạo Admin hoặc do hệ thống cấp]

B1[Người dùng: Nhập email + mật khẩu] --> B2[Hệ thống: Kiểm tra thông tin]
B2 --> B3{{Thông tin hợp lệ?}}
B3 -->|Không| B4[Thông báo lỗi đăng nhập]
B3 -->|Có| B5[Hệ thống: Cấp JWT token hoặc phiên đăng nhập]
B5 --> B6[Chuyển hướng đến dashboard tương ứng theo vai trò]


## ✅ Vai trò và quyền truy cập (Role Permissions)

| Vai trò   | Mô tả | Quyền chính |
|-----------|------|--------------|
| **User** | Người dùng tạo và theo dõi đơn hàng | Tạo đơn, theo dõi, đánh giá |
| **Shipper** | Người giao hàng | Nhận đơn, cập nhật trạng thái |
| **Admin** | Quản trị viên hệ thống | Quản lý user/shipper/đơn hàng, xét duyệt hồ sơ |

---

## 🛠 Tính năng cần triển khai

- Đăng ký theo vai trò
- Xác minh hồ sơ Shipper
- Phân quyền khi đăng nhập
- Token (JWT hoặc session)
- Giao diện đăng nhập riêng cho từng loại vai trò (hoặc chung, phân loại sau)

---
