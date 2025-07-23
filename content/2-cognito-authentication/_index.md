+++
title = "Setting Up Amazon Cognito"
date = 2025-07-22
weight = 2
+++

## Part 2: Setting Up Amazon Cognito (User Authentication)

### 2.1. Creating a User Pool

**Step 1: Access Cognito Service**

1. In the AWS Console search bar, type "Cognito" and select it from the results
   ![ConnectPrivate](/images/1.introduce/2.png)
2. Click "Create user pool"

**Step 2: Configure Sign-in Experience**

1. In the "Configure sign-in experience" section:
   - Select "Email" as the sign-in option
   - Uncheck any other options
   - Click "Next"

**Step 3: Configure Security Requirements**

1. In the "Configure security requirements" section:
   - Keep the default password policy settings
   - Select "No MFA" (No Multi-Factor Authentication)
   - Check "Enable self-registration" to allow users to sign up
   - Click "Next"

**Step 4: Configure Sign-up Experience**

1. In the "Configure sign-up experience" section:
   - Select "Send email with Cognito"
   - Click "Next"

**Step 5: Configure App Integration**

1. In the "Configure app integration" section:
   - User pool name: Enter `"YouTubeThumbnailCreatorUsers"`
   - Check "Use the Cognito Hosted UI"
   - Domain name: Enter "youtube-thumbnail-creator-[your-name]"
   - In the "Initial app client" section:
     - App client name: Enter "WebClient"
     - Select "Public client"
     - Uncheck "Generate a client secret"
   - Click "Next"

**Step 6: Review and Create**

1. Review all settings
2. Click "Create user pool"

### 2.2. Saving User Pool Information

**Step 1: Get User Pool ID**

1. After creation, you'll see the User Pool details page
2. Note down the "User Pool ID" displayed at the top (e.g., us-east-1_AbCdEfGh)

**Step 2: Get App Client ID**

1. Select the "App integration" tab
2. Scroll down to the "App clients and analytics" section
3. Click on the "WebClient" app client name
4. Note down the "Client ID" (e.g., 1a2b3c4d5e6f7g8h9i0j)
