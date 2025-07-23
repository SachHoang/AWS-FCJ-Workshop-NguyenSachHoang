+++
title = "Cài đặt API Gateway"
date = 2025-07-22
weight = 5
+++

## Phần 5: Cài đặt API Gateway (Tạo API cho website)

### 5.1. Tạo API

**Bước 1: Truy cập API Gateway**

1. Trong ô tìm kiếm của AWS Console, gõ "API Gateway" và chọn dịch vụ
2. Nhấn "Create API" hoặc "Tạo API"

**Bước 2: Chọn loại API**

1. Chọn "REST API" (không phải "REST API Private" hoặc "HTTP API")
2. Nhấn "Build" hoặc "Xây dựng"

**Bước 3: Cấu hình API**

1. Chọn "New API" hoặc "API mới"
2. Nhập tên API: `"ThumbnailCreatorAPI"`
3. Giữ các cài đặt khác mặc định
4. Nhấn "Create API" hoặc "Tạo API"

### 5.2. Tạo Resource và Method

**Bước 1: Tạo Resource**

1. Trong trang API vừa tạo, nhấn "Actions" hoặc "Hành động"
2. Chọn "Create Resource" hoặc "Tạo tài nguyên"
3. Nhập "Resource Name": `feedback`
4. Giữ các cài đặt khác mặc định
5. Nhấn "Create Resource" hoặc "Tạo tài nguyên"

**Bước 2: Tạo Method**

1. Chọn resource "/feedback" vừa tạo
2. Nhấn "Actions" > "Create Method" hoặc "Tạo phương thức"
3. Từ dropdown menu, chọn "POST"
4. Nhấn dấu tích để xác nhận
5. Trong phần "Setup" hoặc "Thiết lập":
   - Integration type: Chọn "Lambda Function"
   - Lambda Function: Nhập `"FeedbackHandler"` và chọn từ danh sách
6. Nhấn "Save" hoặc "Lưu"
7. Khi hộp thoại xác nhận hiện lên, nhấn "OK"

### 5.3. Cấu hình CORS

**Bước 1: Bật CORS**

1. Chọn resource "/feedback"
2. Nhấn "Actions" > "Enable CORS" hoặc "Bật CORS"
3. Trong phần "Access-Control-Allow-Origin", nhập "\*" (cho phép tất cả các nguồn)
4. Giữ các cài đặt khác mặc định
5. Nhấn "Enable CORS and replace existing CORS headers" hoặc "Bật CORS và thay thế headers CORS hiện có"
6. Trong hộp thoại xác nhận, nhấn "Yes, replace existing values" hoặc "Có, thay thế giá trị hiện có"
