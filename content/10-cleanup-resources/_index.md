+++
title = "Cleaning Up AWS Resources"
date = 2025-07-22
weight = 10
+++

## Part 10: Cleaning Up AWS Resources After Completion

After finishing the workshop or if you no longer need the resources, you should delete your AWS resources to avoid unexpected charges.

### 10.1. Delete S3 Bucket

1. Go to the AWS Console and open the S3 service.
2. Select the bucket you created for the website.
3. Click "Delete".
4. Confirm the bucket name to complete deletion.

### 10.2. Delete Cognito User Pool

1. Go to the Cognito service.
2. Select the User Pool you created.
3. Click "Delete".
4. Confirm to delete the User Pool.

### 10.3. Delete Lambda Functions

1. Go to the Lambda service.
2. Select each function you created (FeedbackHandler, EmailVerifier).
3. Click "Delete".
4. Confirm to delete the function.

### 10.4. Delete API Gateway

1. Go to the API Gateway service.
2. Select the API you created (ThumbnailCreatorAPI).
3. Click "Delete".
4. Confirm to delete the API.

### 10.5. Delete Other Resources (if any)

- If you created additional resources such as DynamoDB, IAM Roles, SES Identities, etc., delete them if you no longer need them.

> **Note:** Double-check before deleting to avoid losing important data.
