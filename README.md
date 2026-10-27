# 3 Angle Events

Responsive website with a three-step event inquiry form and Google Sheets intake backend.

## Deployment

Connect this repository to Vercel, framework preset **Other**, root directory **/**. Vercel serves `index.html` and the `api/inquiry.js` function.

## Google Sheets backend setup

1. Open the dedicated spreadsheet: https://docs.google.com/spreadsheets/d/1k5NUjuRBciXJ-XgUFsSNcoD-hlmmyskBs8MGASda8Qk/edit
2. Go to **Extensions → Apps Script**. Replace default Code.gs with `google-apps-script/Code.gs` in this repository.
3. In **Project Settings → Script properties**, add `INQUIRY_SHARED_SECRET` with a long random secret. Keep it private.
4. Choose **Deploy → New deployment → Web app**, execute as **Me**, access **Anyone**. Authorize and deploy. This access level is needed for the server-to-server Vercel request; the shared secret limits writes. Do not use this endpoint for sensitive material beyond event inquiry details.
5. In Vercel project **Settings → Environment Variables**, add `GOOGLE_SCRIPT_WEB_APP_URL` (the web app `/exec` URL) and `INQUIRY_SHARED_SECRET` (the same secret). Use encrypted variables, set for Production and Preview if appropriate.
6. Redeploy the project and submit a test inquiry. Confirm that a row appears in the **Event Inquiries** tab. Change the status to follow up.

### Important

The inquiry form intentionally fails closed while the backend is not configured. It never promises a successful submission unless the Apps Script returns an affirmative result. Avoid publishing your secret or private script URLs to the GitHub repository. The spreadsheet holds personal contact details. Restrict sheet access to authorized staff.
