+++
title = "Cài đặt Amazon Cognito"
date = 2025-07-22
weight = 2
+++

## Phần 2: Cài đặt Amazon Cognito (Hệ thống xác thực người dùng)

### 2.1. Tạo User Pool

**Bước 1: Truy cập dịch vụ Cognito**

1. Trong ô tìm kiếm của AWS Console, gõ "Cognito" và chọn "Cognito" từ kết quả
   ![ConnectPrivate](/images/1.introduce/2.png)
2. Nhấn "Create user pool" hoặc "Tạo nhóm người dùng"
   ![ConnectPrivate](/images/1.introduce/2.1.png)

**Bước 2: Cấu hình đăng nhập**

1. Trong phần "Configure sign-in experience":
   - Chọn "Email" làm phương thức đăng nhập
   - Bỏ chọn các tùy chọn khác
   - Nhấn "Next" hoặc "Tiếp theo"

**Bước 3: Cấu hình yêu cầu bảo mật**

1. Trong phần "Configure security requirements":
   - Để mặc định cài đặt mật khẩu
   - Chọn "No MFA" (Không xác thực đa yếu tố)
   - Chọn "Enable self-registration" (Cho phép người dùng tự đăng ký)
   - Nhấn "Next" hoặc "Tiếp theo"

**Bước 4: Cấu hình gửi email**

1. Trong phần "Configure sign-up experience":
   - Chọn "Send email with Cognito" (Gửi email bằng Cognito)
   - Nhấn "Next" hoặc "Tiếp theo"

**Bước 5: Cấu hình ứng dụng**

1. Trong phần "Configure app integration":
   - Đặt tên User Pool: `"YouTubeThumbnailCreatorUsers"`
   - Chọn "Use the Cognito Hosted UI" (Sử dụng giao diện của Cognito)
   - Đặt tên domain: youtube-thumbnail-creator-[tên-của-bạn]
   - Trong phần "Initial app client":
     - Tên: "WebClient"
     - Chọn "Public client" (Ứng dụng công khai)
     - Bỏ chọn "Generate a client secret" (Không tạo client secret)
   - Nhấn "Next" hoặc "Tiếp theo"

**Bước 6: Xem lại và tạo**

1. Xem lại tất cả cài đặt
2. Nhấn "Create user pool" hoặc "Tạo nhóm người dùng"

### 2.2. Lưu thông tin User Pool

**Bước 1: Lấy User Pool ID**

1. Sau khi tạo xong, bạn sẽ thấy trang chi tiết User Pool
2. Ghi lại "User Pool ID" hiển thị ở trên cùng (ví dụ: ap-southeast-1_AbCdEfGh)

**Bước 2: Lấy App Client ID**

1. Chọn tab "App integration" hoặc "Tích hợp ứng dụng"
2. Kéo xuống phần "App clients and analytics"
3. Nhấn vào tên app client "WebClient"
4. Ghi lại "Client ID" (ví dụ: 1a2b3c4d5e6f7g8h9i0j)
