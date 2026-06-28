# 🏦 Banking Management System

<div align="center">

![Banking](https://img.shields.io/badge/Project-Banking%20Management%20System-blue)
![React](https://img.shields.io/badge/Frontend-React-61DAFB)
![NodeJS](https://img.shields.io/badge/Backend-Node.js-339933)
![Express](https://img.shields.io/badge/API-Express-black)
![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791)
![MongoDB](https://img.shields.io/badge/NoSQL-MongoDB-47A248)
![License](https://img.shields.io/badge/License-MIT-green)

### Secure • Scalable • Modern Banking Solution

A full-stack Banking Management System built using **React, Node.js, Express, PostgreSQL, and MongoDB**, designed to automate banking operations including customer management, account handling, fund transfers, loan processing, transaction tracking, reporting, and analytics.

</div>

---

# 📖 Overview

The Banking Management System is a comprehensive web application that digitizes traditional banking services. It provides customers with secure online banking capabilities while enabling administrators and employees to efficiently manage banking operations.

This project integrates concepts from:

* Database Theory
* Database Laboratory
* Software Engineering
* Full Stack Web Development
* REST API Design
* Database Optimization
* Software Testing
* Agile Development

---

# ✨ Key Features

## 👤 Customer Management

* Customer Registration
* Customer Verification
* Profile Management
* KYC Information Storage
* Account Activation & Deactivation

## 💳 Account Management

* Savings Accounts
* Current Accounts
* Multiple Accounts Per Customer
* Account Status Tracking
* Balance Management

## 💰 Transaction Management

* Deposit Money
* Withdraw Money
* Transfer Funds
* Transaction History
* Mini Statements
* Monthly Statements

## 🏦 Loan Management

* Loan Applications
* Loan Approval Workflow
* EMI Calculation
* Loan Tracking
* Repayment Management

## 👨‍💼 Employee Management

* Employee Registration
* Role Assignment
* Branch Assignment
* Permission Management

## 🏢 Branch Management

* Multiple Branch Support
* Branch Managers
* Branch Performance Reports

## 📊 Analytics Dashboard

* Revenue Reports
* Monthly Transactions
* Loan Statistics
* Customer Growth Reports
* Branch Performance Analytics

## 🔒 Security

* JWT Authentication
* Password Hashing (bcrypt)
* Role-Based Access Control (RBAC)
* Input Validation
* SQL Injection Prevention
* Secure API Endpoints

---

# 🛠 Technology Stack

## Frontend

| Technology    | Purpose          |
| ------------- | ---------------- |
| React.js      | User Interface   |
| React Router  | Navigation       |
| Redux Toolkit | State Management |
| Tailwind CSS  | Styling          |
| Axios         | API Requests     |

## Backend

| Technology | Purpose           |
| ---------- | ----------------- |
| Node.js    | Runtime           |
| Express.js | Server Framework  |
| JWT        | Authentication    |
| bcrypt     | Password Security |
| Multer     | File Upload       |

## Database

| Technology | Purpose                     |
| ---------- | --------------------------- |
| PostgreSQL | Primary Relational Database |
| MongoDB    | Logs & Unstructured Data    |

## Development Tools

* Git
* GitHub
* Postman
* Swagger
* VS Code

---

# 🏗 System Architecture

```text
┌─────────────────┐
│   React Client  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  REST API Layer │
│ Node + Express  │
└────────┬────────┘
         │
 ┌───────┴────────┐
 ▼                ▼

PostgreSQL      MongoDB
(Relational)   (Logs/Notes)

```

# 📂 Project Structure

```bash
Banking-Management-System/
│
├── client/
│   ├── src/
│   ├── components/
│   ├── pages/
│   ├── redux/
│   └── services/
│
├── server/
│   ├── controllers/
│   ├── routes/
│   ├── middleware/
│   ├── models/
│   ├── config/
│   └── utils/
│
├── database/
│   ├── schema.sql
│   ├── seed.sql
│   └── procedures.sql
│
├── docs/
│   ├── SRS.pdf
│   ├── ER-Diagram.png
│   ├── DFD-Level-0.png
│   └── API-Documentation.pdf
│
└── README.md

```

# 🗄 Database Entities

## Main Tables

* Users
* Customers
* Accounts
* Transactions
* Loans
* Employees
* Branches
* Roles
* Permissions
* Audit Logs

### Relationships

```text
Customer
   │
   ├── Accounts
   │      │
   │      └── Transactions
   │
   └── Loans

Branch
   │
   ├── Employees
   └── Accounts
```

# 🚀 Installation

## Clone Repository

```bash
git clone https://github.com/yourusername/banking-management-system.git
```

```bash
cd banking-management-system
```

## Backend Setup

```bash
cd server
npm install
```

Create .env

```env
PORT=5000

DATABASE_URL=

JWT_SECRET=

MONGODB_URI=
```

Run Backend

```bash
npm run dev
```

## Frontend Setup

```bash
cd client
npm install
npm run dev
```

---

# 🔑 User Roles

## Customer

* Create Account
* Deposit Funds
* Withdraw Funds
* Transfer Money
* Apply for Loan
* View Transactions

## Employee

* Verify Customers
* Process Transactions
* Manage Accounts

## Manager

* Approve Loans
* Generate Reports
* Manage Employees

## Administrator

* Full System Access
* User Management
* Branch Management
* Security Controls

---

# 📡 API Modules

## Authentication

```http
POST /api/auth/register
POST /api/auth/login
```

## Customers

```http
GET    /api/customers
POST   /api/customers
PUT    /api/customers/:id
DELETE /api/customers/:id
```

## Accounts

```http
GET    /api/accounts
POST   /api/accounts
```

## Transactions

```http
POST /api/transactions/deposit
POST /api/transactions/withdraw
POST /api/transactions/transfer
```

## Loans

```http
POST /api/loans
GET  /api/loans
PUT  /api/loans/:id
```

---

# 📈 Performance Optimization

### Database Indexing

* Customer ID Index
* Account Number Index
* Transaction Date Index
* Loan Status Index

### Query Optimization

* EXPLAIN ANALYZE
* Composite Indexes
* Query Refactoring

---

# 🧪 Testing

## Unit Testing

```bash
npm test
```

## Integration Testing

```bash
npm run test:integration
```

### Testing Coverage

* Authentication
* Customer APIs
* Account APIs
* Transactions
* Loan Processing

---

# 🔒 Security Measures

* JWT Authentication
* Password Hashing
* Input Validation
* SQL Injection Protection
* XSS Prevention
* Role-Based Access Control
* Secure API Middleware

---

# 📚 Academic Learning Outcomes

This project demonstrates:

✅ Database Design

✅ ER Modeling

✅ Normalization (1NF → 3NF)

✅ SQL Queries

✅ Transactions

✅ Triggers

✅ Stored Procedures

✅ Indexing

✅ Query Optimization

✅ NoSQL Integration

✅ REST API Development

✅ React Frontend Development

✅ Software Engineering Principles

✅ Agile Workflow

✅ Software Testing

---

# 📅 Development Roadmap

| Phase   | Description                      |
| ------- | -------------------------------- |
| Phase 1 | Requirements & Database Design   |
| Phase 2 | SQL & Backend Development        |
| Phase 3 | Optimization & Advanced Database |
| Phase 4 | Frontend & Testing               |
| Phase 5 | Final Deployment & Documentation |

---

# 👨‍💻 Author

**Rakib Hasan Prmanik**


Banking Management System

Database Theory • Database Lab • Software Engineering

---

# ⭐ Support

If you found this project useful:

⭐ Star the repository

🍴 Fork the repository

📢 Share with others

---

# 📄 License

This project is licensed under the MIT License.

---

<div align="center">

### 🏦 Banking Management System

Building Secure Banking Solutions with Modern Technologies 🚀

</div>
#   B a n k i n g _ M a n a g e m e n t _ S y s t e m 2  
 