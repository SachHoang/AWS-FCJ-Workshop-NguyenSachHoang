+++
title = "Troubleshooting"
date = 2025-07-22
weight = 8
+++

## Part 8: Troubleshooting

### 8.1. CORS Issues

**Symptoms:**

- Error in browser console: "Access to fetch at '...' from origin '...' has been blocked by CORS policy"

**Solutions:**

1. Check your CORS configuration in API Gateway:
   - Go to API Gateway
   - Select your API
   - Select the "/feedback" resource
   - Click "Actions" > "Enable CORS"
   - Make sure "Access-Control-Allow-Origin" is set to "\*"
   - Click "Enable CORS and replace existing CORS headers"
2. After updating CORS, remember to redeploy the API:
   - Click "Actions" > "Deploy API"
   - Select the "prod" stage
   - Click "Deploy"

### 8.2. Login/Registration Issues

**Symptoms:**

- Unable to register or log in
- Error "User does not exist" or "Incorrect username or password"

**Solutions:**

1. Check your Cognito information:
   - Make sure User Pool ID and App Client ID are correctly updated in your code
   - Verify that the App Client is configured correctly (no client secret)
2. Check Lambda permissions:
   - Make sure the EmailVerifier Lambda function has AmazonCognitoPowerUser permission
3. Check logs:
   - Open the Lambda function
   - Select the "Monitor" tab > "Logs"
   - View logs to find specific errors

### 8.3. Email Sending Issues

**Symptoms:**

- Not receiving verification or feedback confirmation emails
- Error "Email address not verified" in Lambda logs

**Solutions:**

1. Check email verification status:
   - Go to SES Console
   - Select "Verified identities"
   - Make sure your email has "Verified" status
2. Check SES Sandbox:
   - If you're in the Sandbox, you can only send emails to verified addresses
   - Make sure the recipient email address is also verified
3. Check Lambda permissions:
   - Make sure Lambda functions have AmazonSESFullAccess permission
4. Check code:
   - Make sure you replaced `your-verified-email@example.com` with your verified email
