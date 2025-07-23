+++
title = "Cài đặt Website"
date = 2025-07-22
weight = 6
+++

## Phần 6: Cài đặt Website

### 6.1. Tải xuống mã nguồn

**Bước 1: Tạo thư mục dự án**

1. Tạo một thư mục mới trên máy tính của bạn (ví dụ: youtube-thumbnail-creator)
2. Trong thư mục đó, tạo thư mục con "website"

**Bước 2: Tạo các file HTML**

1. Tạo các file sau trong thư mục "website":
   - index.html
   - feedback.html
   - login.html
   - register.html
   - verify.html
   - forgot-password.html
2. Bạn có thể tải mã nguồn từ repository GitHub hoặc sử dụng mã nguồn được cung cấp trong hướng dẫn này.

### 6.2. Cập nhật thông tin cấu hình

**Bước 1: Cập nhật thông tin Cognito**

1. Mở file `login.html` trong trình soạn thảo văn bản
2. Tìm đoạn code chứa thông tin Cognito (thường nằm trong phần JavaScript)
3. Thay thế:
   - ClientId: Thay bằng App Client ID của bạn
   - UserPoolId: Thay bằng User Pool ID của bạn

**Bước 2: Cập nhật URL API Gateway**

1. Mở file `feedback.html` trong trình soạn thảo văn bản
2. Tìm đoạn code gọi API (thường là hàm fetch hoặc axios)
3. Thay thế URL API bằng URL của bạn (ví dụ: https://abc123def.execute-api.ap-southeast-1.amazonaws.com/prod/feedback)

**Bước 3: Cập nhật email đã xác thực**

1. Mở file `register.html` trong trình soạn thảo văn bản
2. Tìm đoạn code liên quan đến gửi email
3. Thay thế địa chỉ email mặc định bằng email đã xác thực của bạn

### 6.3. Upload files lên S3

**Bước 1: Truy cập bucket S3**

1. Quay lại AWS Console và mở dịch vụ S3
2. Chọn bucket bạn đã tạo

**Bước 2: Upload files**

1. Nhấn nút "Upload" hoặc "Tải lên"
2. Nhấn "Add files" hoặc "Thêm files"
3. Chọn tất cả các file HTML từ thư mục "website" của bạn
4. Nhấn "Upload" hoặc "Tải lên"
