# 🎖️ Officers Mess Management System

A fully functional, free web app — powered by **Google Sheets as a database** and hosted on **GitHub Pages**.

---

## ✅ One-Time Setup Guide (~10 minutes)

Follow these steps in order. You only do this once.

---

### STEP 1 — Create a Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com)
2. Click **+ Blank** to create a new spreadsheet
3. Name it: `Officers Mess Database`
4. Leave it open — you'll need it in Step 2

---

### STEP 2 — Add the Apps Script Backend

1. In your Google Sheet, click the menu: **Extensions → Apps Script**
2. A new tab will open with a code editor
3. **Delete all existing code** in the editor
4. Open the file `Code.gs` from this repository
5. **Copy all the code** and paste it into the Apps Script editor
6. Click **💾 Save** (Ctrl+S)

---

### STEP 3 — Create the Admin Account

1. Still in the Apps Script editor, find the function dropdown at the top
2. Select **`setupInitialAdmin`** from the dropdown
3. Click **▶ Run**
4. A permissions popup will appear — click **Review permissions → Allow**
5. Check the **Execution log** at the bottom — it should say:
   > `Admin created. Login: admin@mess.mil / admin@1234`

---

### STEP 4 — Deploy as Web App

1. In the Apps Script editor, click **Deploy → New deployment**
2. Click the ⚙️ gear icon next to "Select type" → choose **Web app**
3. Fill in:
   - **Description:** `Mess Management API`
   - **Execute as:** `Me`
   - **Who has access:** `Anyone`
4. Click **Deploy**
5. **Copy the Web App URL** — it looks like:
   ```
   https://script.google.com/macros/s/AKfycb.../exec
   ```
   ⚠️ Keep this URL — you need it in the next step.

---

### STEP 5 — Connect the App to Your Sheet

1. Open `index.html` in any text editor (Notepad, VS Code, etc.)
2. Find this line near the top:
   ```javascript
   const API_URL = 'YOUR_APPS_SCRIPT_URL_HERE';
   ```
3. Replace `YOUR_APPS_SCRIPT_URL_HERE` with the URL you copied in Step 4:
   ```javascript
   const API_URL = 'https://script.google.com/macros/s/AKfycb.../exec';
   ```
4. Save the file

---

### STEP 6 — Deploy to GitHub Pages

1. Create a new repository on [github.com](https://github.com) — e.g., `mess-management`
2. Upload both files:
   - `index.html`
   - `README.md`
3. Go to **Settings → Pages**
4. Under **Source**, select: `main` branch, `/ (root)`
5. Click **Save**
6. Your app will be live in ~1 minute at:
   ```
   https://YOUR-USERNAME.github.io/mess-management/
   ```

---

## 🔐 Login Credentials

After setup, your initial admin login is:

| Field | Value |
|-------|-------|
| Email | `admin@mess.mil` |
| Password | `admin@1234` |

> **Change the admin email/password in your Google Sheet** (Members tab) after first login.

---

## 👤 How Members Join

1. Officer visits the app URL
2. Clicks **Register** tab
3. Fills in their details and submits
4. Admin sees the request under **Signup Requests** and clicks **Approve**
5. Member can then log in
6. New members get default password: `mess@1234` (they should change it)

---

## 💰 How Billing Works

```
Per Meal Rate = Total Monthly Expenditure ÷ Total Meals Served

Each Member's Bill:
  Gross = (Meals Attended × Per Meal Rate) + Custom Charges
  Balance = Advance Paid − Gross

  Positive Balance = Surplus (refund or carry forward)
  Negative Balance = Amount due from member
```

---

## 📁 File Structure

```
mess-management/
├── index.html     ← Complete app (edit API_URL before uploading)
├── Code.gs        ← Google Apps Script backend (paste into Apps Script)
└── README.md      ← This file
```

---

## ❓ Troubleshooting

| Problem | Solution |
|---------|----------|
| "Not configured" error | Make sure you replaced `YOUR_APPS_SCRIPT_URL_HERE` in index.html |
| Login says invalid credentials | Run `setupInitialAdmin` function again in Apps Script |
| API error on deploy | Make sure "Who has access" is set to **Anyone** |
| Data not saving | Re-deploy the Apps Script (Deploy → Manage deployments → Edit → New version) |
| CORS error in browser | This is normal for Apps Script — the app handles it automatically |

---

## 🔒 Security Notes

- This app uses a simple hash for passwords — suitable for internal mess use
- Do not expose the Google Sheet to public
- The Apps Script URL acts as your private API — do not share it publicly
- For a military-grade secure version, consider upgrading to Firebase Auth

---

*Built for Officers Mess internal management. Free to use and modify.*
