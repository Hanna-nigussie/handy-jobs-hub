# 🛠️ Handy Jobs Hub

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-3.2.6+-0175C2?logo=dart&logoColor=white)](https://dart.dev)
[![NestJS](https://img.shields.io/badge/NestJS-10.x-E0234E?logo=nestjs&logoColor=white)](https://nestjs.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Prisma](https://img.shields.io/badge/Prisma-5.10-2D3748?logo=prisma&logoColor=white)](https://www.prisma.io)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13+-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![State Management](https://img.shields.io/badge/State%20Management-BLoC-blue)](https://bloclibrary.dev)

> A modern, full-stack mobile platform connecting job seekers and employers for handy and skilled services. Built with a robust **NestJS + Prisma** backend and a responsive **Flutter (BLoC)** cross-platform mobile client.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Architecture & Tech Stack](#-architecture--tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [1. Backend Setup](#1-backend-setup)
  - [2. Frontend Setup](#2-frontend-setup)
- [Environment Variables](#-environment-variables)
- [Testing](#-testing)
- [API Reference](#-api-reference)
- [Admin Portal & Security](#-admin-portal--security)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📖 Overview

**Handy Jobs Hub** bridges the gap between employers seeking handy labor/skilled workers and job seekers searching for local and specialized job vacancies. The platform incorporates role-based access control, secure JWT-based authentication, a comprehensive job posting and application workflow, and an integrated feedback/review mechanism to promote trust and accountability.

---

## ✨ Key Features

- **🔐 Authentication & Role-Based Authorization**
  - Secure registration and sign-in with JWT authentication.
  - Granular role-based access control (**`USER`** and **`ADMIN`** roles).
  - Password hashing utilizing Argon2 / Bcrypt.

- **👥 Dual User Types (Employers & Job Seekers)**
  - **Employers (`EMPLOYEE`):** Post job openings, manage listings, specify required skills and salary, and review applicants.
  - **Job Seekers (`JOB_SEEKER`):** Browse listings, upload and manage CV profiles, and connect directly with hiring employers.

- **💼 Job Management (CRUD)**
  - Create, read, update, and delete job postings.
  - Detailed job specifications: title, description, salary, contact phone number, and author attribution.
  - Filter listings specifically tailored for job seekers or employers.

- **⭐ Feedback & Evaluation System**
  - Transparent review system with numerical ratings (1-5) and written feedback.
  - Contributors can view, edit, or delete their submitted reviews.
  - Public visibility into reviews to help users make informed decisions.

- **🛡️ Admin Governance & Controls**
  - Platform-wide administration with capabilities to oversee all job postings and users.
  - Toggle user account status (blocking / unblocking) to enforce community guidelines.
  - Gated admin registration protected by a security passkey.

---

## 🏗️ Architecture & Tech Stack

### 📱 Frontend (`mobilefrontend`)
- **Framework:** [Flutter](https://flutter.dev) (Dart SDK `>=3.2.6 <4.0.0`)
- **State Management:** [BLoC Pattern](https://bloclibrary.dev) (`flutter_bloc`, `equatable`)
- **Routing:** [GoRouter](https://pub.dev/packages/go_router)
- **Networking:** [Dio](https://pub.dev/packages/dio) & [HTTP](https://pub.dev/packages/http)
- **Storage:** [SharedPreferences](https://pub.dev/packages/shared_preferences)
- **UI Components:** [Curved Navigation Bar](https://pub.dev/packages/curved_navigation_bar), Cupertino Icons
- **Testing:** `bloc_test`, `mocktail`, `mockito`

### 🖥️ Backend (`mobilebackend`)
- **Framework:** [NestJS](https://nestjs.com) (Node.js framework with Express)
- **Language:** TypeScript
- **Database & ORM:** [PostgreSQL](https://www.postgresql.org/) & [Prisma ORM](https://www.prisma.io/)
- **Security:** Passport JWT (`@nestjs/passport`, `passport-jwt`), Argon2, Bcrypt, Class-Validator
- **Containerization:** Docker & Docker Compose

---

## 📂 Project Structure

```text
handy-jobs-hub/
└── handy-jobs-hub-bloc/
    ├── mobilebackend/                  # NestJS REST API server
    │   ├── prisma/
    │   │   └── schema.prisma           # Prisma database schema & models
    │   ├── src/
    │   │   ├── auth/                   # Authentication (JWT, signin, signup, guards)
    │   │   ├── job/                    # Job postings & management module
    │   │   ├── review/                 # Review & rating system module
    │   │   ├── user/                   # User profile & admin control module
    │   │   ├── prisma/                 # Prisma service & module
    │   │   ├── app.module.ts           # Root application module
    │   │   └── main.ts                 # Server entry point
    │   ├── test/                       # E2E test suites
    │   ├── docker-compose.yml          # PostgreSQL database container setup
    │   ├── package.json
    │   └── tsconfig.json
    │
    └── mobilefrontend/                 # Flutter mobile client
        ├── lib/
        │   ├── auth/                   # Auth BLoC, repositories, data providers & views
        │   ├── job/                    # Job BLoC, repositories, data providers & views
        │   ├── review/                 # Review BLoC, repositories, data providers & views
        │   ├── user/                   # User profile, admin views & layout navigation
        │   └── main.dart               # App initialization, routing & providers
        ├── test/
        │   ├── unit/                   # BLoC, repository & data provider unit tests
        │   └── widget/                 # Flutter widget test suites
        └── pubspec.yaml                # Flutter dependencies & assets
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed on your machine:
- [Node.js](https://nodejs.org/) (v18.x or later) & [Yarn](https://yarnpkg.com/) (or `npm`)
- [Flutter SDK](https://docs.flutter.dev/get-started/install) (v3.2.x or later)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (for local database) or a local PostgreSQL instance

---

### 1. Backend Setup

1. **Navigate to the backend directory:**
   ```bash
   cd handy-jobs-hub-bloc/mobilebackend
   ```

2. **Install dependencies:**
   ```bash
   yarn install
   ```

3. **Start the PostgreSQL database:**
   ```bash
   docker-compose up -d
   ```
   *This starts PostgreSQL 13 on port `5432`.*

4. **Configure environment variables:**
   Verify or create your `.env` file in `mobilebackend/`:
   ```env
   DATABASE_URL="postgresql://postgres:123@localhost:5432/nest?schema=public"
   JWT_SECRET="password123"
   ```

5. **Run database migrations and generate Prisma client:**
   ```bash
   npx prisma migrate dev --name init
   npx prisma generate
   ```

6. **Start the backend development server:**
   ```bash
   yarn run start:dev
   ```
   *The server runs by default on `http://localhost:3000`.*

---

### 2. Frontend Setup

1. **Navigate to the frontend directory:**
   ```bash
   cd handy-jobs-hub-bloc/mobilefrontend
   ```

2. **Install Flutter packages:**
   ```bash
   flutter pub get
   ```

3. **Configure the API endpoint (if necessary):**
   - By default, the application connects to `http://localhost:3000`.
   - **Android Emulator:** Replace `localhost` with `10.0.2.2` in `lib/**/data_provider/` files.
   - **Physical Device:** Replace `localhost` with your machine's local LAN IP (e.g. `192.168.x.x`).

4. **Run the Flutter application:**
   ```bash
   flutter run
   ```

---

## ⚙️ Environment Variables

### Backend (`mobilebackend/.env`)

| Variable | Description | Default / Example |
| :--- | :--- | :--- |
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://postgres:123@localhost:5432/nest?schema=public` |
| `JWT_SECRET` | Secret key for signing JSON Web Tokens | `password123` |

---

## 🧪 Testing

### Backend Tests
Execute unit and end-to-end test suites using Jest:
```bash
# Run unit tests
yarn run test

# Run tests in watch mode
yarn run test:watch

# Run end-to-end tests
yarn run test:e2e

# Generate test coverage report
yarn run test:cov
```

### Frontend Tests
Execute Flutter unit and widget tests:
```bash
# Run all tests
flutter test

# Run unit tests only
flutter test test/unit/

# Run widget tests only
flutter test test/widget/
```

---

## 📡 API Reference

### Authentication (`/auth`)
- `POST /auth/signup` - Register a new user or administrator
- `POST /auth/signin` - Authenticate and retrieve JWT token
- `GET /auth/profile` - Retrieve authenticated user profile *(Requires JWT)*
- `POST /auth/logout` - Invalidate session

### Jobs (`/jobs`)
- `POST /jobs` - Create a new job vacancy *(Requires JWT)*
- `GET /jobs/forEmployees` - Fetch jobs targeted for employees / employers
- `GET /jobs/forJobSeekers` - Fetch jobs targeted for job seekers
- `GET /jobs/user-jobs/:userId` - Retrieve jobs posted by a specific user
- `PATCH /jobs/:id` - Update job listing details
- `DELETE /jobs/:id` - Delete a job posting
- `GET /jobs/getAllJobs` - Administrative view of all platform jobs *(Admin only)*

### Users (`/users`)
- `GET /users` - Retrieve all registered users *(Admin only)*
- `GET /users/profile/:userId` - View profile information for a user
- `PATCH /users/:id` - Update user profile information
- `DELETE /users/:id` - Delete user account
- `DELETE /users/:id/block` - Toggle block/unblock status for a user *(Admin only)*

### Reviews (`/review`)
- `POST /review` - Submit a new review for a job/user
- `GET /review/job/:jobId` - Fetch all reviews for a specific job
- `GET /review/user/:userId` - Fetch reviews written by or for a user
- `PATCH /review` - Update an existing review *(Author only)*
- `DELETE /review/:id` - Delete a review *(Author only)*

---

## 🔐 Admin Portal & Security

> [!IMPORTANT]
> **Admin Registration Security Passkey:**
> The secret password required to navigate to the Admin Registration page in the mobile application is:
> ```text
> 12345
> ```
> *Only authorized administrators should possess this key to maintain role integrity.*

---

## 🤝 Contributing

Contributions, feedback, and feature suggestions are welcome!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the [UNLICENSED / MIT License](LICENSE) - see repository details for more information.
