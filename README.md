# Fix El Paso 🗺️
**Community Infrastructure Map** — Report potholes, broken lights, flooding, and more.

---

## What's in this project

| File | What it does |
|------|-------------|
| `index.html` | The entire website — map, heat map, reporting form |

---

## Step 1 — Upload to GitHub

1. Open your `fix-el-paso` repository on GitHub
2. Click **Add file → Upload files**
3. Drag in `index.html`
4. Click **Commit changes**

Your site is now live at: `https://YOUR-USERNAME.github.io/fix-el-paso`

It will show sample data until you connect Firebase.

---

## Step 2 — Set up Firebase (free, takes ~10 minutes)

Firebase is Google's free database. It stores reports from community members and updates your map in real time.

### 2a. Create a Firebase project
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Add project** → name it `fix-el-paso` → Continue
3. Disable Google Analytics (not needed) → **Create project**

### 2b. Create a Firestore database
1. In the left sidebar, click **Firestore Database**
2. Click **Create database**
3. Choose **Start in test mode** (you can lock it down later)
4. Select `us-central` as location → **Done**

### 2c. Get your config keys
1. In Firebase Console, click the ⚙️ gear → **Project settings**
2. Scroll to **Your apps** → click the `</>` (web) icon
3. Register app with nickname `fix-el-paso-web` → **Register app**
4. You'll see a code block with your config. It looks like this:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "fix-el-paso.firebaseapp.com",
  projectId: "fix-el-paso",
  storageBucket: "fix-el-paso.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

### 2d. Paste config into index.html
1. Open `index.html` in a text editor (Notepad on Windows, TextEdit on Mac)
2. Find this section near the bottom:
```js
const FIREBASE_CONFIG = {
  apiKey:            "YOUR_API_KEY",
  ...
```
3. Replace each `"YOUR_..."` value with your actual values from Firebase
4. Save the file and re-upload it to GitHub

The yellow setup banner will disappear when Firebase is connected correctly.

---

## Step 3 — Test it

1. Open your live site
2. Click **Report Issue**
3. Pick a category, describe the issue, tap **Use my current location**
4. Click **Submit Report**
5. The pin should appear on the map instantly — and in your Firebase Console under Firestore → reports

---

## Securing your database (do this before sharing publicly)

In Firebase Console → Firestore → **Rules**, replace the rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reports/{report} {
      allow read: if true;           // Anyone can view the map
      allow create: if true;         // Anyone can submit a report
      allow update, delete: if false; // Nobody can edit/delete (only you via Console)
    }
  }
}
```

Click **Publish**.

---

## Issue categories

| Category | Color | Examples |
|----------|-------|---------|
| Pothole | 🔴 Red | Road damage, cracks |
| Streetlight | 🟡 Yellow | Out, flickering |
| Flooding | 🔵 Blue | Standing water, blocked drainage |
| Sidewalk | 🟣 Purple | Cracked, missing, inaccessible |
| Signage | 🟢 Green | Missing stop signs, faded markings |
| Other | ⚫ Gray | Everything else |

---

## Future ideas
- [ ] Photo uploads with reports
- [ ] "Upvote" button to confirm an issue others reported
- [ ] Admin panel to mark issues as resolved
- [ ] Email/SMS alerts when your reported issue is fixed
- [ ] Integration with City of El Paso 311 service

---

Built with [Leaflet.js](https://leafletjs.com), [OpenStreetMap](https://openstreetmap.org), and [Firebase](https://firebase.google.com).
