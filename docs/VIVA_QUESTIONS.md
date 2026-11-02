# TimeFlow — Viva Preparation

1. **What is the MERN stack?** MongoDB, Express.js, React.js and Node.js. MongoDB stores data, Express and Node implement backend APIs, and React builds the frontend.
2. **Why did you choose MongoDB?** It stores JSON-like documents and works naturally with JavaScript objects and Mongoose.
3. **What is a REST API?** An HTTP interface that exposes resources through methods such as GET, POST, PATCH and DELETE.
4. **What is JWT?** A signed token used to prove authentication on later requests. The client sends it in the Authorization header.
5. **Why hash passwords?** A password hash prevents the original password from being stored as plain text. This project uses bcryptjs.
6. **What is middleware in Express?** A function that runs during the request-response cycle. The authentication middleware verifies JWTs before protected routes.
7. **What is Mongoose?** An ODM library that defines schemas and provides model methods to interact with MongoDB.
8. **How is duration calculated?** The server subtracts the start timestamp from the end timestamp and stores the difference in seconds.
9. **How are earnings calculated?** Duration in seconds is divided by 3,600 and multiplied by the project's hourly rate.
10. **How does React update the interface?** Components use state and effects; when state changes, React re-renders the relevant UI.
11. **What is the purpose of Axios?** It sends HTTP requests from the React client to the backend API.
12. **What is the difference between PUT and PATCH?** PUT generally replaces a resource, while PATCH applies a partial update. The project uses PATCH for partial updates.
13. **What is a protected route?** An endpoint that requires a valid authentication token before returning private data.
14. **What are the main collections?** Users, projects and time entries.
15. **What are future improvements?** CSV/PDF export, invoice generation, email verification, password reset, team collaboration and automated tests.
