# Moment


---
📘 Project Plan: Moment – Focus Timer App
Overview
Moment is a cross-platform productivity app designed to help users build focus habits through customizable work and break sessions. Inspired by the Pomodoro technique, Moment allows users to customize their cycles, track progress, view AI-powered summaries, and stay motivated with streaks and reminders.
The app will launch on Web and Android (mobile) with plans to expand mobile functionality in future releases.
Tech Stack:
Monorepo: T3 Turbo
Backend & DB: Neon Postgres + Drizzle ORM
Auth: Better Auth (Google OAuth)
Frontend: Web (Next.js + React) and Mobile (Expo/React Native)

---
🎯 First Release (MVP)
1. Authentication
Google OAuth login (via Better Auth).
On first login, user is prompted for customization (see below).

---
2. Customization Flow (First Login + Settings)
On first login, app asks for:
Continuous sessions per day (default: 2).
Cycles per session (default: 4).
Work duration (default: 25 min).
Short break duration (default: 5 min).
Long break duration (default: 15 min).

Once saved:
firstLogin = false.
Data stored in Postgres.

Users can re-customize anytime via Settings.

---
3. Timer Flow (Core Functionality)
Main Timer Page:
If no active session → show “last work summary” + CTA to Start New Session.
If active session → show live timer for current phase (work/break).

Controls:
Pause
Add time (+1–5 minutes configurable)
Skip current timer
Cancel session (ends session, saves partial data).

Data Saving Rules:
Save on each checkpoint (focus completed, short break completed, long break completed).
Save when session is cancelled.
Save when session is successfully completed.

AI-powered motivational messages during active session (e.g., “Almost there!”, “Stay sharp, you’re crushing it!”).

---
4. Weekly Dashboard (AI Summary + Graphs)
AI-generated weekly summary (progress, consistency, streaks, productivity insights).
Charts & Graphs:
Sessions completed
Time spent focusing
Break/work ratio

CTA: “Start New Session” button.

---
5. History & Streaks
History Page:
Displays all tracked sessions (daily logs).
Each day/session entry is clickable → opens dynamic route with same timer summary view.

Streak Counter:
Increments if user completes at least one session per day.
Resets if a day is missed.

Reminders/Alarms:
Small alert at each checkpoint (end of work or break).

---
6. Web Landing Page
Public-facing landing page with:
App intro (features & screenshots).
Call-to-action: Login (Web app) or Download (Mobile app).

7. Subscription
Subscription to add more presets to the set , free -> 1 preset, paid ? 3 presets and mark those preset model as paid and if not subscribed keep it false
---
🚀 Second Release (Mobile-First Features)
1. Push Notifications
Reminder when:
Work session ends.
Break ends.
Session starts (if user scheduled it).

---
2. Background Timers
Timer continues in background.
Notifications remind user at checkpoints.

---
3. Music-Friendly Alarms
Short alarm sound (5s max).
If music is playing → pause music → play alarm → resume music.

---
4. Offline Mode (Mobile Only)
If logged in on mobile (session valid for 1 year):
App works offline using local storage.
Stores offline sessions.
Syncs with database once user reconnects to internet.

---
📅 Release Strategy
First Release (MVP – Web + Mobile)
Google OAuth
Customization settings
Timer flow with pause/skip/add/cancel
AI motivational messages
AI-powered weekly dashboard + graphs
History + streak counter
Alarms/reminders
Web landing page

Second Release (Mobile Upgrades)
Push notifications
Background timers
Music-friendly alarms
Offline-first mode

---
🧩 Database Design (High-Level)
Users Table
id
email
firstLogin (bool)
settings (JSON: work/break/customization)
streakCount

Sessions Table
id
userId
startedAt
endedAt
status (active, completed, cancelled)
cyclesCompleted

Checkpoints Table
id
sessionId
type (work, shortBreak, longBreak)
completedAt

---
📌 Notes
AI features (weekly summary + motivational messages) can start simple (rule-based prompts) and improve over time.
For alarms & push notifications, mobile implementation will be prioritized in second release.
Offline-first is optional for web but critical for mobile adoption.

---
