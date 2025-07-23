+++
title = "Setting Up Amazon SES"
date = 2025-07-22
weight = 3
+++

## Part 3: Setting Up Amazon SES (Email Service)

### 3.1. Verifying an Email Address

**Step 1: Access SES Service**

1. In the AWS Console search bar, type "SES" and select "Simple Email Service"
2. In the left menu, select "Verified identities"

**Step 2: Create Email Identity**

1. Click "Create identity"
2. Select "Email address"
3. Enter your email address (you must have access to this inbox)
4. Click "Create identity"

**Step 3: Verify the Email**

1. Check the inbox of the email address you entered
2. Look for an email from Amazon SES with the subject "Amazon SES Address Verification Request"
3. Open the email and click the verification link
4. You should see a success confirmation page

### 3.2. Exiting SES Sandbox (Optional)

By default, SES operates in a sandbox environment, allowing you to send emails only to verified addresses. To send emails to any address:

**Step 1: Request Production Access**

1. In the SES Console, select "Account dashboard"
2. Find the "Sending statistics" section
3. Click "Request production access"

**Step 2: Complete the Request Form**

1. Select the region you want to move out of the sandbox
2. Fill in information about how you'll use SES
3. Describe your process for handling bounces and complaints
4. Submit the request

**Step 3: Wait for Approval**

1. AWS typically takes 24-48 hours to review the request
2. You'll receive an email notification when your request is approved
