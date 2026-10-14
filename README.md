# Student Project Tracker

A full-stack web application designed to track electronics workshop and engineering project ideas. Built step-by-step through the WebDev Certification program.

## Architecture & Data Flow

```text
Browser (UI) <---> fetch (/api/projects) <---> Express (app.js) <---> SQLite (node:sqlite)
[HTML / CSS / JS]         [JSON REST API]        [Validation & Routing]     [data/projects.db]
```

- **Frontend**: Semantic HTML5 ([public/index.html](public/index.html)), CSS3 responsive design ([public/style.css](public/style.css)), and asynchronous DOM manipulation ([public/script.js](public/script.js)).
- **Backend**: Express 5 HTTP REST API ([app.js](app.js)) with strict input validation and centralized error handling, launched by [server.js](server.js).
- **Persistence**: Embedded SQLite database ([database.js](database.js)) using Node 22 native `node:sqlite` (`DatabaseSync`), parameterized queries to prevent SQL injection, and schema constraints.
- **Testing**: Automated end-to-end integration and smoke tests ([test/crud.test.js](test/crud.test.js)) testing CRUD, validation, API errors, and persistence across server restarts.

## Prerequisites

- Node.js >= 22.18.0 (Node 22 LTS recommended)
- npm

## How to Run

1. **Install dependencies**:
   ```bash
   npm ci
   ```

2. **Run automated test suite**:
   ```bash
   npm test
   ```
   *Result*: 100% passing across CRUD, validation bounds (1-80 chars, allowed statuses), server restart persistence, and 400/404 error branches.

3. **Start the local server**:
   ```bash
   npm start
   ```

4. **Access the application**:
   Open [http://localhost:3000](http://localhost:3000) in your web browser.

## Verified Behavior & Evidence

- **Persistence**: Project entries are persisted to `data/projects.db` and survive server restarts and browser refreshes.
- **Validation**:
  - `name`: Required, trimmed, between 1 and 80 characters.
  - `status`: Strictly constrained to `Planned`, `In Progress`, or `Completed`.
  - Rejection of malformed JSON or payload sizes exceeding 10KB.
- **Safety**: SQL statements use parameterized queries (`?`), preventing SQL injection. `data/`, `node_modules/`, and `.env` files are excluded from Git tracking via `.gitignore`.
