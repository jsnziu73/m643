# مِعيار | اختبار القدرات العقلية

An Arabic, right-to-left mental-ability assessment for gifted schools. The assessment works without external AI or email accounts; those integrations are optional.

## Requirements

- Node.js 20.6 or newer
- npm

## Run locally

```sh
npm install
npm run dev
```

Open the Vite address printed in the terminal (normally http://localhost:5173). This starts both the Vite frontend and Node API; the API uses port 3001 locally. SQLite creates its database at `backend/data/results.sqlite` on first run.

`npm start` runs only the production API server, using Railway's `PORT` when provided and port 3001 otherwise. To run either process separately, use `npm run server` for the API and `npx vite --host 0.0.0.0` for the frontend in separate terminals.

## Railway deployment

Deploy the repository root as a Node.js service. Railway runs `npm start` automatically; the API listens on the assigned `PORT`. If the frontend is hosted on a separate domain, set `CORS_ORIGIN` on Railway to that exact origin (for example, `https://example.netlify.app`) and set `VITE_API_URL` in the frontend host to the Railway public URL, then rebuild the frontend. Multiple allowed frontend origins can be separated with commas.

## Optional integrations

Copy `backend/.env.example` to `backend/.env` and fill in the credentials:

- `GEMINI_API_KEY` enables personalized Arabic feedback through Gemini. If unset or unavailable, the app generates a local feedback summary from the skill scores.
- `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS`, and optionally `SMTP_SECURE` and `MAIL_FROM` enable result email. Until configured, results remain available on the result page and the app clearly indicates that email was not sent.

Keep `.env` private and do not commit real credentials. The assessment score is computed by the server; the answer key is not returned by the questions endpoint. This sample test is for learning and self-exploration, not an official IQ test or diagnosis.