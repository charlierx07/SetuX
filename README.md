<div align="center">

# 🌐 SetuX

### *Bridging Societal Problems with Academic & Industry Solutions*

[![Node.js](https://img.shields.io/badge/Node.js-≥18.0.0-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![Express](https://img.shields.io/badge/Express-5.x-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/atlas)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4.x-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)

</div>

---

## 📖 Overview

**SetuX** is a full-stack civic-tech platform that empowers citizens to report real-world problems and uses an **AI-powered multi-agent engine** to automatically analyze them, detect duplicates, and match them with the most relevant universities and industry partners capable of solving them.

> The name *SetuX* comes from the Sanskrit word **Setu (सेतु)** meaning *"bridge"* — SetuX bridges the gap between grassroots problems and the academic/industry ecosystem.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 🧾 **Problem Reporting** | Citizens submit problems with title, description, location, and media attachments |
| 🤖 **AI Multi-Agent Analysis** | A Python FastAPI engine auto-analyzes each submission for category, priority & domain |
| 🔍 **Duplicate Detection** | AI agents flag similar/duplicate problems before they are stored |
| 🏛️ **University Matching** | Recommends top universities based on expertise relevant to the problem |
| 🏭 **Industry Matching** | Surfaces relevant industry partners that can solve or fund the problem |
| 👮 **Admin Dashboard** | Dedicated portal for administrators to review, approve, or reject problems |
| 🔐 **JWT Authentication** | Secure user auth with role-based access (citizen / admin) |
| 📱 **Responsive UI** | Modern, mobile-friendly frontend built with React 19 + Tailwind CSS 4 |

---

## 🏗️ Architecture

```
SetuX/
├── backend/                  # Node.js + Express REST API
│   ├── config/
│   │   └── db.js             # MongoDB Atlas connection
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   └── problem.controller.js
│   ├── middleware/
│   │   └── auth.middleware.js
│   ├── models/
│   │   ├── user.model.js
│   │   └── problem.model.js
│   ├── routes/
│   │   ├── auth.routes.js
│   │   └── problem.routes.js
│   ├── .env.example
│   └── server.js
│
└── frontend/
    └── setux-frontend/       # React 19 + Vite + Tailwind CSS 4
        ├── src/
        │   ├── components/   # Reusable UI components
        │   ├── pages/        # Route-level page components
        │   └── services/     # API service layer
        └── index.html
```

---

## 🛠️ Tech Stack

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Node.js | ≥ 18.0.0 | Runtime |
| Express | ^5.2.1 | REST API framework |
| MongoDB + Mongoose | ^9.9.4 | Database & ODM |
| bcryptjs | ^3.0.3 | Password hashing |
| jsonwebtoken | ^9.0.3 | JWT authentication |
| dotenv | ^17.4.2 | Environment config |
| nodemon | ^3.1.14 | Dev auto-restart |

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| React | ^19.2.8 | UI framework |
| React Router DOM | ^7.18.3 | Client-side routing |
| Tailwind CSS | ^4.3.3 | Utility-first styling |
| Vite | ^8.2.2 | Build tool & dev server |
| oxlint | ^1.79.0 | Fast JS/JSX linter |

### External Services
| Service | Purpose |
|---|---|
| **MongoDB Atlas** | Cloud-hosted database |
| **Python FastAPI AI Engine** | Multi-agent problem analysis (separate service) |
| **Railway** | Backend deployment |
| **Vercel** | Frontend deployment |

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) **v18 or higher**
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- A [MongoDB Atlas](https://www.mongodb.com/atlas) cluster (free tier works)
- *(Optional)* Python FastAPI AI service running locally on port `8000`

---

### 1. Clone the Repository

```bash
git clone https://github.com/charlierx07/SetuX.git
cd SetuX
```

---

### 2. Backend Setup

```bash
cd backend
```

**Install dependencies:**
```bash
npm install
```

**Configure environment variables:**
```bash
cp .env.example .env
```

Edit `.env` and fill in your values:

```env
# MongoDB Atlas connection string
MONGODB_URI=mongodb+srv://USER:PASSWORD@cluster0.xxxxx.mongodb.net/societal_innovation?retryWrites=true&w=majority

# JWT secret key (use a long random string in production)
JWT_SECRET=your_super_secret_jwt_key_here

# Gmail SMTP (for email notifications)
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_16_char_gmail_app_password

# URL to the Python AI engine
AI_SERVICE_URL=http://localhost:8000

# Port for the backend server
PORT=5000
```

**Start the backend:**

```bash
# Development (auto-restart on changes)
npm run dev

# Production
npm start
```

The backend will be available at **`http://localhost:5000`**.

---

### 3. Frontend Setup

```bash
cd frontend/setux-frontend
```

**Install dependencies:**
```bash
npm install
```

**Start the development server:**
```bash
npm run dev
```

The frontend will be available at **`http://localhost:5173`**.

---

## 📡 API Reference

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/auth/signup` | Register a new citizen account | ❌ |
| `POST` | `/auth/login` | Login (citizen or admin) | ❌ |
| `POST` | `/auth/admin-login` | Dedicated admin portal login | ❌ |

#### `POST /auth/signup`
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword"
}
```

#### `POST /auth/login`
```json
{
  "email": "john@example.com",
  "password": "securepassword"
}
```

---

### Problem Endpoints

> All problem endpoints require a `Bearer <token>` in the `Authorization` header.

| Method | Endpoint | Description | Role |
|---|---|---|---|
| `POST` | `/problems/` | Submit a new problem | User |
| `GET` | `/problems/my-problems` | Get your own submitted problems | User |
| `GET` | `/problems/all` | Get all problems | Admin |
| `GET` | `/problems/:id` | Get a single problem by ID | User / Admin |

#### `POST /problems/`
```json
{
  "title": "Waterlogging near Main Street",
  "description": "The road floods every time it rains, causing accidents.",
  "address": "Main Street, Mumbai, Maharashtra",
  "latitude": 19.076,
  "longitude": 72.877,
  "images": [],
  "videos": [],
  "documents": []
}
```

**Response includes:**
- Problem record saved to MongoDB
- `ai_analysis` — domain, category, priority, and summary from the AI engine
- `university_discovery` — top matched universities
- `duplicate_check` — whether a similar problem was already filed

---

## 🖥️ Frontend Pages

| Route | Page | Description |
|---|---|---|
| `/` | `Home` | Landing page with hero, how-it-works & portal access |
| `/signup` | `SignUp` | New citizen account registration |
| `/login` | `Login` | Citizen login |
| `/dashboard` | `Dashboard` | Citizen's submitted problems overview |
| `/report-problem` | `ReportProblem` | Problem submission form |
| `/problem/:id` | `ProblemDetails` | Detailed view of a single problem with AI analysis |
| `/problem/:id/universities` | `UniversityMatches` | University recommendations for a problem |
| `/problem/:id/industries` | `IndustryMatches` | Industry match results for a problem |
| `/admin/login` | `AdminLogin` | Admin-only login portal |
| `/admin` | `AdminDashboard` | Admin review dashboard |

---

## 👤 User Roles

### Citizen (User)
- Register & log in
- Submit problems with location and media
- View their own submitted problems and AI analysis results
- Browse university and industry matches for their submissions

### Admin
- Access the dedicated admin portal
- View **all** submitted problems across the platform
- Review AI analysis and recommendations
- Approve or reject problems

**Default Admin Credentials (development only):**
```
Username : csmuadmin
Password : admin1234
```

> ⚠️ **Change admin credentials before deploying to production.**

---

## 🌍 Deployment

### Backend — Railway

The backend includes a [`railway.json`](./backend/railway.json) for zero-config Railway deployments:

```json
{
  "build": { "builder": "NIXPACKS" },
  "deploy": {
    "startCommand": "node server.js",
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 3
  }
}
```

Set all environment variables from `.env.example` in your Railway project settings.

### Frontend — Vercel

The frontend includes a [`vercel.json`](./frontend/setux-frontend/vercel.json) for SPA routing support. Simply connect your GitHub repo to Vercel and set the root directory to `frontend/setux-frontend`.

**Build settings:**
```
Build Command : npm run build
Output Dir    : dist
```

---

## 📁 Key Files

| File | Description |
|---|---|
| [`backend/server.js`](./backend/server.js) | Express app entry point |
| [`backend/config/db.js`](./backend/config/db.js) | MongoDB connection setup |
| [`backend/models/problem.model.js`](./backend/models/problem.model.js) | Problem schema (with AI fields) |
| [`backend/models/user.model.js`](./backend/models/user.model.js) | User schema (citizen / admin) |
| [`backend/controllers/problem.controller.js`](./backend/controllers/problem.controller.js) | Problem CRUD + AI integration |
| [`backend/controllers/auth.controller.js`](./backend/controllers/auth.controller.js) | Signup / Login / Admin auth |
| [`frontend/setux-frontend/src/App.jsx`](./frontend/setux-frontend/src/App.jsx) | React router configuration |
| [`backend/.env.example`](./backend/.env.example) | Environment variable template |

---

## 🔒 Security Notes

- Passwords are hashed with **bcryptjs** (salt rounds: 10)
- JWT tokens expire in **7 days**
- The `.env` file is listed in `.gitignore` — never commit secrets
- CORS is enabled globally (configure allowed origins for production)

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "feat: add my feature"`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**.

---

<div align="center">

Made with ❤️ by the **SetuX Team**

*Bridging problems to solutions, one submission at a time.*

</div>
