# TimeFlow — Freelance Time Tracking Tool

A full-stack MERN application for freelancers to organize projects, track work sessions, review timesheets and estimate billable earnings.

## Technology
- **Frontend:** React 18, Vite, React Router, Axios, Recharts, Lucide React, custom CSS
- **Backend:** Node.js, Express.js, JWT, bcryptjs, express-validator
- **Database:** MongoDB with Mongoose

## Features
- User registration and login with hashed passwords and JWT-protected APIs
- Personal dashboard with tracked hours, today's time, estimated earnings and active projects
- Start/stop timer linked to a project (one running timer per user)
- Project creation, listing and deletion with client, description and hourly rate
- Timesheet with session duration, start/end time and estimated earnings
- Productivity reports with 14-day chart and project breakdown
- Profile settings and default hourly rate
- Responsive dark interface

## Requirements
Install Node.js 18 or newer and MongoDB Community Server, or use a MongoDB Atlas connection string.

## Setup and run
1. Extract the ZIP and open a terminal in the `timeflow-mern` directory.
2. Install root tools:
   ```bash
   npm install
   ```
3. Install server dependencies:
   ```bash
   npm install --prefix server
   ```
4. Create `server/.env` by copying `server/.env.example`. Set `MONGO_URI` and replace `JWT_SECRET` with a long random secret.
5. Install frontend dependencies:
   ```bash
   npm install --prefix client
   ```
6. Make sure MongoDB is running locally (or use Atlas), then start both applications:
   ```bash
   npm run dev
   ```
7. Open **http://localhost:5173**. The API runs at **http://localhost:5000**.

### Run separately
```bash
npm run dev --prefix server
npm run dev --prefix client
```

## Environment variables
| Variable | Purpose | Example |
|---|---|---|
| PORT | API port | 5000 |
| MONGO_URI | MongoDB connection | mongodb://127.0.0.1:27017/timeflow |
| JWT_SECRET | Token signing secret | use-a-long-random-secret |
| CLIENT_URL | Allowed frontend origin | http://localhost:5173 |

## API overview
All protected routes require `Authorization: Bearer <token>`.

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| POST | `/api/auth/register` | Create account | No |
| POST | `/api/auth/login` | Login | No |
| GET | `/api/auth/me` | Current user | Yes |
| PATCH | `/api/auth/profile` | Update profile | Yes |
| GET | `/api/projects` | List projects | Yes |
| POST | `/api/projects` | Create project | Yes |
| PATCH | `/api/projects/:id` | Update project | Yes |
| DELETE | `/api/projects/:id` | Delete project | Yes |
| GET | `/api/time` | List time entries | Yes |
| GET | `/api/time/active` | Get active timer | Yes |
| POST | `/api/time/start` | Start timer | Yes |
| PATCH | `/api/time/:id/stop` | Stop timer | Yes |
| POST | `/api/time/manual` | Add manual entry | Yes |
| DELETE | `/api/time/:id` | Delete completed entry | Yes |
| GET | `/api/health` | API health check | No |

## Database collections
- **users:** name, email, password hash, default hourly rate
- **projects:** owner, project name, client, description, hourly rate, color, status
- **timeentries:** owner, project, description, start/end timestamps, duration in seconds, billable flag

## Calculation
For a completed time entry:
- Duration (seconds) = end timestamp − start timestamp
- Estimated earnings = (duration in seconds ÷ 3,600) × project's hourly rate

Earnings are estimates for demonstration and are not invoices or payments.

## Suggested college demonstration
1. Register a new account.
2. Add a project such as “Portfolio Website” with client “ABC Studio” and rate ₹600/hour.
3. Start the timer, work for a short interval, and stop it.
4. Open Timesheet to show the saved session and estimated earnings.
5. Open Reports to show the productivity charts.
6. Change the profile name or default hourly rate in Settings.

## Project structure
```text
timeflow-mern/
├── client/
│   ├── index.html
│   ├── package.json
│   └── src/
│       ├── components/   # Layout and protected route
│       ├── context/      # Authentication state
│       ├── pages/        # Login, dashboard, projects, timesheet, reports, settings
│       ├── api.js
│       ├── main.jsx
│       └── styles.css
├── server/
│   ├── src/
│   │   ├── config/       # MongoDB connection
│   │   ├── controllers/  # Business logic
│   │   ├── middleware/   # JWT authentication
│   │   ├── models/       # Mongoose schemas
│   │   ├── routes/       # REST endpoints
│   │   └── server.js
│   └── .env.example
└── README.md
```

## Notes / limitations
- This is a college-project starter, not a production-hardened SaaS. Add rate limiting, email verification, password reset, audit logging, stronger deployment security and automated tests before production use.
- The timer is server-recorded when started and stopped. If the browser closes, the running session remains active and can be stopped after logging back in.
- Deleting a project does not delete historical time entries; those records remain visible and may show the project as unavailable.
- No sample account is hard-coded. Register your own account in the app.
