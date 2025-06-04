# action-repo

This repository is used solely to generate GitHub webhook events for:

- **push**  
- **pull_request** (opened & closed/merged)

Whenever you push to any branch, or open/close a pull request, GitHub will send a JSON payload to the webhook endpoint configured below.

---

## How to Configure the Webhook

1. **Go to this repository’s Settings → Webhooks → Add webhook**  
   - **Payload URL**: `https://<YOUR_NGROK_ID>.ngrok-free.app/webhook`  
     (replace `<YOUR_NGROK_ID>` with whatever ngrok tells you, e.g., `357f-202-8-113-246.ngrok-free.app`)  
   - **Content type**: `application/json`  
   - **Secret**: `YWM1NDA5Yjg1NzE2NTc4ZDVkNDNkNTQ2`  
     (this must match the `SECRET_TOKEN` in your Flask app’s `.env`)  
   - **Which events would you like to trigger this webhook?**  
     - Select **Let me select individual events.**  
       - Check **Push**  
       - Check **Pull requests**  
   - Click **Add webhook**.

2. **Verify**  
   After saving, GitHub will try to send a **test payload**. If your Flask server is running at the ngrok address, you’ll see a `200 OK` in the “Recent Deliveries” tab.

---

## Quick Test (after you set up webhook-repo)

1. Make a commit → `git push` → you should see an event arrive at your Flask endpoint.  
2. Create a Pull Request → you should see a “pull_request opened” event arrive.  
3. Merge the Pull Request → you should see a “pull_request closed (merged)” event arrive.

Whenever these happen, your Flask UI (in webhook-repo) will display a new line like:

- `"Travis" pushed to "staging" on 1st April 2021 - 09:30 PM UTC`  
- `"Travis" submitted a pull request from "staging" to "master" on 1st April 2021 - 09:00 AM UTC`  
- `"Travis" merged branch "dev" to "master" on 2nd April 2021 - 12:00 PM UTC`

---
