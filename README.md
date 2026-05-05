# IELTS Progress Tracker

**An elegant, self-hosted web app to track your IELTS skill scores, visualise your progress, and stay motivated — built with React, TypeScript, Tailwind CSS, and Firebase.**

---

## 📖 Overview

IELTS Progress Tracker helps English learners **measure, monitor, and improve** their performance across the four core IELTS skills (Listening, Reading, Writing, Speaking) plus extra language dimensions like Grammar, Pronunciation, and Vocabulary.

The app was born from a simple workflow:

1. Study any authentic English content (article, podcast, video).
2. Submit your response to Claude/Gemini with a standardised prompt.
3. Receive AI-evaluated band scores.
4. Log those scores in the app and let it do the rest — analytics, trends, milestones, and insights.

---

## ✨ Current Features

- **Score Entry Panel** – Log date, topic, source URL, and scores (0–9, 0.5 increments) for all 7 skills.
- **Progress Dashboard**
  – Overall band average (last 30 sessions) with CEFR/IELTS level label.
  – Day streak counter.
  – Total sessions count.
  – Roadmap milestone (5 → 6 → 7 → 8+).
  – Individual skill cards with 7‑day trend arrows (↑ improving, ↓ declining, → stable).
- **Progress Charts**
  – Multi-line chart (7 skills, distinct colours) with zoom (7 / 30 / all days).
- **History Table**
  – All recorded sessions, sortable by date, with source links and AI feedback previews.
  – Delete individual entries.
- **Insights Panel**
  – Weakest/strongest IELTS skill identification.
  – Weekly activity summary.
- **Authentication**
  – Email/Password and Google Sign‑In via Firebase Auth.
  – Read‑only access for unauthenticated visitors (if you choose to enable public data).
  – Multi‑user support — each user’s data is securely isolated in Firestore.
- **Cloud Database**
  – Real‑time sync across devices with Firebase Firestore.
  – Automatic offline support using Firestore persistence.
- **Open Source**
  – Licensed under MIT. Free to use, modify, and deploy your own instance.

---

## 🚀 Roadmap (Upcoming Features)

1. **Target & Countdown**
   – Set personal target band and exam date; see remaining days and required weekly improvement rate.
2. **Predictive Insights**
   – Linear projection of when you’ll reach your target based on past trends.
3. **Prompt Copy Button**
   – One‑click copy of the AI evaluation prompt, pre‑filled with your topic.
4. **Advanced Charts**
   – Individual skill zoom, calendar heatmap (daily study activity).
5. **Export & Backup**
   – Download all sessions as CSV/JSON, save charts as PNG.
6. **Progressive Web App (PWA)**
   – Offline support, installable on mobile/home screen.
7. **UI Polish**
   – Dark mode, bottom navigation on mobile, gesture support.

---

## 🧱 Tech Stack

| Layer          | Technology                              |
| -------------- | --------------------------------------- |
| Frontend       | React 18+ with TypeScript               |
| Styling        | Tailwind CSS                            |
| Charts         | Chart.js (via react-chartjs-2)          |
| Database       | Firebase Firestore                      |
| Authentication | Firebase Auth (Email/Password + Google) |
| Hosting        | Vercel / Firebase Hosting               |
| Build Tool     | Vite                                    |

---

## 📁 Project Structure

```
ielts-tracker/
├── public/
│   ├── favicon.ico
│   └── manifest.json
├── src/
│   ├── assets/                 # Static assets (icons, images)
│   ├── components/             # Reusable React components
│   │   ├── Layout/
│   │   ├── Dashboard/
│   │   ├── AddEntry/
│   │   ├── History/
│   │   ├── Insights/
│   │   └── Auth/
│   ├── hooks/                  # Custom hooks (useAuth, useSessions)
│   ├── lib/                    # Firebase config & utility functions
│   │   ├── firebase.ts
│   │   └── db.ts
│   ├── types/                  # TypeScript type definitions
│   │   └── session.ts
│   ├── utils/                  # Helper functions (calculations, formatting)
│   ├── pages/                  # Page-level components (optional)
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css               # Tailwind directives & global styles
├── .env.example                # Environment variable template
├── .gitignore
├── index.html
├── package.json
├── postcss.config.js
├── tailwind.config.ts
├── tsconfig.json
├── vite.config.ts
└── README.md
```

---

## ⚙️ Setup & Customisation

### 1. Clone or download the repository

```bash
git clone https://github.com/your-username/ielts-tracker.git
cd ielts-tracker
```

### 2. Install dependencies

```bash
npm install
```

### 3. Firebase Configuration

To enable cloud sync and multi‑device support:

1. Create a Firebase project at [console.firebase.google.com](https://console.firebase.google.com).
2. Enable **Firestore Database**.
3. Enable **Authentication** with **Email/Password** and **Google** sign‑in methods.
4. Copy your Firebase config object.
5. Create a `.env` file in the project root (use `.env.example` as template):

```bash
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_AUTH_DOMAIN
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_STORAGE_BUCKET
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_MESSAGING_SENDER_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

6. Deploy Firestore security rules (`firestore.rules`):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    // Optional: allow public read of a shared collection
    match /public/{document=**} {
      allow read: if true;
      allow write: if false;
    }
  }
}
```

### 4. Run Locally

```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

### 5. Deploy to Vercel

1. Push your repository to GitHub.
2. Import the project in Vercel.
3. Add the same environment variables from `.env.example` in Vercel’s project settings.
4. Deploy — Vercel will automatically build and host the React app.

---

## 📝 Usage (End‑to‑End Flow)

1. **Study** – Pick any English article, podcast, or video.
2. **Get Scores** – Use the built‑in prompt (optional) to ask Claude/Gemini for IELTS band scores (0‑9) on:
   - Listening, Reading, Writing, Speaking (core)
   - Grammar, Pronunciation, Vocabulary (extra)
3. **Log Session** – Open the app, sign in (Email/Google), go to **+ Add Entry**, fill in the topic and scores, and **Save**.
4. **Track Progress** – Visit the **Dashboard** for trends, streaks, and milestone progress.
5. **Analyse** – The **Insights** tab highlights your weakest/strongest skills and recent activity.

---

## 🎯 Why This App?

- **Sign in with Google or Email** – Quick, secure access with no extra friction.
- **Open source & self-hostable** – Full control of your data. Deploy your own instance for free.
- **Multi‑device sync** – Firestore keeps your sessions in sync wherever you log in.
- **Privacy-first** – Your data is securely stored in your own Firebase project.
- **IELTS‑specific metrics** – Band scores, CEFR levels, and milestone roadmap aligned with real IELTS grading.
- **Lightweight & modern** – Built with React, TypeScript, and Tailwind for a smooth developer and user experience.

---

## 🤝 Contributing

This project is open source and welcomes contributions!  
Please open an issue first to discuss any major changes, then follow these steps:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature/your-feature`.
5. Open a Pull Request.

### Development Roadmap Tasks

- [ ] Add user‑defined target & countdown
- [ ] Implement predictive trend analysis
- [ ] PWA support (manifest + service worker)
- [ ] Export to CSV/JSON
- [ ] Dark mode toggle
- [ ] Calendar heatmap for daily study activity
- [ ] Internationalisation (i18n)

---

## 📄 License

This project is open‑source under the [MIT License](LICENSE).

---

_Made with ❤️ MotalebShabbir for IELTS aspirants who believe in consistent, measurable progress._
