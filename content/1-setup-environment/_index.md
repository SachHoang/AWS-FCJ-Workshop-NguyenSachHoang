+++
title = "Setting Up AWS Environment"
date = 2025-07-22
weight = 1
+++

## Part 1: Setting Up AWS Environment

### 1.1. Creating an AWS Account (if you don't have one)

**Step 1: Sign up for AWS**

1. Open your web browser and go to: https://aws.amazon.com
2. Click on "Create a free account" button
3. Fill in your personal information and credit card details (AWS requires a card for identity verification, but you won't be charged if you stay within free tier limits)
4. Complete the registration and verification process

**Step 2: Access AWS Management Console**

1. Go to https://aws.amazon.com
2. Click "Sign in to the Console"
3. Enter your login credentials

### 1.2. Creating an S3 Bucket for Website Hosting

**Step 1: Navigate to S3 Service**

1. In the AWS Management Console, type "S3" in the search bar at the top
2. Select "S3" from the search results
   ![ConnectPrivate](/images/1.introduce/1.1.png)

**Step 2: Create a New Bucket**

1. Click the orange "Create bucket" button
   ![ConnectPrivate](/images/1.introduce/1.2.png)
2. In the "General configuration" section:
   - Enter a unique bucket name (e.g., `youtube-thumbnail-creator-[your-name]`)
   - Note: Bucket names must be globally unique
3. In the "AWS Region" section:
   - Select a region close to your location (e.g., us-east-1 for US East)

**Step 3: Configure Public Access Settings**

1. Scroll down to "Block Public Access settings for this bucket"
2. Uncheck the box for "Block all public access"
3. Check the acknowledgment box that says "I acknowledge that the current settings might result in this bucket and the objects within becoming public"
   ![ConnectPrivate](/images/1.introduce/1.3.png)
4. Keep all other settings as default
5. Click "Create bucket" at the bottom of the page

### 1.3. Configuring S3 for Static Website Hosting

**Step 1: Open Bucket Properties**

1. From the list of buckets, click on the name of your newly created bucket
2. Select the "Properties" tab
   ![ConnectPrivate](/images/1.introduce/1.4.1.png)

**Step 2: Enable Static Website Hosting**

1. Scroll down to find the "Static website hosting" section
   ![ConnectPrivate](/images/1.introduce/1.4.2.png)
2. Click the "Edit" button
3. Select "Enable"
   ![ConnectPrivate](/images/1.introduce/1.4.3.png)
4. For "Index document", enter: index.html
5. Click "Save changes"

**Step 3: Note the Website URL**

1. After saving, scroll back to the "Static website hosting" section
2. You'll see a "Bucket website endpoint" - this is your website's URL
3. Make a note of this URL for later use
   ![ConnectPrivate](/images/1.introduce/1.4.4.png)

### 1.4. Setting Bucket Permissions

**Step 1: Configure Bucket Policy**

1. Select the "Permissions" tab
2. Scroll down to the "Bucket policy" section
3. Click "Edit"

**Step 2: Add the Policy**

1. In the policy editor, paste the following policy (replace [bucket-name] with your actual bucket name):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::[bucket-name]/*"
    }
  ]
}
```

2. For example, if your bucket name is "youtube-thumbnail-creator-john", the policy would be:

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

3. Click "Save changes"
