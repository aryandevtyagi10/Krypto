# Krypto 💰

**A full-stack cryptocurrency price tracker** built with **React** and **Flask**. Use it locally with SQLite, or deploy to AWS with DynamoDB, SNS, and EC2.

---

## Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Environment & Configuration](#️-environment--configuration)
- [Database](#-database)
- [API Overview](#-api-overview)
- [Deployment](#-deployment)
- [Default Credentials](#-default-credentials)

---

## 🚀 Features

| Feature | Description |
|--------|-------------|
| **Live prices** | Real-time crypto data from CoinGecko API (with optional API key for better rate limits) |
| **Watchlist** | Add and remove coins to a personal watchlist (persisted per user) |
| **Auth** | JWT-based login/register with secure password hashing |
| **Roles** | User and Admin roles with protected routes |
| **Admin panel** | View users, block/unblock accounts, and basic metrics |
| **Compare** | Side-by-side comparison of two coins with charts |
| **Local + cloud** | SQLite for local dev; AWS-ready (DynamoDB, SNS, EC2) |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18, React Router, Axios, Material UI, Chart.js, Framer Motion, React Toastify |
| **Backend** | Python 3, Flask, Flask-CORS, Flask-JWT-Extended |
| **Auth** | JWT (access tokens) |
| **Database (local)** | SQLite |
| **Database (cloud)** | AWS DynamoDB |
| **Notifications** | AWS SNS |
| **Hosting** | AWS EC2 (backend), Netlify (frontend) |
| **External API** | CoinGecko |

---

## 📂 Repository Structure

```
Krypto-main/
├── backend/
│   ├── app.py              # Flask app (local)
│   ├── aws_app.py          # Flask app (AWS config)
│   ├── init_db.py           # DB schema setup
│   ├── models.py            # SQLite helpers
│   ├── requirements.txt
│   ├── routes/
│   │   ├── auth.py         # Login, register
│   │   ├── admin.py        # Admin dashboard, user management
│   │   ├── watchlist.py    # Watchlist CRUD
│   │   └── crypto.py       # Crypto-related endpoints
│   └── services/
│       └── price_fetcher.py
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── api/            # CoinGecko client
│   │   ├── components/
│   │   ├── pages/
│   │   └── functions/
│   ├── package.json
│   ├── .env.example
│   └── netlify.toml
│
├── .gitignore
└── README.md
```

---

## 📥 Getting Started

### Prerequisites

- **Node.js** (v16+)
- **Python** (3.8+)
- **Git**

### 1. Clone the repo

```bash
git clone https://github.com/aryandevtyagi10/crypto-price-tracker.git
cd crypto-price-tracker
```

If the repo is named differently locally (e.g. `Krypto-main`), `cd` into that folder.

### 2. Backend (Flask)

```bash
cd backend
python -m venv venv
```

**Windows (PowerShell / CMD):**
```bash
venv\Scripts\activate
```

**macOS / Linux:**
```bash
source venv/bin/activate
```

Then:

```bash
pip install -r requirements.txt
python app.py
```

Backend runs at **http://127.0.0.1:5000**.

### 3. Frontend (React)

Open a new terminal:

```bash
cd frontend
npm install
npm start
```

Frontend runs at **http://localhost:3000**.

---

## ⚙️ Environment & Configuration

### Backend

- **JWT secret**: Set in `app.py` (`JWT_SECRET_KEY`). Change this in production.
- **Database**: SQLite file `backend/database.db` is created automatically.

### Frontend

- **API base URL**  
  In `src/api.js`, the axios base URL is set to your backend (e.g. `http://localhost:5000`). Update it for production or a different host.

- **CoinGecko API key** (optional but recommended)  
  Reduces rate limits and improves loading:

  1. Copy `.env.example` to `.env` in the `frontend` folder.
  2. Get a key from [CoinGecko API](https://www.coingecko.com/en/api).
  3. In `.env`:
     ```env
     REACT_APP_COINGECKO_API_KEY=your_api_key_here
     ```
  4. Restart `npm start` after changing `.env`.

---

## 🗄 Database

**Local:** SQLite at `backend/database.db`.

| Table     | Purpose                          |
|----------|-----------------------------------|
| `users`  | Email, hashed password, role      |
| `watchlist` | User watchlist entries (e.g. coin_id) |

Tables are created on first run via `init_db` / `models`.

---

## 📡 API Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST   | `/auth/register` | Register new user |
| POST   | `/auth/login`    | Login, returns JWT |
| GET    | `/watchlist/all` | Current user’s watchlist |
| POST   | `/watchlist/add` | Add coin to watchlist |
| POST   | `/watchlist/remove` | Remove from watchlist |
| GET    | `/admin/...`     | Admin-only (users, block, etc.) |

All protected routes expect the JWT in the `Authorization: Bearer <token>` header.

---

## 🚀 Deployment

- **Frontend:** Configured for Netlify (`netlify.toml`). Set build command to `npm run build` and publish the `build` folder. Point the app’s API base URL to your deployed backend.
- **Backend:** Use `aws_app.py` and your AWS credentials/config for DynamoDB and SNS. Run on EC2 or another host and set CORS to your frontend origin.

---

## 🔐 Default Credentials

**Admin account (pre-seeded):**

- **Email:** `aryandt@gmail.com`
- **Password:** `aryandt`

Use these to access the admin dashboard and user management.

---

## 📄 License

This project is for educational and portfolio use. CoinGecko data is subject to [CoinGecko’s terms](https://www.coingecko.com/en/api_terms).
