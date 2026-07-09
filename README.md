# 📢 Real-Time Feedback & Complaint Management System

A modernized, premium real-time customer feedback and complaint management system. Designed for seamless venue-level customer interaction (via QR code scans) and immediate administrative response (via Socket.io and mobile push notifications).

---

## 🚀 Quick Access Links

| Module | Purpose | Live Link / Location |
| :--- | :--- | :--- |
| **📲 QR Feedback Portal** | Customer-facing portal to submit reviews/complaints | [Launch Portal](https://sanghi-brothers-feedback.onrender.com/) |
| **⚙️ Backend Server** | REST API & Socket.io engine | [API Endpoint](https://feedback-backend-fdux.onrender.com/) |
| **📦 Android Application** | Mobile Staff App APK | [Download Android APK (base.apk)](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/apk%20file/base.apk) |


---

## 🛠 Features

1. **Smart AI Classification**: Automatically detects whether a customer submission is a **Feedback** or a **Complaint** based on semantic keyphrase matching (e.g., *slow, poor, bug, kharab* auto-routes to Complaints, while *nice, excellent, badiya* routes to Feedback).
2. **Instant Real-Time Communication**: Uses **Socket.io** to push incoming complaints directly to the active dashboards without manual page reloads.
3. **Omnipresent Alerts**: Integrates **Expo Server SDK** to push mobile alerts directly to administrative staff on the move.
4. **Draft-to-Final Sync**: Live-typing states and draft submissions are synced from client portals to provide real-time engagement monitoring.
5. **Modern Visual Dashboards**: Fully interactive dashboard with clean charts, search indexing, category filtering, and one-click status resolution.

---

## 📐 System Architecture

```mermaid
sequenceDiagram
    autonumber
    actor Customer as 👤 Customer
    participant QR as 📱 QR Feedback Portal (Web)
    participant Server as ⚙️ Node.js Backend API
    participant DB as 💾 MongoDB Database
    participant Admin as 📊 React / HTML Admin Panel
    participant Mobile as 📲 Mobile Staff App (Expo)

    Customer->>QR: Scans QR code & types review
    QR->>Server: HTTP POST /feedback (message content)
    activate Server
    Note over Server: Run Smart Auto-Classifier<br/>Categorize: Feedback / Complaint
    Server->>DB: Saves review status: "Pending"
    Server->>Admin: Emits Socket.io "newFeedback"
    Server->>Mobile: Sends Push Notification via Expo SDK
    deactivate Server
    Admin->>Admin: Plays notification & shows live card
    Mobile->>Mobile: Displays push alert on lock screen
    Admin->>Server: Click ✅ "Mark Closed" (PATCH /feedback/:id/status)
    Server->>DB: Updates status to "Closed"
    Server->>Admin: Emits Socket.io "statusUpdated"
    Admin->>Admin: Strikes through message & resolves card
```

---

## 📁 Directory Structure

Click to explore each folder directly:

* 📂 [Backend](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/Backend) - Node.js server, Mongoose models, and WebSocket triggers.
* 📂 [Website_Admin](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/Website_Admin) - Modern React + Vite administrative control center with Framer Motion.
* 📂 [Website](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/Website) - Lightweight, single-file Vanilla JS & Socket.io dashboard.
* 📂 [QR](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/QR) - Vite + React web interface optimized for QR code scans.
* 📂 [Frontend](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/Frontend) - Expo React Native app code.
* 📂 [apk file](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/apk%20file) - Houses the compiled Android package ([base.apk](file:///e:/Products/Jo%20Hogya%20hai%20🟢🟢🟢/Feedback_App/Feedback/apk%20file/base.apk)).

---

## ⚙️ Setup & Local Execution

### 1. Backend Server Setup
1. Navigate to the backend folder:
   ```bash
   cd Backend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Set up environment variables in a `.env` file:
   ```env
   PORT=5000
   MONGO_URI=mongodb+srv://your_username:your_password@cluster.mongodb.net/your_db
   ```
4. Start the server:
   ```bash
   npm start
   ```

### 2. QR Portal & Admin Panel (React)
1. Navigate to the folder (e.g., `QR` or `Website_Admin`):
   ```bash
   cd QR
   # or
   cd Website_Admin
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the Vite development server:
   ```bash
   npm run dev
   ```

### 3. Mobile App (Expo)
1. Navigate to the app folder:
   ```bash
   cd Frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the Expo packager:
   ```bash
   npx expo start
   ```
4. Scan the QR code with Expo Go or build the binary.

---

## 📈 Database Schema (Mongoose)

The schema for submissions is structured as follows:

```javascript
const feedbackSchema = new mongoose.Schema({
  message: { type: String, required: true },
  type: { type: String, enum: ["Feedback", "Complaint"], required: true },
  status: { type: String, enum: ["Pending", "Closed"], default: "Pending" },
  time: { type: Date, default: Date.now },
  isDraft: { type: Boolean, default: false }
});
```
