---
title : "Setup Messenger Bot"
date :  "2025-09-09" 
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## Setting Up the Messenger Chatbot

The MeetAssist chatbot is integrated with Facebook Messenger, allowing users to interact naturally to book, update, or cancel appointments.

### Step 1: Create a Facebook App

1. Go to [Facebook Developers](https://developers.facebook.com/)
2. Click **"My Apps"** → **"Create App"**
3. Fill in your app name (e.g., `MeetAssist`) and App Contact Email → Click **"Next"**
4. Select **"Messaging businesses"** as your use case → Click **"Next"**
5. Select your **"Business"** profile or choose none if you just want to test the app → Click **"Next"**
6. Click **"Go to Dashboard"**

### Step 2: Configure App Settings

1. In your app dashboard, click **"App Settings"** → **"Basic"**
2. Copy and save your **App ID** and **App Secret**
3. Paste the Privacy Policy URL: `https://www.freeprivacypolicy.com/live/e7193dae-4bba-4482-876e-7b76d83a0676`
4. Select **"Messenger for Business"** as the app category → Click **"Save Changes"**

### Step 3: Store Facebook Credentials in AWS

Run the following AWS CLI commands to securely store your Facebook credentials:

#### Create SSM Parameters:

```powershell
# Facebook App ID
aws ssm put-parameter `
    --name "/meetassist/facebook/app_id" `
    --value "YOUR_FACEBOOK_APP_ID" `
    --type "String" `
    --description "Facebook App ID for MeetAssist" `
    --region ap-northeast-1

# Facebook App Secret
aws ssm put-parameter `
    --name "/meetassist/facebook/app_secret" `
    --value "YOUR_FACEBOOK_APP_SECRET" `
    --type "String" `
    --description "Facebook App Secret for MeetAssist" `
    --region ap-northeast-1
```

#### Create Secrets Manager Secrets:

```powershell
# Facebook Page Access Token (get this from step 4 below)
aws secretsmanager create-secret `
    --name "meetassist/facebook/page_token" `
    --description "Facebook Page Access Token for MeetAssist" `
    --secret-string "YOUR_FACEBOOK_PAGE_ACCESS_TOKEN" `
    --region ap-northeast-1

# Facebook Verify Token (create a random string, e.g., "my_secure_token_12345")
aws secretsmanager create-secret `
    --name "/meetassist/facebook/verify_token" `
    --description "Facebook Webhook Verify Token for MeetAssist" `
    --secret-string "YOUR_CUSTOM_VERIFY_TOKEN_123456" `
    --region ap-northeast-1
```

{{% notice warning %}}
Replace `YOUR_FACEBOOK_APP_ID`, `YOUR_FACEBOOK_APP_SECRET`, `YOUR_FACEBOOK_PAGE_ACCESS_TOKEN`, and `YOUR_CUSTOM_VERIFY_TOKEN_123456` with your actual values.
{{% /notice %}}

### Step 4: Connect Facebook Page and Get Page Access Token

1. In your app dashboard, click **"Use Cases"** → **"Customize"**
2. Go to **"Messenger API Settings"**, under **"Generate Access Token"** click **"Connect"**
3. Link your Facebook Page to the app
4. Copy the **Page Access Token** that is generated
5. Use this token in the `aws secretsmanager create-secret` command above

### Step 5: Configure Webhooks API

1. Get your Webhook URL from the `outputs.json` file (generated after CDK deployment)
2. In your app dashboard, go to **"Messenger API Settings"**
3. Under **"Webhooks"** section, click **"Add Callback URL"**
4. Enter the following:
   - **Callback URL**: `https://<your-api-gateway-url>/webhook` (from `outputs.json`)
   - **Verify Token**: The same random string you used in step 3 (e.g., `YOUR_CUSTOM_VERIFY_TOKEN_123456`)
5. Click **"Verify and Save"**
6. Subscribe to the following webhook fields:
   - `messages`
   - `messaging_postbacks`
   - `messaging_account_linking`

### Step 6: Subscribe Page to Your App

1. In **"Messenger API Settings"**, scroll to **"Webhooks"** section
2. Click **"Add or Remove Pages"**
3. Select your Facebook Page and click **"Subscribe"**

### Step 7: Configure Messenger Profile (Get Started Button & Greeting)

After deployment, the chatbot automatically configures:
- **Get Started Button**: Users click this to begin conversation
- **Greeting Text**: Welcome message shown before user starts chatting

To manually update if needed:

```bash
# Set Get Started Button
curl -X POST "https://graph.facebook.com/v18.0/me/messenger_profile?access_token=<PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "get_started": {"payload": "GET_STARTED"}
  }'

# Set Greeting Text
curl -X POST "https://graph.facebook.com/v18.0/me/messenger_profile?access_token=<PAGE_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "greeting": [
      {
        "locale": "default",
        "text": "Xin chào! Mình là MeetAssist, trợ lý đặt lịch hẹn tư vấn hướng nghiệp. Hãy nhấn \"Bắt đầu\" để sử dụng dịch vụ! 👋"
      }
    ]
  }'
```

### Step 8: App Mode and Permissions

{{% notice info %}}
**Development Mode**: Your app is currently in development mode. Only you (the app developer) and testers you add can interact with the bot.

**Public Access**: To allow other users to use your bot, go to your app dashboard and switch the app to **"Live Mode"** under **"App Settings"** → **"Basic"**.

**App Review**: For full features and permissions, you must complete Facebook's App Review process. For testing purposes only, App Review is not required.
{{% /notice %}}

### Verification

Test your bot by:
1. Opening your Facebook Page in Messenger
2. Clicking the **"Get Started"** button
3. Verifying you receive the greeting message
4. Try sending a test message to confirm the webhook is working

If everything is configured correctly, the bot should respond to your messages!
