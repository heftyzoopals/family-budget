# Family Budget — Setup Guide

Follow these steps once and you'll have a shared budget app that both you and your wife can access from any device.

---

## Step 1 — Create a Firebase project (free)

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"**
3. Name it something like `family-budget`
4. Disable Google Analytics (not needed) → click **"Create project"**

---

## Step 2 — Create a Realtime Database

1. In the left sidebar, click **"Build" → "Realtime Database"**
2. Click **"Create Database"**
3. Choose the server location closest to you (e.g. `us-central1`)
4. When asked about rules, select **"Start in test mode"** → click **"Enable"**

> ⚠️ Test mode allows open read/write for 30 days. You'll secure it in Step 3.

---

## Step 3 — Set database security rules

1. In the Realtime Database page, click the **"Rules"** tab
2. Replace the contents with:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

3. Click **"Publish"**

> This keeps it open for just your family. Since the database URL isn't public, this is fine for personal use. If you want stricter security later, look into Firebase Authentication.

---

## Step 4 — Get your Firebase config

1. In the left sidebar, click the **gear icon ⚙️** → **"Project settings"**
2. Scroll down to **"Your apps"**
3. Click the **"</> Web"** icon to register a web app
4. Give it a name (e.g. `family-budget-web`) — no need to check "Firebase Hosting"
5. Click **"Register app"**
6. You'll see a config block that looks like this:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "family-budget-xxxxx.firebaseapp.com",
  databaseURL: "https://family-budget-xxxxx-default-rtdb.firebaseio.com",
  projectId: "family-budget-xxxxx",
  storageBucket: "family-budget-xxxxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

7. **Copy those 7 values** — you'll paste them into the app on first launch.

---

## Step 5 — Host on GitHub Pages

1. **Create a new GitHub repository** at https://github.com/new
   - Name it something like `family-budget`
   - Set it to **Public** (required for free GitHub Pages)
   - Click **"Create repository"**

2. **Upload your files.** The easiest way:
   - On your new repo page, click **"uploading an existing file"**
   - Drag and drop `index.html` and `SETUP.md`
   - Click **"Commit changes"**

3. **Enable GitHub Pages:**
   - Go to your repo → **Settings** → **Pages** (in the left sidebar)
   - Under "Source", select **"Deploy from a branch"**
   - Branch: **main**, Folder: **/ (root)**
   - Click **Save**

4. After about 1 minute, your app will be live at:
   ```
   https://YOUR-GITHUB-USERNAME.github.io/family-budget/
   ```

---

## Step 6 — Connect the app to Firebase

1. Open your GitHub Pages URL in a browser
2. You'll see the setup screen asking for your Firebase config
3. Paste each value from Step 4 into the matching fields
4. Click **"Connect and open budget →"**

The config is saved to your browser's local storage, so you only do this once per device.

**Share the GitHub Pages URL with your wife** and have her do Step 6 on her device too — she'll enter the same Firebase config values.

---

## Both of you are connected ✓

From now on:
- Any entry either of you adds appears for the other within seconds
- Recurring entries (rent, paychecks, subscriptions) auto-populate every month
- The balance at the top always reflects the current month

**Bookmark the URL** on both your phones for easy access.

---

## Updating the app later

If you want to change anything in the app, edit `index.html` on GitHub directly (click the file → pencil icon), commit the change, and it'll go live in about a minute.

---

## Troubleshooting

**"Permission denied" error in the browser console**
→ Check your database rules in Firebase (Step 3) and make sure `.read` and `.write` are both `true`.

**Data not syncing between devices**
→ Make sure both devices used the exact same `databaseURL` value when setting up.

**App shows setup screen again**
→ The Firebase config is stored per-browser. If you open a new browser or clear local storage, you'll need to re-enter the config. The data itself is safe in Firebase.

**Want to reset all data**
→ Go to Firebase Console → Realtime Database → click the three dots next to your database → "Delete all data". This is permanent.
