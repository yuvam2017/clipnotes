# ClipNotes 🗒️

> Your thoughts, anywhere. A fast, minimal notes app with real-time sync across devices.

![ClipNotes](https://img.shields.io/badge/ClipNotes-v1.0-e8c547?style=for-the-badge&logoColor=black)
![Firebase](https://img.shields.io/badge/Firebase-Firestore-orange?style=for-the-badge&logo=firebase)
![HTML](https://img.shields.io/badge/Built_with-HTML%2FJS-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Live Demo → [yuvam2017.github.io/clipnotes](https://yuvam2017.github.io/clipnotes)**

---

## ✨ Features

- 🔐 **Authentication** — Login / Signup with Email & Password or Google
- 📝 **Simple Notes** — Freeform text notes for thoughts, ideas, anything
- ✅ **List Notes** — Checklist items with checkbox + strikethrough when done
- 💾 **Auto Save** — Notes save automatically to Firestore every 1.5 seconds
- 🔍 **Search** — Search across all your notes instantly
- 🗂️ **Filter** — Filter by All, Notes, or Lists
- 📤 **Share** — Share notes via WhatsApp, Gmail, Copy text, or Native share
- 🗑️ **Delete** — Delete notes with confirmation prompt
- 👤 **Multi-user** — Each user's notes are completely private and isolated
- 📱 **Responsive** — Works on mobile, tablet, and desktop

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, Vanilla JavaScript |
| Authentication | Firebase Auth (Email + Google OAuth) |
| Database | Cloud Firestore |
| Hosting | GitHub Pages |
| Fonts | Instrument Serif + Geist Mono (Google Fonts) |

---

## 🚀 Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/yuvam2017/clipnotes.git
cd clipnotes
```

### 2. Open locally
Just open `index.html` in your browser directly, or use VS Code Live Server:
```
Right click index.html → Open with Live Server
```
No build step. No npm install. No framework. Just open and run.

### 3. Deploy to GitHub Pages
```
GitHub → Your repo → Settings → Pages
Source → Deploy from branch → main → / (root)
Save → Live at https://yuvam2017.github.io/clipnotes
```

---

## 🔐 Security

ClipNotes is secured with multiple layers:

### Firestore Security Rules
Users can only read and write their own notes. No cross-user data access is possible.
```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null
                         && request.auth.uid == userId;
    }
  }
}
```

### API Key Restrictions
The Firebase API key is locked to specific authorized domains only:
```
localhost/*
yuvam2017.github.io/*
my-note-app-97cb2.firebaseapp.com/*
```

### Authorized Domains
Google Sign-In only works on whitelisted domains set in Firebase Console.

### What This Means
- ✅ Even if someone sees your `firebaseConfig` — they cannot read your notes
- ✅ Each user is completely isolated by their Firebase UID
- ✅ Unauthenticated requests are blocked at the database level

---

## 📁 Project Structure

```
clipnotes/
│
├── index.html        ← entire app (single file)
└── README.md         ← this file
```

The entire app lives in one `index.html` file — auth, dashboard, editor, modals, and Firebase logic all included.

---

## 🗄️ Firestore Data Structure

```
users/
  {uid}/
    notes/
      {noteId}/
        title      : string
        type       : "note" | "list"
        body       : string        (for simple notes)
        items      : array         (for list notes)
          - text    : string
          - checked : boolean
        createdAt  : timestamp
        updatedAt  : timestamp
```

---

## 📸 Screenshots

> Login screen with Google and Email auth

> Dashboard with note cards, search, and filter

> List note editor with checkboxes and strikethrough

> Share modal with WhatsApp, Gmail, and copy options

---

## 🔧 Firebase Setup (for your own deployment)

If you want to fork this and use your own Firebase project:

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Authentication** → Email/Password + Google
3. Create a **Firestore Database** (start in test mode, then apply rules above)
4. Register a **Web App** and copy the `firebaseConfig`
5. Replace the `firebaseConfig` object in `index.html`
6. Add your domain to **Authorized Domains** in Firebase Auth settings
7. Lock your **API Key** to your domain in Google Cloud Console
8. Deploy Firestore Security Rules from the Rules tab

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 👨‍💻 Author

Made by [Yuvam](https://github.com/yuvam2017)

---

<div align="center">
  <sub>Built with ☕ and Firebase</sub>
</div>
