+++
title = "Cài đặt AWS Lambda"
date = 2025-07-22
weight = 4
+++

## Phần 4: Cài đặt AWS Lambda (Xử lý logic phía máy chủ)

### 4.1. Tạo Lambda Function cho xử lý phản hồi

**Bước 1: Truy cập dịch vụ Lambda**

1. Trong ô tìm kiếm của AWS Console, gõ "Lambda" và chọn "Lambda"
2. Nhấn "Create function" hoặc "Tạo hàm"

**Bước 2: Cấu hình function**

1. Chọn "Author from scratch" hoặc "Tạo từ đầu"
2. Trong phần "Basic information":
   - Function name: Nhập `"FeedbackHandler"`
   - Runtime: Chọn "Node.js 16.x" từ danh sách
   - Architecture: Giữ mặc định "x86_64"
3. Mở rộng phần "Permissions" hoặc "Quyền":
   - Chọn "Create a new role with basic Lambda permissions"
4. Nhấn "Create function" hoặc "Tạo hàm"

**Bước 3: Thêm code**

1. Trong tab "Code", bạn sẽ thấy trình soạn thảo code
2. Xóa tất cả code hiện có
3. Dán code sau vào:

```javascript
const AWS = require("aws-sdk");
const ses = new AWS.SES({ region: "ap-southeast-1" }); // Thay đổi region nếu cần

exports.handler = async (event) => {
  try {
    // Parse request body
    const body = JSON.parse(event.body);
    const { message, userEmail } = body;

    if (!message || !userEmail) {
      return {
        statusCode: 400,
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ error: "Thiếu thông tin bắt buộc" }),
      };
    }

    // Gửi email xác nhận
    await sendConfirmationEmail(userEmail);

    // Lưu phản hồi (có thể mở rộng để lưu vào DynamoDB)
    console.log(`Phản hồi từ ${userEmail}: ${message}`);

    return {
      statusCode: 200,
      headers: {
        "Access-Control-Allow-Origin": "*",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ message: "Đã nhận phản hồi thành công" }),
    };
  } catch (error) {
    console.error("Lỗi:", error);
    return {
      statusCode: 500,
      headers: {
        "Access-Control-Allow-Origin": "*",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ error: "Lỗi máy chủ nội bộ" }),
    };
  }
};

async function sendConfirmationEmail(email) {
  const params = {
    Source: "your-verified-email@example.com", // Thay bằng email đã xác thực của bạn
    Destination: {
      ToAddresses: [email],
    },
    Message: {
      Subject: {
        Data: "Cảm ơn bạn đã gửi phản hồi - YouTube Thumbnail Creator",
      },
      Body: {
        Html: {
          Data: `...`,
        },
      },
    },
  };

  return ses.sendEmail(params).promise();
}
```

4. Thay thế `your-verified-email@example.com` bằng địa chỉ email bạn đã xác thực trong SES
5. Nhấn "Deploy" để lưu code

### 4.2. Tạo Lambda Function cho xác thực email

**Bước 1: Tạo function mới**

1. Quay lại trang chính của Lambda
2. Nhấn "Create function" hoặc "Tạo hàm"
3. Chọn "Author from scratch" hoặc "Tạo từ đầu"
4. Function name: Nhập "EmailVerifier"
5. Runtime: Chọn "Node.js 16.x"
6. Mở rộng phần "Permissions" và chọn "Create a new role with basic Lambda permissions"
7. Nhấn "Create function" hoặc "Tạo hàm"

**Bước 2: Thêm code**

1. Trong tab "Code", xóa tất cả code hiện có
2. Dán code sau vào:

```javascript
const AWS = require("aws-sdk");
const cognito = new AWS.CognitoIdentityServiceProvider();
const ses = new AWS.SES({ region: "ap-southeast-1" }); // Thay đổi region nếu cần

exports.handler = async (event) => {
  try {
    // Parse request body
    const body = JSON.parse(event.body);
    const { action, userEmail, password } = body;

    if (action === "send_otp") {
      // Tạo mã OTP
      const otpCode = generateOTP();

      // Gửi email OTP
      await sendOTPEmail(userEmail, otpCode);

      return {
        statusCode: 200,
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          message: "Đã gửi OTP thành công",
          otpCode: otpCode, // Trong môi trường thực tế, không nên trả về mã này
        }),
      };
    } else if (action === "signup_with_otp") {
      const { confirmationCode } = body;

      // Tạo người dùng trong Cognito
      await createCognitoUser(userEmail, password);

      return {
        statusCode: 200,
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ message: "Đã tạo người dùng thành công" }),
      };
    } else {
      return {
        statusCode: 400,
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ error: "Hành động không hợp lệ" }),
      };
    }
  } catch (error) {
    console.error("Lỗi:", error);
    return {
      statusCode: 500,
      headers: {
        "Access-Control-Allow-Origin": "*",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ error: error.message || "Lỗi máy chủ nội bộ" }),
    };
  }
};

function generateOTP() {
  return Math.floor(100000 + Math.random() * 900000).toString();
}

async function sendOTPEmail(email, otpCode) {
  const params = {
    Source: "your-verified-email@example.com", // Thay bằng email đã xác thực của bạn
    Destination: {
      ToAddresses: [email],
    },
    Message: {
      Subject: {
        Data: "Mã xác thực của bạn - YouTube Thumbnail Creator",
      },
      Body: {
        Html: {
          Data: `...`,
        },
      },
    },
  };

  return ses.sendEmail(params).promise();
}

async function createCognitoUser(email, password) {
  const params = {
    ClientId: "YOUR_COGNITO_APP_CLIENT_ID", // Thay bằng App Client ID của bạn
    Username: email,
    Password: password,
    UserAttributes: [
      {
        Name: "email",
        Value: email,
      },
      {
        Name: "email_verified",
        Value: "true",
      },
    ],
  };

  return cognito.signUp(params).promise();
}
```

3. Thay thế:
   - `your-verified-email@example.com` bằng địa chỉ email bạn đã xác thực trong SES
   - `YOUR_COGNITO_APP_CLIENT_ID` bằng App Client ID bạn đã ghi lại từ Cognito
4. Nhấn "Deploy" để lưu code

### 4.3. Cấu hình quyền cho Lambda

**Bước 1: Cấu hình quyền cho FeedbackHandler**

1. Mở Lambda function "FeedbackHandler"
2. Chọn tab "Configuration" hoặc "Cấu hình"
3. Chọn "Permissions" hoặc "Quyền" từ menu bên trái
4. Nhấn vào role name (tên vai trò) để mở IAM Console
5. Trong IAM Console, nhấn "Add permissions" > "Attach policies"
6. Tìm và chọn "AmazonSESFullAccess"
7. Nhấn "Add permissions" hoặc "Thêm quyền"

**Bước 2: Cấu hình quyền cho EmailVerifier**

1. Quay lại Lambda và mở function "EmailVerifier"
2. Chọn tab "Configuration" > "Permissions"
3. Nhấn vào role name để mở IAM Console
4. Nhấn "Add permissions" > "Attach policies"
5. Tìm và chọn cả hai policy:
   - AmazonSESFullAccess
   - AmazonCognitoPowerUser
6. Nhấn "Add permissions" hoặc "Thêm quyền"
