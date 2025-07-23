+++
title = "Setting Up the Website"
date = 2025-07-22
weight = 6
+++

## Part 6: Setting Up the Website

### 6.1. Downloading the Source Code

**Step 1: Create Project Directory**

1. Create a new folder on your computer (e.g., youtube-thumbnail-creator)
2. Inside that folder, create a subfolder named "website"

**Step 2: Create HTML Files**

1. Create the following files in the "website" folder:
   - index.html
   - feedback.html
   - login.html
   - register.html
   - verify.html
   - forgot-password.html
2. You can download the source code from the GitHub repository or use the code provided in this guide.

### 6.2. Updating Configuration Information

**Step 1: Update Cognito Information**

1. Open the `login.html` file in a text editor
2. Find the code section containing Cognito information (usually in the JavaScript section)
3. Replace:
   - ClientId: Replace with your App Client ID
   - UserPoolId: Replace with your User Pool ID

**Step 2: Update API Gateway URL**

1. Open the `feedback.html` file in a text editor
2. Find the code section that calls the API (usually a fetch or axios function)
3. Replace the API URL with your own (e.g., https://abc123def.execute-api.us-east-1.amazonaws.com/prod/feedback)

**Step 3: Update Verified Email**

1. Open the `register.html` file in a text editor
2. Find the code section related to sending emails
3. Replace the default email address with your verified email

### 6.3. Uploading Files to S3

**Step 1: Access S3 Bucket**

1. Go back to the AWS Console and open the S3 service
2. Select your bucket

**Step 2: Upload Files**

1. Click the "Upload" button
2. Click "Add files"
3. Select all HTML files from your "website" folder
4. Click "Upload"
