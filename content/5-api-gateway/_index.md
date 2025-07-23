+++
title = "Setting Up API Gateway"
date = 2025-07-22
weight = 5
+++

## Part 5: Setting Up API Gateway (Creating APIs for the Website)

### 5.1. Creating an API

**Step 1: Access API Gateway**

1. In the AWS Console search bar, type "API Gateway" and select the service
2. Click "Create API"

**Step 2: Choose API Type**

1. Select "REST API" (not "REST API Private" or "HTTP API")
2. Click "Build"

**Step 3: Configure the API**

1. Select "New API"
2. API name: Enter `"ThumbnailCreatorAPI"`
3. Keep other settings as default
4. Click "Create API"

### 5.2. Creating Resources and Methods

**Step 1: Create a Resource**

1. In your newly created API page, click "Actions"
2. Select "Create Resource"
3. Resource Name: Enter `"feedback"`
4. Keep other settings as default
5. Click "Create Resource"

**Step 2: Create a Method**

1. Select the "/feedback" resource you just created
2. Click "Actions" > "Create Method"
3. From the dropdown menu, select "POST"
4. Click the checkmark to confirm
5. In the "Setup" section:
   - Integration type: Select "Lambda Function"
   - Lambda Region: Select your Lambda region (e.g., us-east-1)
   - Lambda Function: Type "FeedbackHandler" and select it from the dropdown
6. Click "Save"
7. When the permission confirmation dialog appears, click "OK"

### 5.3. Configuring CORS

**Step 1: Enable CORS**

1. Select the "/feedback" resource
2. Click "Actions" > "Enable CORS"
3. For "Access-Control-Allow-Origin", enter "\*" (to allow all origins)
4. Keep other settings as default
5. Click "Enable CORS and replace existing CORS headers"
6. In the confirmation dialog, click "Yes, replace existing values"
