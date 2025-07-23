+++
title = "Xử lý sự cố"
date = 2025-07-22
weight = 8
+++

## Phần 8: Xử lý sự cố

### 8.1. Vấn đề CORS

**Triệu chứng:**

- Lỗi trong console trình duyệt: "Access to fetch at '...' from origin '...' has been blocked by CORS policy"

**Cách khắc phục:**

1. Kiểm tra lại cấu hình CORS trong API Gateway:
   - Truy cập API Gateway
   - Chọn API của bạn
   - Chọn resource "/feedback"
   - Nhấn "Actions" > "Enable CORS"
   - Đảm bảo "Access-Control-Allow-Origin" được đặt thành "\*"
   - Nhấn "Enable CORS and replace existing CORS headers"
2. Sau khi cập nhật CORS, nhớ triển khai lại API:
   - Nhấn "Actions" > "Deploy API"
   - Chọn stage "prod"
   - Nhấn "Deploy"

### 8.2. Lỗi đăng nhập/đăng ký

**Triệu chứng:**

- Không thể đăng ký hoặc đăng nhập
- Lỗi "User does not exist" hoặc "Incorrect username or password"

**Cách khắc phục:**

1. Kiểm tra thông tin Cognito:
   - Đảm bảo User Pool ID và App Client ID đã được cập nhật đúng trong code
   - Kiểm tra xem App Client có được cấu hình đúng không (không có client secret)
2. Kiểm tra quyền Lambda:
   - Đảm bảo Lambda function EmailVerifier có quyền AmazonCognitoPowerUser
3. Kiểm tra logs:
   - Mở Lambda function
   - Chọn tab "Monitor" > "Logs"
   - Xem logs để tìm lỗi cụ thể

### 8.3. Lỗi gửi email

**Triệu chứng:**

- Không nhận được email xác thực hoặc xác nhận phản hồi
- Lỗi "Email address not verified" trong logs Lambda

**Cách khắc phục:**

1. Kiểm tra trạng thái xác thực email:
   - Truy cập SES Console
   - Chọn "Verified identities"
   - Đảm bảo email của bạn có trạng thái "Verified"
2. Kiểm tra SES Sandbox:
   - Nếu bạn đang trong Sandbox, chỉ có thể gửi email đến địa chỉ đã xác thực
   - Đảm bảo địa chỉ email nhận cũng đã được xác thực
3. Kiểm tra quyền Lambda:
   - Đảm bảo Lambda functions có quyền AmazonSESFullAccess
4. Kiểm tra code:
   - Đảm bảo đã thay thế `your-verified-email@example.com` bằng email đã xác thực của bạn
