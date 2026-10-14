# Student Project Tracker

A hands-on web app development workshop project. It adds, displays, edits and deletes engineering projects, with data stored in local SQLite.

## Run locally
Use the workshop Node 22 baseline (at least 22.18, below 23), Git and VS Code.
Open a terminal inside the project, then run:

    npm ci
    npm start

Open http://localhost:3000. Stop the server with Ctrl+C.

## How it works
Browser HTML/CSS/JavaScript -> fetch/HTTP -> Express API -> SQLite -> JSON response -> updated page.
- `public/index.html`: page structure and form.
- `public/style.css`: appearance and responsive layout.
- `public/script.js`: input, API requests, rendering and feedback.
- `server.js`: starts the local server.
- `app.js`: routes, validation and responses.
- `database.js`: SQLite operations; creates `data/projects.db` locally.

## API
- `GET /api/health` - checks server status (`{"ok": true}`).
- `GET /api/projects` - lists all stored projects.
- `POST /api/projects` - validates and creates a new project.
- `PUT /api/projects/:id` - validates and updates an existing project.
- `DELETE /api/projects/:id` - deletes a project by ID.

## Verification
Actual checks performed:
- **Automated test suite**: Ran `npm test` (`node --test test/*.test.js`). 1/1 test suite passed verifying CRUD endpoints, boundary validation (1–80 chars, invalid status rejection), 400/404 error cases, and database persistence across server restart.
- **Manual CRUD lifecycle**: Created "IoT Monitor" with status "Planned", edited name and status to "Completed", and confirmed deletion with dialog prompt.
- **Persistence across server restart**: Created records, shut down the server process, restarted it, and verified records still persisted with intact IDs from `data/projects.db`.
- **Server downtime / error handling**: Attempted operations while server was stopped; verified the UI displays accessible error feedback without crashing.
- **Mobile responsiveness**: Verified with DevTools viewport at 390px; form controls, buttons, and card actions remain accessible without horizontal scroll.

## Workshop limitations
This local teaching app has no sign-in or per-user permissions. Browsers calling the same server share its collection. The SQLite data file and `node_modules` are not uploaded to GitHub. Cloud hosting requires separate server and database configuration.
