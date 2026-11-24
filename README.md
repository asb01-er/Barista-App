# ☕ Barista Hub

A full-stack recipe manager for baristas. Visitors can browse coffee recipes; signed-in users can add, edit and delete their own.

**Live demo:** https://barista-app-1.onrender.com
**API:** https://barista-app.onrender.com

> The demo runs on a free Render server, so the first load can take up to 30 seconds while it wakes up.

## Features

- Sign up, log in and log out with cookie-based JWT authentication
- Browse all recipes on a public dashboard
- Add, edit and delete recipes (logged-in users only)
- Protected routes that redirect visitors to the login page
- Toast notifications for success and error messages

## Tech stack

| Layer    | Technology                                   |
| -------- | -------------------------------------------- |
| Frontend | React, React Router, Axios, React Toastify   |
| Backend  | Node.js, Express                             |
| Database | MongoDB with Mongoose                        |
| Auth     | JSON Web Tokens stored in httpOnly cookies   |
| Hosting  | Render (Web Service for the API, Static Site for the client) |

## Project structure

```
Barista-App/
├── client/
│   └── client/        # React app (Create React App)
└── server/            # Express API
    ├── Controllers/
    ├── Routes/
    └── index.js
```

## Getting started

### Prerequisites

- Node.js 18+
- A MongoDB database (local or MongoDB Atlas)

### 1. Clone the repository

```bash
git clone https://github.com/asb01-er/Barista-App.git
cd Barista-App
```

### 2. Run the server

```bash
cd server
npm install
```

Create `server/.env`:

```env
MONGO_URL=your_mongodb_connection_string
PORT=4000
CLIENT_URL=http://localhost:3000
NODE_ENV=development
# plus the JWT secret variable your auth code reads
```

Then start it:

```bash
npm start
```

### 3. Run the client

In a second terminal:

```bash
cd client/client
npm install
npm start
```

The app opens at http://localhost:3000 and talks to the API at `http://localhost:4000`.

To point the client at a different API, set `REACT_APP_API_URL` before starting or building.

## API overview

| Method | Endpoint        | Description                        | Auth |
| ------ | --------------- | ---------------------------------- | ---- |
| POST   | `/auth/signup`  | Create an account                  | No   |
| POST   | `/auth/login`   | Log in and set the auth cookie     | No   |
| POST   | `/auth/logout`  | Clear the auth cookie              | Yes  |
| GET    | `/auth/verify`  | Check the current user             | Yes  |
| GET    | `/recipes`      | List all recipes                   | No   |
| POST   | `/recipes`      | Create a recipe                    | Yes  |
| PUT    | `/recipes/:id`  | Update a recipe                    | Yes  |
| DELETE | `/recipes/:id`  | Delete a recipe                    | Yes  |

## Deployment notes

- **Server (Render Web Service):** root directory `server`, build `npm install`, start `npm start`. Set `MONGO_URL`, `CLIENT_URL` (no trailing slash), `NODE_ENV=production` and the JWT secret.
- **Client (Render Static Site):** root directory `client/client`, build `npm install && npm run build`, publish directory `build`. Set `REACT_APP_API_URL` to the API URL and add a rewrite from `/*` to `/index.html`.
- Because the client and API sit on different domains, cookies are set with `secure: true` and `sameSite: "none"` in production.

## Author

**Ernest Ekelem** — [GitHub](https://github.com/asb01-er) · [LinkedIn](https://www.linkedin.com/in/ernest-ekelem-5a771735a)
