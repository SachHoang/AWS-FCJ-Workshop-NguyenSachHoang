+++
title = "Dọn dẹp tài nguyên AWS"
date = 2025-07-22
weight = 10
+++

## Phần 10: Dọn dẹp tài nguyên AWS sau khi hoàn thành

Sau khi hoàn thành workshop hoặc không còn nhu cầu sử dụng, bạn nên xóa các tài nguyên AWS để tránh phát sinh chi phí không mong muốn.

### 10.1. Xóa S3 Bucket

1. Truy cập AWS Console, vào dịch vụ S3.
2. Chọn bucket bạn đã tạo cho website.
3. Nhấn "Delete" hoặc "Xóa".
4. Xác nhận tên bucket để hoàn tất xóa.

### 10.2. Xóa User Pool Cognito

1. Vào dịch vụ Cognito.
2. Chọn User Pool bạn đã tạo.
3. Nhấn "Delete" hoặc "Xóa".
4. Xác nhận để xóa User Pool.

### 10.3. Xóa Lambda Functions

1. Vào dịch vụ Lambda.
2. Chọn từng function bạn đã tạo (FeedbackHandler, EmailVerifier).
3. Nhấn "Delete" hoặc "Xóa".
4. Xác nhận để xóa function.

### 10.4. Xóa API Gateway

1. Vào dịch vụ API Gateway.
2. Chọn API bạn đã tạo (ThumbnailCreatorAPI).
3. Nhấn "Delete" hoặc "Xóa".
4. Xác nhận để xóa API.

### 10.5. Xóa các tài nguyên khác (nếu có)

- Nếu bạn tạo thêm DynamoDB, IAM Role, SES Identity... hãy xóa các tài nguyên này nếu không còn sử dụng.

> **Lưu ý:** Hãy kiểm tra kỹ trước khi xóa để tránh mất dữ liệu quan trọng.
