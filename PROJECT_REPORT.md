# PROJECT REPORT
## TIMEFLOW — FREELANCE TIME TRACKING TOOL

**Project type:** Full Stack Web Application  
**Technology:** MongoDB, Express.js, React.js, Node.js (MERN)  
**Submitted by:** __________________________  
**Roll No.:** ______________________________  
**Course / Semester:** _____________________  
**Submitted to:** __________________________  
**College:** _______________________________

---

## Certificate

This is to certify that the project entitled **“TimeFlow — Freelance Time Tracking Tool”** is submitted by __________________ in partial fulfillment of the requirements of the course __________________. The work has been completed under the guidance of __________________.

**Guide signature:** _______________  **Date:** _______________

## Declaration

I declare that this project report titled “TimeFlow — Freelance Time Tracking Tool” is my academic work. The application has been developed for learning and demonstration purposes using the MERN stack. Any external libraries used are acknowledged in the project dependencies.

**Student signature:** _______________  **Date:** _______________

## Acknowledgement

I express my sincere gratitude to my project guide and faculty members for their guidance and support. I also thank my institution, friends and family for their encouragement during the development of this project.

## Abstract

TimeFlow is a web-based freelance time tracking application designed to help independent professionals record the time spent on client projects and understand their work patterns. Users can create an account, maintain projects with hourly rates, start and stop work timers, review completed sessions in a timesheet and view productivity reports. The system calculates estimated billable earnings from recorded duration and the hourly rate assigned to each project. The application uses React for the user interface, Express and Node.js for REST APIs, and MongoDB for persistent data storage. JWT-based authentication protects user-specific operations. The goal is to provide a simple, centralized and responsive tool for time management and work estimation.

## 1. Introduction

Freelancers often work on multiple assignments and need to know how much time is spent on each client project. Manually recording work hours can lead to incomplete records and inaccurate estimates. TimeFlow addresses this problem through a centralized application that connects time entries to projects and rates. It gives users a dashboard for a quick overview and reports for reviewing productivity.

## 2. Problem Statement

Maintaining work logs manually is inconvenient, especially when a freelancer handles several projects. A user may forget start/end times, lose track of total hours, or find it difficult to estimate the value of completed work. A digital system is needed to organize projects, record sessions and calculate estimated earnings consistently.

## 3. Objectives

1. Provide secure user registration and login.
2. Allow users to create and manage freelance projects.
3. Record working time through a start/stop timer.
4. Store completed sessions in a timesheet.
5. Estimate billable earnings using project hourly rates.
6. Present useful productivity summaries and charts.
7. Provide a responsive interface for different screen sizes.

## 4. Scope

The application supports individual user accounts, project organization, timer-based time entries, timesheet review, estimated earnings and basic productivity reporting. The current academic version does not process payments, generate tax invoices, or provide team collaboration.

## 5. Technology Description

- **MongoDB:** NoSQL database for storing user, project and time-entry documents.
- **Express.js:** Backend framework for REST API routing and middleware.
- **React.js:** Component-based frontend for interactive pages.
- **Node.js:** JavaScript runtime for backend execution.
- **Mongoose:** Object data modeling and schema validation for MongoDB.
- **JWT:** Authentication tokens for protected API requests.
- **bcryptjs:** Password hashing before database storage.
- **Recharts:** Data visualization for activity reports.

## 6. System Requirements

**Hardware:** Dual-core processor or better, 4 GB RAM minimum (8 GB recommended), and sufficient disk space for Node.js and MongoDB.

**Software:** Windows, Linux or macOS; Node.js 18+; npm; MongoDB Community Server or MongoDB Atlas; modern browser; code editor such as Visual Studio Code.

## 7. System Modules

### 7.1 Authentication
A user can register with a name, email and password or sign in with existing credentials. Passwords are hashed using bcryptjs. The backend issues a JWT after successful authentication.

### 7.2 Project Management
Users can add projects with a project name, client, description, hourly rate and display color. Project records are associated with their owner.

### 7.3 Time Tracking
A user selects an active project and starts a timer. The backend stores the start timestamp. When the user stops the timer, the backend records the end timestamp and calculates duration in seconds. One active timer is permitted per user.

### 7.4 Timesheet
Completed sessions are listed with project, description, date, start time, end time, duration and estimated earnings. Users can remove completed entries.

### 7.5 Reports and Dashboard
The dashboard summarizes total time, today's hours, estimated earnings and active projects. Reports show recent daily activity and a project-wise time breakdown.

### 7.6 Settings
Users can update their display name and default hourly rate. The email is displayed as a read-only account identifier.

## 8. System Architecture

The React client sends HTTP requests to the Express API using Axios. Protected routes attach a JWT in the Authorization header. Authentication middleware verifies the token and identifies the user. Controllers validate requests and use Mongoose models to read or update MongoDB. API responses are returned as JSON and displayed by React components.

```text
+---------------------------+
|       React Client        |
| Dashboard / Timer / UI    |
+-------------+-------------+
              | HTTP + JWT
              v
+---------------------------+
|     Express REST API      |
| Routes / Controllers      |
| JWT Authentication       |
+-------------+-------------+
              | Mongoose
              v
+---------------------------+
|         MongoDB           |
| Users / Projects / Time   |
+---------------------------+
```

## 9. Database Design

### Users
- `_id`: unique user identifier
- `name`: user's display name
- `email`: unique email address
- `password`: bcrypt password hash
- `hourlyRate`: default hourly rate
- `createdAt`, `updatedAt`: timestamps

### Projects
- `_id`: unique project identifier
- `user`: reference to owner
- `name`: project name
- `client`: client or organization name
- `description`: project details
- `hourlyRate`: project-specific rate
- `color`: UI color
- `status`: active, completed or archived

### Time Entries
- `_id`: unique entry identifier
- `user`: reference to owner
- `project`: reference to project
- `description`: work performed
- `startTime`, `endTime`: session timestamps
- `duration`: total seconds
- `billable`: whether the work is billable

## 10. Main Algorithms

**Timer start:** Verify that the user has no running entry. Validate that the selected project belongs to the user and is active. Create an entry with the current server timestamp and a null end time.

**Timer stop:** Find the user's active entry, record the current server timestamp as the end time, and calculate duration as the difference between end and start timestamps in seconds.

**Estimated earnings:** `estimated earnings = (duration in seconds / 3600) × project hourly rate`.

## 11. Testing

| Test case | Expected result |
|---|---|
| Register with valid details | Account created and user signed in |
| Register with an invalid email | Validation error returned |
| Login with incorrect password | Access denied |
| Open protected endpoint without token | HTTP 401 response |
| Create a project with a name | Project saved for current user |
| Start timer with valid project | Active time entry created |
| Start a second timer while one is active | Request rejected |
| Stop active timer | End time and duration saved |
| View timesheet | Completed entries displayed |
| View reports | Activity and project charts displayed |

## 12. Installation and Execution

1. Install Node.js 18+ and MongoDB.
2. Extract the project ZIP and open its folder in a terminal.
3. Run `npm install` at the root.
4. Run `npm install --prefix server` and `npm install --prefix client`.
5. Copy `server/.env.example` to `server/.env` and configure the MongoDB URI and JWT secret.
6. Start MongoDB.
7. Run `npm run dev` from the project root.
8. Open `http://localhost:5173` and register a user.

## 13. Future Enhancements

- Export timesheets to CSV and PDF.
- Weekly targets, reminders and calendar integration.
- Invoice generation and payment-status tracking.
- Team workspaces, roles and collaboration.
- Password reset and email verification.
- Automated tests, audit logs and deployment monitoring.

## 14. Conclusion

TimeFlow demonstrates how the MERN stack can be used to develop a practical full-stack productivity application. It combines authentication, database operations, REST APIs, real-time timer interaction, project management and data visualization. The application provides a foundation that can be extended with invoicing, collaboration and advanced reporting features.

## References

1. MongoDB Documentation — https://www.mongodb.com/docs/
2. Express.js Documentation — https://expressjs.com/
3. React Documentation — https://react.dev/
4. Node.js Documentation — https://nodejs.org/docs/
5. Mongoose Documentation — https://mongoosejs.com/docs/
6. Recharts Documentation — https://recharts.org/
