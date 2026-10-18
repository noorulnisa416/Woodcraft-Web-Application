# 🪵 Woodcraft – Workshop Management System

A modern, full-stack workshop management platform tailored for custom woodworking businesses, carpentry workshops, and artisan studios. **Woodcraft** streamlines customer order commissions, artisan worklog & wage tracking, raw material inventory, billing & invoice management, and administrative approval workflows in a unified, role-aware dashboard.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features & Modules](#-key-features--modules)
- [User Roles & Permissions](#-user-roles--permissions)
- [Demo Credentials](#-demo-credentials)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Directory Structure](#-directory-structure)
- [Installation & Setup](#-installation--setup)
  - [Prerequisites](#prerequisites)
  - [1. Frontend Setup (Quick Start)](#1-frontend-setup-quick-start)
  - [2. Backend Setup (Optional for Full API)](#2-backend-setup-optional-for-full-api)
  - [3. Database Setup](#3-database-setup)
- [Application Routes](#-application-routes)
- [API Reference](#-api-reference)
- [Development Mode & Data Handling](#-development-mode--data-handling)
- [Available Scripts](#-available-scripts)
- [Academic & Portfolio Submission Notes](#-academic--portfolio-submission-notes)

---

## 🌟 Overview

Running a custom woodcraft workshop involves coordinating bespoke customer requests, tracking precious timber stock, assigning skilled artisans, monitoring billable hours, and processing multi-stage payments.

**Woodcraft** addresses these challenges by offering:
- **Role-Aware Portals**: Dedicated UI experiences and views for Administrators, Artisans/Employees, and Customers.
- **Complete Commission Lifecycle**: From order inquiry and material estimation to crafting, delivery, and receipt generation.
- **Built-in Offline / DEV Mode**: Zero-configuration mock data fallback with `localStorage` persistence, allowing full evaluation and UI interaction without requiring an active MySQL database connection.
- **Production-Ready REST API**: Node.js, Express, and MySQL backend with JWT authentication and parameterized SQL queries.

---

## 🚀 Key Features & Modules

### 1. 🔐 Authentication & Access Control (RBAC)
- Secure JWT-based authentication and `bcrypt` password hashing.
- Role-based route protection (`admin`, `customer`, `employee`).
- **Registration Approval Workflow**:
  - **Admin Accounts**: Instant registration and immediate access.
  - **Customer & Employee Accounts**: Registration requests enter a pending approval queue managed by the Administrator.
  - **Existing Registered Users**: Seamless login without recurring approvals.

### 2. 📋 Commission & Order Management
- Order lifecycle tracking: `Pending` ➔ `In Progress` ➔ `Completed` ➔ `Delivered`.
- Order categorization: *Custom Design*, *Furniture Creation*, *Wood Repair / Restoration*.
- Material allocation per order with automated stock deduction.
- Employee/Artisan task assignment and logged labor hours tracking.

### 3. 🪵 Inventory & Raw Materials Management
- Real-time stock level monitoring for lumber, hardwoods, finishes, and hardware.
- Low-stock threshold alerts to prevent workshop production bottlenecks.
- Unit cost tracking, stock replenishment, and material utilization analytics.

### 4. 👥 Employee & Artisan Directory
- Detailed artisan profiles with skill tags (e.g., *Joinery*, *Woodturning*, *CNC Carving*, *Finishing*).
- Hourly wage rate configuration and active assignment metrics.
- Comprehensive task allocation overview for workshop managers.

### 5. ⏱️ Worklog & Wage Tracking
- Artisans can log daily work hours against specific assigned orders.
- Task notes, completion status, and logged time records.
- **Automated Wage Calculations**: Breakdown of total hours worked, hourly rate multiplier, and gross earnings summary.

### 6. 💳 Invoicing, Billing & Receipts
- Unified financial hub for workshop billing.
- Invoices linked directly to customer orders with status tracking: `Unpaid`, `Partial`, `Paid`.
- Payment recording, balance computation, and printable receipt actions.

### 7. 📊 Reports & Workshop Analytics
- Visual analytics powered by Recharts.
- Monthly revenue trends and financial health breakdown.
- Material consumption metrics and popular wood types.
- Artisan productivity and on-time order completion statistics.

### 8. 🛡️ User Access & Audit Management (Admin Only)
- Pending registration review queue (Approve / Reject actions).
- Active user directory and account status controls (Active / Blocked).
- System audit log view for administrative oversight.

---

## 👥 User Roles & Permissions

| Role | Accessible Modules & Permissions |
| :--- | :--- |
| **Admin** | Full system control: User approvals & access control, all orders, inventory management, employee directory, billing & invoices, reports & analytics, system configuration. |
| **Customer** | Place new custom commission orders, track order progress in real-time, view invoices, make payments, and view receipts. |
| **Employee** | View assigned workshop tasks & orders, update order status, submit daily worklogs, and review personal wage summaries. |

---

## 🔑 Demo Credentials

The application includes pre-configured demo credentials in development mode for instant testing:

| Role | Email Address | Password | Default Access |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@woodcraft.com` | `admin123` | Full Administrator Dashboard |
| **Customer** | `customer@woodcraft.com` | `customer123` | Customer Portal & Order Tracker |
| **Employee** | `employee@woodcraft.com` | `employee123` | Artisan Worklog & Task Board |

> 💡 **Tip**: On the login page, you can use the quick demo account buttons to fill credentials automatically.

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: [React 18](https://react.dev/) with [TypeScript](https://www.typescriptlang.org/)
- **Build Tool**: [Vite](https://vitejs.dev/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) with `tailwindcss-animate`
- **UI Components**: [shadcn/ui](https://ui.shadcn.com/) built on [Radix UI](https://www.radix-ui.com/) primitives
- **Icons**: [Lucide React](https://lucide.dev/)
- **Charts & Data Viz**: [Recharts](https://recharts.org/)
- **State & Data Fetching**: [TanStack React Query](https://tanstack.com/query) & [Axios](https://axios-http.com/)
- **Routing**: [React Router v6](https://reactrouter.com/)
- **Notifications**: [Sonner](https://sonner.emilkowal.ski/) & Radix Toast

### Backend (Reference & API)
- **Runtime**: [Node.js](https://nodejs.org/) (ES Modules)
- **Web Framework**: [Express.js](https://expressjs.com/)
- **Database Engine**: [MySQL](https://www.mysql.com/) via `mysql2/promise`
- **Authentication**: `jsonwebtoken` (JWT) & `bcrypt`
- **Configuration**: `cors`, `dotenv`

---

## 🏗️ Project Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                       React Frontend                        │
│   (Vite + TypeScript + Tailwind CSS + shadcn/ui + Router)   │
└──────────────┬──────────────────────────────┬───────────────┘
               │                              │
     [DEV Mode Fallback]             [Live API Requests]
               │                              │
               ▼                              ▼
┌─────────────────────────────┐ ┌─────────────────────────────┐
│    Local Storage Engine     │ │     Express REST API        │
│ (devData.ts / Mock Store)   │ │  (JWT Auth, Routes, CORS)   │
└─────────────────────────────┘ └──────────────┬──────────────┘
                                               │
                                               ▼
                                ┌─────────────────────────────┐
                                │        MySQL Database       │
                                │ (woodcraft.sql Schema)      │
                                └─────────────────────────────┘
```

---

## 📁 Directory Structure

```
Woodcraft/
├── backend/                        # Node.js + Express backend
│   ├── middleware/
│   │   └── auth.js                 # JWT verification & role authorization
│   ├── routes/
│   │   ├── auth.js                 # Login & registration endpoints
│   │   ├── billing.js              # Payment transactions
│   │   ├── customers.js            # Customer management
│   │   ├── employees.js            # Artisan data & wages
│   │   ├── inventory.js            # Material stock & prices
│   │   ├── invoices.js             # Invoice generation & status
│   │   ├── orders.js               # Order lifecycle & material linking
│   │   └── worklog.js              # Artisan time logging
│   ├── db.js                       # MySQL connection pool
│   ├── package.json                # Backend dependencies
│   ├── server.js                   # Express server entry point
│   └── .env                        # Backend environment variables
│
├── database/                       # Database schemas & exports
│   ├── woodcraft.sql               # Core MySQL database dump
│   └── woodcraft_full_schema.sql   # Extended SQL schema with seeds
│
├── reference/                      # Documentation reference copy
│   └── README.md                   # Backend implementation guide
│
├── src/                            # React frontend application
│   ├── assets/                     # Logos, brand assets, and icons
│   ├── components/                 # Reusable UI & layout components
│   │   ├── layout/                 # AppShell, Navbar, Sidebar
│   │   └── ui/                     # shadcn/ui component library
│   ├── hooks/                      # Custom React hooks (e.g., use-toast)
│   ├── lib/                        # Auth context, API client, mock data
│   │   ├── api.ts                  # Axios instance with JWT interceptor
│   │   ├── auth.tsx                # AuthProvider & role guard helpers
│   │   ├── calc.ts                 # Financial & wage calculation helpers
│   │   ├── devData.ts              # Local mock database & seed values
│   │   └── store.ts                # Client storage helpers
│   ├── pages/                      # Page views & routing
│   │   ├── dashboards/             # Role-specific dashboard overviews
│   │   │   ├── AdminOverview.tsx
│   │   │   ├── CustomerOverview.tsx
│   │   │   └── EmployeeOverview.tsx
│   │   ├── AdminProfile.tsx        # Admin profile settings
│   │   ├── Billing.tsx             # Billing, invoices & receipts
│   │   ├── CustomerProfile.tsx     # Customer account management
│   │   ├── Customers.tsx           # Customer directory for Admin
│   │   ├── Dashboard.tsx           # Dynamic role dashboard router
│   │   ├── EmployeeProfile.tsx     # Artisan account management
│   │   ├── Employees.tsx           # Artisan management for Admin
│   │   ├── Index.tsx               # Public landing page
│   │   ├── Inventory.tsx           # Raw materials & stock
│   │   ├── Login.tsx               # Authentication portal
│   │   ├── NotFound.tsx            # 404 handler
│   │   ├── Orders.tsx              # Commission & task manager
│   │   ├── Register.tsx            # Registration with approval flow
│   │   ├── Reports.tsx             # Analytics & financial reports
│   │   ├── UserAccess.tsx          # User approvals & access control
│   │   ├── WageSummary.tsx         # Artisan wage tracker
│   │   └── Worklog.tsx             # Artisan time-tracking
│   ├── services/                   # API integration services
│   ├── App.tsx                     # Route definitions & providers
│   ├── main.tsx                    # React DOM entry point
│   └── index.css                   # Global styles & design tokens
│
├── public/                         # Static web assets
├── package.json                    # Frontend dependencies & scripts
├── tailwind.config.ts              # Tailwind CSS configuration
├── tsconfig.json                   # TypeScript configuration
└── vite.config.ts                  # Vite build configuration
```

---

## 💻 Installation & Setup

### Prerequisites
- **Node.js**: `v18.0.0` or higher
- **npm** or **bun** / **yarn** / **pnpm**
- **MySQL Server** *(Optional: Only needed if running the live backend API)*

---

### 1. Frontend Setup (Quick Start)

The frontend can run standalone with its integrated mock-data engine for instant preview and testing.

```bash
# Clone or navigate to the project directory
cd Woodcraft

# Install dependencies
npm install

# Start the Vite development server
npm run dev
```

Open your browser and navigate to:
```
http://localhost:5173
```

---

### 2. Backend Setup (Optional for Full API)

To run the Node.js + Express backend API:

```bash
# Navigate to the backend directory
cd backend

# Install backend dependencies
npm install

# Configure environment variables in backend/.env
# (Ensure DB_HOST, DB_USER, DB_PASS, DB_NAME, and PORT are set)

# Start the backend server
npm run dev
# or
node server.js
```

The backend server will start on `http://localhost:5000`.

---

### 3. Database Setup

To initialize the MySQL database:

1. Start your local MySQL service (e.g., via MySQL Workbench, XAMPP, or CLI).
2. Create and seed the database using the provided SQL dump:

```bash
mysql -u root -p < database/woodcraft.sql
```

3. Update the credentials in `backend/.env` to match your local database settings:
```env
DB_HOST=localhost
DB_USER=root
DB_PASS=your_mysql_password
DB_NAME=woodcraft
JWT_SECRET=your_jwt_secret_key
PORT=5000
```

---

## 🚦 Application Routes

| Path | Description | Access Level |
| :--- | :--- | :--- |
| `/` | Public Workshop Homepage & Showcase | Public |
| `/login` | User Authentication Portal | Public |
| `/register` | Account Registration Request | Public |
| `/app` | Role-Aware Overview Dashboard | Authenticated (All Roles) |
| `/app/orders` | Commission Management & Task Tracking | Admin, Customer, Employee |
| `/app/inventory` | Material Stock & Pricing Management | Admin |
| `/app/employees` | Artisan Management & Directory | Admin |
| `/app/customers` | Customer Directory | Admin |
| `/app/billing` | Invoicing, Payments & Receipts | Admin, Customer |
| `/app/worklog` | Daily Time-Tracking & Task Logging | Admin, Employee |
| `/app/wage-summary` | Artisan Earnings & Wage Breakdown | Employee |
| `/app/reports` | Business Analytics & Performance Reports | Admin |
| `/app/user-access` | Registration Approvals & User Access | Admin |
| `/admin/profile` | Administrator Profile Settings | Admin |
| `/employee/profile` | Artisan Profile Settings | Employee |
| `/customer/profile` | Customer Profile Settings | Customer |

---

## 📡 API Reference

When the backend API is active, the following REST endpoints are available under `http://localhost:5000`:

| Method | Endpoint | Description | Auth Required |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new user | No |
| `POST` | `/api/auth/login` | Authenticate user & receive JWT token | No |
| `GET` | `/api/orders` | Fetch all orders with linked materials | Yes |
| `POST` | `/api/orders` | Create a new order with material allocation | Yes |
| `PUT` | `/api/orders/:id` | Update order details / status | Yes |
| `DELETE`| `/api/orders/:id` | Remove an order | Yes |
| `GET` | `/api/inventory` | List all materials & current stock | Yes |
| `POST` | `/api/inventory` | Add new raw material to inventory | Yes |
| `PUT` | `/api/inventory/:id`| Update material stock / price | Yes |
| `GET` | `/api/invoices` | List all invoices with customer & order info | Yes |
| `POST` | `/api/invoices` | Generate a new invoice | Yes |
| `PUT` | `/api/invoices/:id` | Record payment against invoice | Yes |
| `GET` | `/api/employees` | List artisans with hourly rates & skills | Yes |
| `GET` | `/api/customers` | List registered customer records | Yes |
| `GET` | `/api/worklog` | Retrieve logged work hours | Yes |
| `POST` | `/api/worklog` | Submit new worklog entry | Yes |

---

## 💾 Development Mode & Data Handling

The frontend is architected with a dual-layer data strategy:
1. **Zero-Configuration DEV Mode**: When testing without the backend, the UI uses rich mock datasets (`src/lib/devData.ts`) and synchronizes interactive updates to browser `localStorage`.
2. **Synchronized Keys**:
   - `user` / `token`: User session state
   - `dev_orders`: Persisted orders and status updates
   - `dev_worklogs`: Artisan logged hours
   - `dev_pending_requests`: Pending user registration approval queue
3. **Seamless API Mode**: When connected to the Express backend, Axios calls attach the JWT bearer token automatically via `src/lib/api.ts`.

---

## 📜 Available Scripts

In the root directory, you can execute:

| Command | Description |
| :--- | :--- |
| `npm run dev` | Starts the Vite development server with HMR at `http://localhost:5173`. |
| `npm run build` | Compiles and builds production-ready bundle into `/dist`. |
| `npm run preview` | Locally previews the production build. |
| `npm run lint` | Runs ESLint to identify code quality and style issues. |
| `npm run test` | Runs the test suite using Vitest. |
| `npm run test:watch` | Runs Vitest in interactive watch mode. |

In the `backend/` directory:

| Command | Description |
| :--- | :--- |
| `npm start` | Runs the Express server using Node.js. |
| `npm run dev` | Runs the server in development environment mode. |

---

## 🎓 Academic & Portfolio Submission Notes

This repository is structured for academic project submissions and portfolio showcases:
- **Full Architecture Documentation**: Includes schema scripts ([`database/woodcraft.sql`](database/woodcraft.sql) and [`database/woodcraft_full_schema.sql`](database/woodcraft_full_schema.sql)) and backend references ([`reference/README.md`](reference/README.md)).
- **Self-Contained Evaluation**: Evaluators can instantly test the entire application, navigate all role views, and submit approval workflows directly from the browser without installing database drivers.
- **Enterprise Design Standards**: Clean separation of concerns, TypeScript type safety, custom design tokens, accessible UI components, and modular services.

---

<div align="center">
  <p>Crafted with precision for <strong>Woodcraft Workshop Management</strong>.</p>
</div>
