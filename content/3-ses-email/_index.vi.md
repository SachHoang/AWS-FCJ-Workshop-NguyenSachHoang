+++
title = "Cài đặt Amazon SES"
date = 2025-07-22
weight = 3
+++

## Phần 3: Cài đặt Amazon SES (Dịch vụ gửi email)

### 3.1. Xác thực email

**Bước 1: Truy cập dịch vụ SES**

1. Trong ô tìm kiếm của AWS Console, gõ "SES" và chọn "Simple Email Service"
2. Trong menu bên trái, chọn "Verified identities" hoặc "Danh tính đã xác minh"

**Bước 2: Tạo danh tính email**

1. Nhấn "Create identity" hoặc "Tạo danh tính"
2. Chọn "Email address" hoặc "Địa chỉ email"
3. Nhập địa chỉ email của bạn (bạn phải có quyền truy cập vào hộp thư này)
4. Nhấn "Create identity" hoặc "Tạo danh tính"

**Bước 3: Xác nhận email**

1. Kiểm tra hộp thư đến của địa chỉ email bạn vừa nhập
2. Tìm email từ Amazon SES với tiêu đề "Amazon SES Address Verification Request"
3. Mở email và nhấn vào liên kết xác nhận
4. Bạn sẽ thấy trang xác nhận thành công

### 3.2. Thoát khỏi SES Sandbox (tùy chọn)

Mặc định, SES hoạt động trong môi trường Sandbox, chỉ cho phép gửi email đến các địa chỉ đã xác thực. Nếu bạn muốn gửi email đến bất kỳ địa chỉ nào:

**Bước 1: Yêu cầu truy cập sản xuất**

1. Trong SES Console, chọn "Account dashboard" hoặc "Bảng điều khiển tài khoản"
2. Tìm phần "Sending statistics" hoặc "Thống kê gửi"
3. Nhấn "Request production access" hoặc "Yêu cầu truy cập sản xuất"

**Bước 2: Điền form yêu cầu**

1. Chọn khu vực bạn muốn thoát khỏi Sandbox
2. Điền thông tin về cách bạn sẽ sử dụng SES
3. Mô tả quy trình xử lý email bị trả lại và khiếu nại
4. Gửi yêu cầu

**Bước 3: Chờ phê duyệt**

1. AWS thường mất 24-48 giờ để xem xét yêu cầu
2. Bạn sẽ nhận được email thông báo khi yêu cầu được phê duyệt
