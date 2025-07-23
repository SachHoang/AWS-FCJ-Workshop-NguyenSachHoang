+++
title = "Chuẩn bị môi trường"
date = 2025-07-22
weight = 1
+++

## Phần 1: Chuẩn bị môi trường

### 1.1. Tạo tài khoản AWS (nếu chưa có)

1. Mở trình duyệt web và truy cập: https://aws.amazon.com
2. Nhấn vào nút "Tạo tài khoản AWS miễn phí" hoặc "Create a free account"
3. Điền thông tin cá nhân và thẻ tín dụng (AWS yêu cầu thẻ để xác minh danh tính, nhưng bạn sẽ không bị tính phí nếu chỉ sử dụng dịch vụ miễn phí)
4. Hoàn thành quá trình đăng ký và xác minh

### 1.2. Tạo bucket S3 cho website

**Bước 1: Đăng nhập vào AWS**

1. Truy cập https://aws.amazon.com
2. Nhấn "Sign in to the Console" hoặc "Đăng nhập vào Console"
3. Nhập thông tin đăng nhập của bạn

**Bước 2: Tìm dịch vụ S3**

1. Sau khi đăng nhập, bạn sẽ thấy trang AWS Management Console
2. Trong ô tìm kiếm ở trên cùng, gõ "S3" và chọn "S3" từ kết quả tìm kiếm
   ![ConnectPrivate](/images/1.introduce/1.1.png)

**Bước 3: Tạo bucket mới**

1. Trong trang S3, nhấn nút "Create bucket" hoặc "Tạo bucket" màu cam
   ![ConnectPrivate](/images/1.introduce/1.2.png)
2. Trong phần "General configuration":
   - Nhập tên bucket (ví dụ: `youtube-thumbnail-creator-[tên-của-bạn]`)
   - Lưu ý: Tên bucket phải là duy nhất trên toàn cầu
3. Trong phần "AWS Region":
   - Chọn khu vực gần vị trí của bạn (ví dụ: ap-southeast-1 cho Singapore)

**Bước 4: Cấu hình quyền truy cập**

1. Kéo xuống phần "Block Public Access settings for this bucket"
2. Bỏ chọn ô "Block all public access"
3. Đánh dấu vào ô xác nhận "I acknowledge that the current settings might result in this bucket and the objects within becoming public"
   ![ConnectPrivate](/images/1.introduce/1.3.png)
4. Giữ các cài đặt khác mặc định
5. Nhấn nút "Create bucket" ở cuối trang

### 1.3. Cấu hình bucket S3 làm website tĩnh

**Bước 1: Mở cài đặt bucket**

1. Trong danh sách bucket, nhấn vào tên bucket bạn vừa tạo
2. Chọn tab "Properties" hoặc "Thuộc tính"
   ![ConnectPrivate](/images/1.introduce/1.4.1.png)

**Bước 2: Bật tính năng website tĩnh**

1. Kéo xuống tìm phần "Static website hosting" hoặc "Lưu trữ trang web tĩnh"
   ![ConnectPrivate](/images/1.introduce/1.4.2.png)
2. Nhấn nút "Edit" hoặc "Chỉnh sửa"
3. Chọn "Enable" hoặc "Bật"
   ![ConnectPrivate](/images/1.introduce/1.4.3.png)
4. Trong phần "Index document", nhập: index.html
5. Nhấn "Save changes" hoặc "Lưu thay đổi"

**Bước 3: Ghi lại URL website**

1. Sau khi lưu, kéo xuống lại phần "Static website hosting"
2. Bạn sẽ thấy "Bucket website endpoint" - đây là URL của website
3. Ghi lại URL này để sử dụng sau
   ![ConnectPrivate](/images/1.introduce/1.4.4.png)

### 1.4. Cấu hình quyền truy cập cho bucket

**Bước 1: Mở cài đặt quyền**

1. Chọn tab "Permissions" hoặc "Quyền"
2. Kéo xuống phần "Bucket policy" hoặc "Chính sách bucket"
3. Nhấn "Edit" hoặc "Chỉnh sửa"

**Bước 2: Thêm chính sách**

1. Trong hộp soạn thảo, dán chính sách sau (thay thế [tên-bucket] bằng tên bucket của bạn):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::[tên-bucket]/*"
    }
  ]
}
```

2. Ví dụ, nếu tên bucket của bạn là "youtube-thumbnail-creator-john", chính sách sẽ là:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::youtube-thumbnail-creator-john/*"
    }
  ]
}
```

3. Nhấn "Save changes" hoặc "Lưu thay đổi"
