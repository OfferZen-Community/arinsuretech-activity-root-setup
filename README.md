## Build an augmented reality app on Root Insurance

# Activity: Getting set up with Root Insurance

## Intro

*This activity should take you about* **30 minutes to complete**, *and afterwards you'll be ready with everything you need to easily generate insurance quotes, policy holders and policies, and process claims.*

In this activity you'll be setting up your Root Insurance account, creating an organization, enabling insurance modules, generating an API key and setting up a webhook. When you complete this activity, MakeBot will reward you with cred by posting in your team channel about your great success.

If you'd like some assistance at any point, chat to your team in the team channel on Make Slack and mention @dan. You can also chat to Root support on Make Slack at #root.

## Useful resources
- [Root Insurance guides](https://app.root.co.za/docs/insurance/guides)
- [Root Insurance API documentation](https://app.root.co.za/docs/insurance/api)

## Process

### Step 0: Set up your root account

- You will receive an invitation email from Root to get started. Follow the invitation link and create your account.
- If you haven't received an invitation yet, contact @dan on Make Slack.

### Step 1: Create an organization
- Navigate to your [Root Insurance organization dashboard](https://app.root.co.za/organizations)
- Click "Create an Organization"
- Choose any name you like. You can leave the other fields blank for now.
- Click "Create"

### Step 2: Activate modules
- Open "Settings" from the sidebar
- Choose "Insurance modules"
- Enable all modules, "Gadgets", "Funeral", "Term", "Personal Accident", "Group Personal Accident"

You now have access to all of Root's insurance modules.

### Step 3: Create an API key
- From the settings menu, choose "API keys"
- Click "Create API key"
- Choose whatever you like for the description
- Tick the "select all" checkbox to enable all permissions
- Click "Create API key"
- Copy your API key and save it somewhere - you'll need it later!
- Click "close"

Now that your account has all the required modules, and your API key is activated, you're ready to set up a webhook!

### Step 4: Create a webhook to Make

- For context, check out the [Root webhook docs](https://app.root.co.za/docs/insurance/api#webhooks) for details on what webhooks are and how they work. If you like, you can use the JSON API and the language of your choice to interact with the webhook endpoint. For simplicity, you can also use `curl` in the terminal. 
- Follow the instructions in [Root API docs: Creating a webhook](https://app.root.co.za/docs/insurance/api#create-webhook) to create a webhook to Make. Remember to update the `-u` parameter to reflect your API key, and use the following payload:
```
curl https://api.root.co.za/v1/insurance/webhooks \
  --request POST
  -u test_key_tYILz1640w9q5n5kNQUZ: \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Make Day",
    "description": "Whatever you like",
    "verification_token": "YOUR_EMAIL_ADDRESS",
    "url": "https://make.offerzen.com/api/root/webhooks/blah",
    "subscriptions": [
      "application_created",
      "claim_opened",
      "complaint_opened",
      "policy_issued",
      "quote_created"
    ],
  }'
```
- You'll receive a response with fields `webhook_id` and `secret` - save this data for later.

### Step 5: Test your webhook
- Follow the instructions in [Root API docs: Pinging a webhook](https://app.root.co.za/docs/insurance/api#ping-webhook) to complete this activity. Replace your webhook ID and API keys in the request:
```
curl https://api.root.co.za/v1/insurance/webhooks/WEBHOOK_ID/ping \
  -u test_key_tYILz1640w9q5n5kNQUZ:
 ```
- You'll receive (some kind of response??)

- Check your team slack channel and bask in the glory of your great success! 🌈


