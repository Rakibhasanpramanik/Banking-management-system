# NovaBank — Full-Stack Banking Management System (Production Edition)

A complete banking management system built with **Next.js 14** (App Router), **Node.js / Express**, and **MySQL** — with mobile banking deposits (bKash, Nagad, Rocket) and bank transfer support, plus production-grade security and reliability.

## ✨ Features

### Customer side
- Register (auto-creates a savings account with a unique account number) & secure JWT login
- Account lockout after repeated failed logins (brute-force protection)
- Dashboard: balance overview, quick actions, recent activity
- **Multi-channel deposits:**
  - **Cash** — instant, in-branch / admin-assisted
  - **bKash / Nagad / Rocket** — customer sends money to the merchant number shown on screen, then submits the sender number + Transaction ID (TrxID) for verification
  - **Bank Transfer** — customer transfers to the displayed bank account, then submits proof
  - All mobile banking / bank deposits go into a **pending verification queue** and are credited only after an admin approves them — exactly like real Bangladeshi merchant flows without a payment gateway
  - Duplicate TrxID submissions are automatically blocked
  - Customers can track the status (pending / approved / rejected) of every deposit request in real time
- Withdraw funds (instant, balance-checked)
- Transfer funds to any other account number (instant, atomic, with a daily transfer limit)
- Full transaction history with channel badges, filters and pagination
- Profile management (update details, change password)

### Admin panel
- Dashboard stats: total customers, active/blocked counts, total bank balance, transaction counts, and a **live pending-deposit alert** with total value awaiting verification
- **Deposit Requests queue** — review each bKash/Nagad/Rocket/bank submission (sender number, TrxID, amount), Approve to instantly credit the customer or Reject with a reason shown back to them
- Manage users: search/filter, activate, block, delete
- Manually credit/debit any customer's balance (creates an auditable transaction)
- View the full bank-wide transaction ledger with filters + pagination
- Every sensitive admin action (status changes, balance adjustments, deposit approvals) is written to an **audit log** with the admin's ID and IP
- Role-based route protection (admin vs customer areas fully separated)

### Production-grade backend
- **Validation:** every input is validated server-side with `express-validator` (rejects malformed emails, out-of-range amounts, missing fields, etc.)
- **Security headers:** `helmet` (CSP, HSTS, etc.), HTTP Parameter Pollution protection (`hpp`), payload size limits
- **Rate limiting:** separate limiters for general API traffic, auth endpoints (login/register), and money-movement endpoints
- **Centralized error handling:** a single `AppError` class + error middleware turns every failure into a clean, consistent JSON response — no leaking stack traces to clients
- **Structured logging:** Winston logs to console + rotating files (`logs/error.log`, `logs/combined.log`), plus Morgan HTTP request logging
- **Environment validation:** the server refuses to boot if required `.env` values (DB creds, `JWT_SECRET`) are missing or a weak secret is used
- **Money-safe transactions:** deposits/withdrawals/transfers/approvals use MySQL transactions with row-level locking (`FOR UPDATE`) to prevent race conditions and double-spending
- **Graceful shutdown** and unhandled-rejection safety nets
- **Health check** endpoint (`/health`) for uptime monitoring / load balancers

### UI/UX
- Clean, modern, responsive design (Tailwind CSS), currency displayed in **৳ (BDT)**
- Payment-method picker on the Deposit page (Cash / bKash / Nagad / Rocket / Bank) with contextual instructions, copyable merchant numbers, and a live deposit-request tracker
- Admin sidebar shows a **live badge** with the pending deposit count
- Dedicated mobile navigation drawer
- Toast notifications for every action
- Landing page, login and register pages with a polished two-panel layout

---

## 🗂 Project Structure

```
bank-system/
├── backend/
│   ├── config/         # DB pool + env validation
│   ├── controllers/    # Business logic (auth, user, transactions, admin, config)
│   ├── middleware/      # auth, admin guard, validation, rate limiters, error handler
│   ├── validators/      # express-validator rule sets
│   ├── routes/           # API routes
│   ├── utils/             # AppError, asyncHandler, logger, token, account number gen
│   ├── db/schema.sql       # Database schema (users, accounts, transactions,
│   │                        deposit_requests, audit_logs, support_tickets)
│   ├── seed.js               # Creates a default admin account
│   └── server.js
└── frontend/
    ├── app/                # Pages: landing, login, register, dashboard, admin
    │   ├── dashboard/deposit   # Multi-channel deposit page
    │   └── admin/deposits       # Admin deposit verification queue
    ├── components/          # Sidebar, Topbar, Cards, ProtectedRoute...
    ├── context/AuthContext.js
    └── lib/api.js, utils.js  # Axios instance + currency/channel helpers
```

---

## 🚀 Getting Started

### 1. Database setup
```bash
mysql -u root -p < backend/db/schema.sql
```

### 2. Backend setup
```bash
cd backend
cp .env.example .env
# Edit .env: set DB_PASSWORD, a strong JWT_SECRET (20+ random chars),
# and your real bKash/Nagad/Rocket/bank receiving details (MERCHANT_* vars)
npm install
node seed.js             # creates default admin: admin@bank.com / Admin@123
npm run dev                # starts API on http://localhost:5000
```

### 3. Frontend setup
```bash
cd frontend
cp .env.local.example .env.local
npm install
npm run dev               # starts app on http://localhost:3000
```

### 4. Log in
- Open http://localhost:3000
- Register a new customer account, or log in as admin with:
  - **Email:** admin@bank.com
  - **Password:** Admin@123 — **change this immediately in any real deployment**

### 5. Try the deposit flow
- As a customer, go to **Deposit**, pick bKash/Nagad/Rocket/Bank, follow the on-screen instructions, and submit a (test) TrxID
- Log in as admin, open **Deposit Requests**, and Approve or Reject it — the customer's balance updates instantly on approval

---

## 🔐 Security notes
- Passwords are hashed with bcrypt (12 rounds by default, configurable)
- All protected routes require a valid JWT; user status is re-checked on every request so a blocked account is rejected immediately even with a still-valid token
- Repeated failed logins temporarily lock the account (configurable via `MAX_LOGIN_ATTEMPTS` / `LOGIN_LOCK_MINUTES`)
- Money transactions use MySQL transactions with row locking to prevent race conditions
- Mobile banking / bank deposits can never self-credit — an admin must verify and approve every one, with duplicate TrxIDs rejected outright
- All admin actions are recorded in `audit_logs` for accountability
- Rate limiting on auth and transaction endpoints blunts brute-force and abuse

## 🛠 Tech Stack
- **Frontend:** Next.js 14, React 18, Tailwind CSS, Axios, lucide-react, react-hot-toast
- **Backend:** Node.js, Express, MySQL2, JWT, bcryptjs, express-validator, helmet, express-rate-limit, winston, morgan
- **Database:** MySQL

## 📌 Notes / possible next steps
- Integrate real bKash/Nagad Payment Gateway APIs (Merchant/PGW) to auto-verify TrxIDs instead of manual admin review
- Add SMS/email notifications when a deposit is approved or rejected
- Add refresh tokens for longer, more secure sessions
- Add PDF/CSV statement export
