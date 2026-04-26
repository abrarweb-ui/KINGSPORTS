# 🏏 King Sports Kashmir – Setup Guide

## File Structure

```
kingsportskashmir/
├── index.html          ← Homepage
├── shop.html           ← Product listing
├── cart.html           ← Shopping cart
├── about.html          ← Brand story
├── contact.html        ← Contact page
├── admin.html          ← Admin dashboard
│
├── css/
│   ├── style.css       ← Main website styles
│   └── admin.css       ← Admin panel styles
│
└── js/
    ├── firebase-config.js   ← Firebase init (edit this!)
    ├── config.js            ← Store details
    ├── utils.js             ← Shared utilities
    ├── cart.js              ← Cart logic (localStorage)
    ├── auth.js              ← Admin auth helper
    ├── main.js              ← Homepage JS
    ├── shop.js              ← Shop page JS
    └── admin.js             ← Admin dashboard JS
```

---

## 🔥 Step 1: Firebase Setup

### 1. Create Firebase Project

1. Go to https://console.firebase.google.com/
2. Click "Add project"
3. Name it: `king-sports-kashmir`
4. Enable Google Analytics (optional)
5. Click "Create project"

---

### 2. Enable Firestore Database

1. In Firebase Console → **Firestore Database**
2. Click "Create database"
3. Choose **Start in test mode** (for development)
4. Select region: `asia-south1` (Mumbai – closest to Srinagar)
5. Click "Enable"

---

### 3. Enable Authentication

1. Firebase Console → **Authentication**
2. Click "Get started"
3. Go to **Sign-in method** tab
4. Enable **Email/Password**
5. Save

---

### 4. Create Admin User

1. Authentication → **Users** tab
2. Click "Add user"
3. Enter your admin email and password
4. Click "Add user"
5. **Important:** Note down these credentials – you'll use them to log into `admin.html`

---

### 5. Get Firebase Config

1. Firebase Console → **Project Settings** (gear icon)
2. Scroll down to "Your apps"
3. Click **"</>" (Web)** to add a web app
4. Register app name: `King Sports Kashmir Web`
5. Copy the `firebaseConfig` object

---

### 6. Update firebase-config.js

Open `js/firebase-config.js` and replace:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",            // ← Replace
  authDomain: "YOUR_PROJECT_ID.firebaseapp.com",  // ← Replace
  projectId: "YOUR_PROJECT_ID",     // ← Replace
  storageBucket: "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

With the actual values from your Firebase project.

---

## 🛡️ Step 2: Firestore Security Rules

In Firebase Console → Firestore → **Rules**, paste:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Products - public read, admin write only
    match /products/{productId} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

Click **Publish**.

---

## 🧪 Step 3: Add Your First Product

1. Open `admin.html` in your browser
2. Log in with the admin credentials you created
3. Click "➕ Add Product"
4. Fill in:
   - **Name:** Street King Pro
   - **Price:** 2999
   - **Category:** Kashmir Willow
   - **Stock:** 10
   - **Image URL:** (paste a Cloudinary or direct image URL)
   - **Description:** Premium Grade A Kashmir Willow cricket bat...
   - Check **Featured** to show it on the homepage
5. Click "Save Product"

The product will appear on the shop and homepage immediately.

---

## 🖼️ Getting Product Images

### Option A: Unsplash (Free, No account needed)
Use URLs like:
```
https://images.unsplash.com/photo-1540747913346-19e32dc3e97e?w=600&q=80
```

### Option B: Cloudinary (Recommended)
1. Create free account at https://cloudinary.com
2. Upload product photos
3. Copy the image URL
4. Paste into the Image URL field in admin

### Option C: Any direct image URL
Any publicly accessible image URL works.

---

## 🚀 Step 4: Deploy Your Website

### Option A: Netlify (Easiest – Free)

1. Go to https://netlify.com
2. Sign up / log in
3. Drag and drop your entire project folder onto the Netlify dashboard
4. Wait ~30 seconds
5. You get a live URL like: `https://king-sports-kashmir.netlify.app`
6. Optional: Set custom domain in Site Settings → Domain Management

### Option B: Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# In your project folder
firebase init hosting

# Select your project
# Public directory: . (current folder)
# Single page app: No
# Overwrite index.html: No

# Deploy
firebase deploy
```

Your site will be live at: `https://YOUR_PROJECT_ID.web.app`

### Option C: GitHub Pages

1. Create GitHub account
2. New repository → `kingsportskashmir`
3. Upload all files
4. Settings → Pages → Source: main branch
5. Live at: `https://yourusername.github.io/kingsportskashmir`

---

## 📱 PWA Setup (Optional)

To make the website installable as an app, create a `manifest.json`:

```json
{
  "name": "King Sports Kashmir",
  "short_name": "King Sports",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#0B1628",
  "theme_color": "#D4A847",
  "icons": [
    {
      "src": "icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    }
  ]
}
```

Add to `<head>` of all HTML files:
```html
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#D4A847">
```

---

## ✅ Checklist Before Going Live

- [ ] Firebase config updated in `js/firebase-config.js`
- [ ] Firestore security rules published
- [ ] Admin user created in Firebase Auth
- [ ] At least 3-5 products added with images
- [ ] Test Add to Cart → Cart page → WhatsApp checkout
- [ ] Test admin login/logout
- [ ] Test on mobile (responsive)
- [ ] Google Search Console: submit sitemap

---

## 💡 Quick Tips

- **WhatsApp Checkout** works without any payment gateway – customers confirm via chat
- **Stock = 0** automatically shows "Sold Out" badge
- **Stock = 1-3** shows "Only X Left" warning
- **Featured = true** shows product on homepage
- All cart data is in browser localStorage – no database needed for cart
- Admin panel is protected – only logged-in Firebase users can access

---

## 📞 Support

For any setup questions:
- **WhatsApp:** +91 70063 21949
- **Email:** kingsportsks844@gmail.com
- **Instagram:** @kingsports_ks
