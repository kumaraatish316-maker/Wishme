# Wishme marketplace
Files: server.js, index.html, app.js, package.json (all 4 in the repo root).

Roles (everyone uses the same Log in button):
- Owner: logs in with ADMIN_PHONE / ADMIN_PASS. Only the owner sees Overview, People, Settings.
- Customer: creates own account, books, pays by UPI QR.
- Seller: applies from the app, owner approves, then adds products with price and photo.
- Delivery partner: applies with PAN, Aadhaar, bank details and photos, owner approves.

Render environment variables: ADMIN_PHONE, ADMIN_PASS, JWT_SECRET (long random, never change it later), NODE_VERSION=20.18.0
Optional: UPI_ID, UPI_NAME (or set them in the app: Settings tab).
Render: Build `npm install`, Start `npm start`. Add a Disk and DB_PATH=/data/wishme.db or data is lost on redeploy.

## WhatsApp updates (optional)
In-app notifications work with no setup. For automatic WhatsApp messages add these Render env vars
(needs a Meta WhatsApp Business Cloud API account):
- WA_TOKEN = permanent access token
- WA_PHONE_ID = WhatsApp phone number ID
- WA_TEMPLATE = (optional) approved template name with ONE body variable {{1}}; needed to message customers outside the 24-hour window
- WA_LANG = (optional) template language code, default en

## Cancel and refund
Customers can cancel until 1 day before the event date (not after delivery starts). For paid orders they give a UPI ID or bank account;
the owner sees it in Orders > Refunds, pays it from their UPI app, and taps "Refund sent".

## Online payment with Razorpay (optional, automatic)
Create a Razorpay account (razorpay.com, needs KYC), then in Render > Environment add:
- RZP_KEY_ID = your Key ID (start with Test keys: rzp_test_...)
- RZP_KEY_SECRET = your Key Secret
- RZP_WEBHOOK_SECRET = any long secret you choose; use the same one in Razorpay > Settings > Webhooks
In Razorpay, add a webhook URL: https://YOUR-SITE.onrender.com/api/rzp/webhook with events payment.captured and order.paid.
Also keep payment capture set to Automatic in Razorpay settings.
Once set, customers pay inside the app, orders confirm by themselves and cancellations refund to the original payment method.
Without these keys the app keeps working with the manual UPI QR flow.

## OTP login (optional)
Customers can log in with a 6-digit OTP. Add ONE of these in Render > Environment:
- FAST2SMS_KEY = API key from fast2sms.com (sends OTP by SMS)
- or the WhatsApp settings (WA_TOKEN + WA_PHONE_ID) to send OTP on WhatsApp
Without them the app keeps the password login. Owner, sellers and delivery partners always use their password.
Login stays active for 60 days on the same phone.
