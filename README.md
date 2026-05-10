# NoBunk Frontend

Frontend for NoBunk, built with plain HTML, CSS, and Vanilla JavaScript.

## Files

- `index.html`: Main dashboard page.
- `onboarding.html`: User onboarding flow.

## Architecture

- No framework and no build step.
- Styling and app logic are mostly inline in each HTML file.
- User identity is passed through URL query parameters and persisted in `localStorage`.
- Frontend calls backend APIs directly with `fetch`.

## Backend Dependency

The frontend expects a running backend that exposes auth, onboarding, dashboard, and AI verdict APIs.

Current API base URL in code points to:

- `https://attendease-backend-wrag.onrender.com`

For local development, replace the `API` constant in both HTML files with your local backend URL (for example `http://localhost:8000`).

## User Flow

1. User lands on app and triggers Google login.
2. Backend callback redirects user to either:
   - `onboarding.html` when `onboarded` is false
   - `index.html` when `onboarded` is true
3. Onboarding collects section/batch and attendance baseline.
4. Dashboard displays attendance metrics and AI guidance.

## Running Locally

Since this is static HTML, you can:

- open files directly in browser, or
- serve this folder via any static server.

Example using Python:

```bash
cd attendease-frontend
python -m http.server 3000
```

Then open `http://localhost:3000/index.html`.

## Common Gotchas

- If dashboard appears empty, verify `user_id` is present in query string or `localStorage`.
- If redirects keep sending users to onboarding, verify backend is setting `onboarded` correctly.
- If backend CORS blocks requests in local setup, update allowed origins in backend config.
