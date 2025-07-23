+++
title = "Setting Up AWS Lambda"
date = 2025-07-22
weight = 4
+++

## Part 4: Setting Up AWS Lambda (Server-side Logic)

### 4.1. Creating a Lambda Function for Feedback Handling

**Step 1: Access Lambda Service**

1. In the AWS Console search bar, type "Lambda" and select it
2. Click "Create function"

**Step 2: Configure the Function**

1. Select "Author from scratch"
2. In the "Basic information" section:
   - Function name: Enter `"FeedbackHandler"`
   - Runtime: Select "Node.js 16.x" from the dropdown
   - Architecture: Keep the default "x86_64"
3. Expand the "Permissions" section:
   - Select "Create a new role with basic Lambda permissions"
4. Click "Create function"

**Step 3: Add the Code**

1. In the "Code" tab, you'll see a code editor
2. Delete all existing code
3. Paste the following code:

```javascript
const AWS = require("aws-sdk");
const ses = new AWS.SES({ region: "us-east-1" }); // Change region if needed

exports.handler = async (event) => {
  try {
    // Parse request body
    const body = JSON.parse(event.body);
    const { message, userEmail } = body;

    if (!message || !userEmail) {
      return {
        statusCode: 400,
        body: JSON.stringify({ error: "Missing required information" }),
      };
    }

    // Send confirmation email
    await sendConfirmationEmail(userEmail);

    // Store feedback (could be expanded to save to DynamoDB)
    console.log(`Feedback from ${userEmail}: ${message}`);

    return {
      statusCode: 200,
      body: JSON.stringify({ message: "Feedback received successfully" }),
    };
  } catch (error) {
    console.error("Error:", error);
    return {
      statusCode: 500,
      body: JSON.stringify({ error: "Internal server error" }),
    };
  }
};

async function sendConfirmationEmail(email) {
  const params = {
    Source: "your-verified-email@example.com", // Replace with your verified email
    Destination: {
      ToAddresses: [email],
    },
    Message: {
      Subject: {
        Data: "Thank you for your feedback - YouTube Thumbnail Creator",
      },
      Body: { Html: { Data: `...` } },
    },
  };

  return ses.sendEmail(params).promise();
}
```

4. Replace `your-verified-email@example.com` with the email address you verified in SES
5. Replace `us-east-1` with your AWS region if different
6. Click "Deploy" to save the code

### 4.2. Creating a Lambda Function for Email Verification

**Step 1: Create a New Function**

1. Go back to the Lambda main page
2. Click "Create function"
3. Select "Author from scratch"
4. Function name: Enter "EmailVerifier"
5. Runtime: Select "Node.js 16.x"
6. Expand "Permissions" and select "Create a new role with basic Lambda permissions"
7. Click "Create function"

**Step 2: Add the Code**

1. In the "Code" tab, delete all existing code
2. Paste the following code:

```javascript
const AWS = require("aws-sdk");
const cognito = new AWS.CognitoIdentityServiceProvider();
const ses = new AWS.SES({ region: "us-east-1" }); // Change region if needed

exports.handler = async (event) => {
  try {
    // Parse request body
    const body = JSON.parse(event.body);
    const { action, userEmail, password } = body;

    if (action === "send_otp") {
      // Generate OTP
      const otpCode = generateOTP();
      await sendOTPEmail(userEmail, otpCode);
      return {
        statusCode: 200,
        body: JSON.stringify({ message: "OTP sent successfully", otpCode }),
      };
    } else if (action === "signup_with_otp") {
      const { confirmationCode } = body;
      await createCognitoUser(userEmail, password);
      return {
        statusCode: 200,
        body: JSON.stringify({ message: "User created successfully" }),
      };
    } else {
      return {
        statusCode: 400,
        body: JSON.stringify({ error: "Invalid action" }),
      };
    }
  } catch (error) {
    console.error("Error:", error);
    return {
      statusCode: 500,
      body: JSON.stringify({ error: error.message || "Internal server error" }),
    };
  }
};

function generateOTP() {
  return Math.floor(100000 + Math.random() * 900000).toString();
}

async function sendOTPEmail(email, otpCode) {
  const params = {
    Source: "your-verified-email@example.com", // Replace with your verified email
    Destination: { ToAddresses: [email] },
    Message: {
      Subject: { Data: "Your verification code - YouTube Thumbnail Creator" },
      Body: { Html: { Data: `...` } },
    },
  };
  return ses.sendEmail(params).promise();
}

async function createCognitoUser(email, password) {
  const params = {
    ClientId: "YOUR_COGNITO_APP_CLIENT_ID", // Replace with your App Client ID
    Username: email,
    Password: password,
    UserAttributes: [
      { Name: "email", Value: email },
      { Name: "email_verified", Value: "true" },
    ],
  };
  return cognito.signUp(params).promise();
}
```

3. Replace:
   - `your-verified-email@example.com` with your verified email address
   - `YOUR_COGNITO_APP_CLIENT_ID` with your App Client ID from Cognito
   - `us-east-1` with your AWS region if different
4. Click "Deploy" to save the code

### 4.3. Configuring Lambda Permissions

**Step 1: Configure Permissions for FeedbackHandler**

1. Open the "FeedbackHandler" Lambda function
2. Select the "Configuration" tab
3. Select "Permissions" from the left menu
4. Click on the role name to open the IAM Console
5. In the IAM Console, click "Add permissions" > "Attach policies"
6. Search for and select "AmazonSESFullAccess"
7. Click "Add permissions"

**Step 2: Configure Permissions for EmailVerifier**

1. Go back to Lambda and open the "EmailVerifier" function
2. Select "Configuration" > "Permissions"
3. Click on the role name to open the IAM Console
4. Click "Add permissions" > "Attach policies"
5. Search for and select both policies:
   - AmazonSESFullAccess
   - AmazonCognitoPowerUser
6. Click "Add permissions"
