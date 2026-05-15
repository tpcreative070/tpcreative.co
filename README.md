# TPCreative AI — Website

> Portfolio & landing page for **TPCreative AI**, a full-stack software studio.  
> Built with vanilla HTML/CSS/JS · Hosted on Firebase Hosting · Analytics via Firebase Analytics.

---

## Table of Contents

- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [First-Time Setup](#first-time-setup)
- [Deploy to Firebase](#deploy-to-firebase)
- [Preview Before Going Live](#preview-before-going-live)
- [Securing the Firebase API Key](#securing-the-firebase-api-key)
- [Firebase Analytics Events](#firebase-analytics-events)
- [Updating the Site](#updating-the-site)
- [Useful Commands](#useful-commands)

---

## Project Structure

```
tpcreative.co/
├── build.sh            # Deploy script (run this to ship)
├── firebase.json       # Firebase Hosting config
├── README.md           # This file
└── public/
    ├── index.html      # Main site (single-page)
    └── index_v1.html   # Previous version (backup)
```

---

## Prerequisites

Make sure the following are installed on your machine before deploying.

| Tool | Version | Install |
|---|---|---|
| Node.js | ≥ 18 | https://nodejs.org |
| npm | ≥ 9 | Comes with Node.js |
| Firebase CLI | latest | `npm install -g firebase-tools` |

Check your versions:

```bash
node -v
npm -v
firebase --version
```

---

## First-Time Setup

### 1. Clone / open the project

```bash
cd tpcreative.co
```

### 2. Make the deploy script executable

```bash
chmod +x build.sh
```

> You only need to do this once. After the first run, `build.sh` makes itself executable automatically.

### 3. Log in to Firebase

```bash
firebase login
```

A browser window will open. Sign in with the Google account that owns the `tpcreative-b06d7` project.

### 4. Verify the project is linked

```bash
firebase projects:list
```

You should see `tpcreative-b06d7` in the list.

---

## Deploy to Firebase

Run the deploy script from the project root:

```bash
./build.sh
```

The script will:

1. Check that Firebase CLI is installed (installs it if not)
2. Verify you are logged in
3. Confirm `public/index.html` and `firebase.json` exist
4. Deploy to Firebase Hosting

When finished, your site is live at:

```
https://tpcreative-b06d7.web.app
https://tpcreative-b06d7.firebaseapp.com
```

---

## Preview Before Going Live

Deploy to a **temporary preview URL** without touching the live site:

```bash
./build.sh --preview
```

- The preview link is active for **7 days**
- Share it with clients or teammates for review
- The live site is completely unaffected

Example preview URL:
```
https://tpcreative-b06d7--preview-20260515-225200-abc1def2.web.app
```

---

## Securing the Firebase API Key

The Firebase config in `index.html` is visible in the browser by design — this is normal for web apps. Real security comes from restricting how and where the key can be used.

### Step 1 — Restrict the API key to your domain

1. Go to [Google Cloud Console → Credentials](https://console.cloud.google.com/apis/credentials)
2. Click on your API key
3. Under **Application restrictions**, choose **HTTP referrers**
4. Add your allowed domains:

```
https://tpcreative-b06d7.web.app/*
https://tpcreative-b06d7.firebaseapp.com/*
https://tpcreative.co/*
```

### Step 2 — Lock Firebase Security Rules

In Firebase Console → **Firestore / Storage → Rules**, never leave the default open:

```js
// ❌ Never use in production
allow read, write: if true;

// ✅ Require authentication
allow read, write: if request.auth != null;
```

### Step 3 — Restrict authorized domains

Firebase Console → **Authentication → Settings → Authorized domains**  
Remove any domains you do not own.

---

## Firebase Analytics Events

The following events are tracked automatically:

| Event | Trigger |
|---|---|
| `page_view` | Page load |
| `cta_click` | Hero button clicks (Start a project, Our services) |
| `language_switch` | EN / VI toggle |
| `nav_click` | Navigation link click |
| `mobile_menu_open` | Hamburger menu opened |
| `service_card_engage` | Hovered a service card for > 0.8s |
| `contact_form_submit` | Contact form submitted |
| `scroll_depth` | Scrolled to 25 / 50 / 75 / 90% of page |
| `section_view` | A section scrolled into view |

View live data at:  
**Firebase Console → Analytics → Events**

---

## Updating the Site

1. Edit `public/index.html`
2. Test locally by opening the file in a browser:
   ```bash
   open public/index.html
   # or on Linux:
   xdg-open public/index.html
   ```
3. Deploy when ready:
   ```bash
   ./build.sh
   ```

---

## Useful Commands

```bash
# Deploy to live
./build.sh

# Deploy to a preview channel
./build.sh --preview

# Log in to Firebase
firebase login

# Log out
firebase logout

# List all your Firebase projects
firebase projects:list

# View active preview channels
firebase hosting:channel:list --project tpcreative-b06d7

# Delete a preview channel manually
firebase hosting:channel:delete CHANNEL_ID --project tpcreative-b06d7

# Open Firebase Hosting dashboard in browser
firebase open hosting:site --project tpcreative-b06d7
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | CSS3 (custom properties, grid, flexbox) |
| Scripting | Vanilla JavaScript (ES Modules) |
| Fonts | Google Fonts — Playfair Display, DM Sans, DM Mono |
| Analytics | Firebase Analytics 10.x |
| Hosting | Firebase Hosting |
| Deploy | Bash (`build.sh`) |

---

*© 2026 TPCreative AI. All rights reserved.*
