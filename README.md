# Study Plan Optimizer

Single-page study planner with Firebase Auth + Firestore persistence, task analytics, and smart scheduling.

## Features
- Email/password auth with Remember Me and password reset
- Firestore persistence per user (tasks + daily limit)
- Auto-balance and auto-reschedule algorithms
- Validation with regex and XSS protection
- Status tracking, analytics, and accessible UI

## Project Structure
- `index.html` - App views and markup
- `styles.css` - UI styles and animations
- `app.js` - All logic and modules
- `firebase.json` - Firebase Hosting + Firestore rules config
- `firestore.rules` - Firestore security rules

## Firebase Setup (Console)
1. Create a Firebase project.
2. Add a Web App and copy config into `app.js` (`FIREBASE_CONFIG`).
3. Enable **Authentication → Email/Password**.
4. Create a **Firestore Database** and apply rules from `firestore.rules`.
5. Add authorized domains: `localhost`, `your-project.web.app`, `your-project.firebaseapp.com`.

## Run Locally
You can open `index.html` directly and the app UI will load.
If Firebase Auth is blocked by the browser on `file://`, use a local server.

Option A (simple static server):
```bash
python3 -m http.server 5173
```
Then open `http://localhost:5173`.

Option B (Firebase Hosting emulator):
```bash
firebase emulators:start --only hosting
```
Then open `http://localhost:5000`.

Note: this app connects to production Firebase by default. To use local Auth/Firestore emulators,
you would need to add emulator wiring in `app.js`.

## Deploy via Firebase CLI
```bash
firebase login
firebase use
firebase deploy --only firestore:rules,hosting
```

## GitHub Actions Deploy
Workflows in `.github/workflows/` deploy to Hosting on merge to `main`.
Add these repository secrets:
- `FIREBASE_SERVICE_ACCOUNT` (service account JSON)
- `FIREBASE_PROJECT_ID` (e.g. `weekly-timetable-eda8d`)

## Notes
- User documents are stored at `users/{uid}` in Firestore.
- The display name defaults to the email prefix if no profile name exists.
