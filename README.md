# 🔥 AURA — Setup & Deploy Guide

## Step 1 — Firebase Project Banao

1. **firebase.google.com** pe jao → Sign in
2. **"Add Project"** click karo → Name: `aura-app`
3. Google Analytics → Skip karo
4. Project ban jaayega ✅

### Firestore Database Enable karo:
1. Left sidebar → **"Firestore Database"**
2. **"Create database"** click karo
3. **"Start in test mode"** select karo → Next → Done ✅

### Authentication Enable karo:
1. Left sidebar → **"Authentication"**
2. **"Get started"** click karo
3. **"Anonymous"** provider → Enable karo → Save ✅

### App Config Copy karo:
1. Project Settings (gear icon) → **"Your apps"**
2. **"</> Web"** icon click karo
3. App name: `aura-web` → Register
4. **firebaseConfig** ka saara data copy kar lo 📋

---

## Step 2 — Project Setup

```bash
# Project folder mein jao
cd aura-app

# .env.local file banao
cp .env.example .env.local

# .env.local file open karo aur Firebase config values paste karo
```

`.env.local` file aisi dikhni chahiye:
```
VITE_FIREBASE_API_KEY=AIzaSy...
VITE_FIREBASE_AUTH_DOMAIN=aura-app-123.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=aura-app-123
VITE_FIREBASE_STORAGE_BUCKET=aura-app-123.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789
VITE_FIREBASE_APP_ID=1:123456789:web:abc123
```

---

## Step 3 — Local Test karo

```bash
npm install
npm run dev
```

Browser mein `http://localhost:5173` khulega 🚀

---

## Step 4 — Vercel pe Deploy karo

### Option A — GitHub se (Recommended):

1. **github.com** pe new repo banao → `aura-app`
2. Code push karo:
```bash
git init
git add .
git commit -m "🔥 AURA app launch"
git remote add origin https://github.com/TUMHARA_USERNAME/aura-app.git
git push -u origin main
```
3. **vercel.com** pe jao → **"Import Project"**
4. GitHub repo select karo
5. ⚠️ **Environment Variables** section mein saari VITE_ variables add karo
6. **Deploy** click karo ✅

### Option B — Vercel CLI se:
```bash
npm install -g vercel
vercel
# Prompts follow karo
# Environment variables manually add karne padenge Vercel dashboard mein
```

---

## Data Kahan Store Hoga?

```
Firebase Firestore
└── users/
    └── {userId}/          ← Har user ka unique ID (anonymous)
        ├── xp: 120
        ├── streak: 7
        ├── habits: [...]
        ├── missions: [...]
        ├── createdAt: timestamp
        └── updatedAt: timestamp
```

- ✅ Real-time sync hota hai
- ✅ Page refresh ke baad bhi data rehta hai
- ✅ Ek hi device pe same user ka data save rahega
- ✅ Firebase free tier mein 50,000 reads/day milte hain

---

## File Structure

```
aura-app/
├── index.html
├── package.json
├── vite.config.js
├── .env.example        ← Template
├── .env.local          ← Tumhara actual config (git mein mat daalo!)
└── src/
    ├── main.jsx        ← Entry point
    ├── App.jsx         ← Main app + all screens
    ├── firebase.js     ← Firebase init + auth
    ├── useAuraData.js  ← Data hooks (Firestore)
    └── audioEngine.js  ← Web Audio sounds
```

---

## 🆘 Problems?

| Problem | Solution |
|---------|----------|
| Firebase error | `.env.local` mein values check karo |
| Data save nahi ho raha | Firestore test mode mein hai? Check karo |
| Build fail | `npm install` dobara run karo |
| Vercel deploy fail | Environment variables add kiye? |
