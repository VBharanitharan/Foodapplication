# FoodApp — GitHub + Vercel deployment

This repository contains a Vite/React frontend (`frontend/`) and an Express/MongoDB backend (`backend/`).

## Important security note
The original archive contained live-looking database, JWT, Cloudinary, Stripe, email, and Groq credentials. They have been removed from this cleaned copy. **Rotate/revoke those credentials now** in their respective dashboards, especially the MongoDB database password, JWT secret, Cloudinary API secret, Stripe test secret, and Groq key. Do not reuse the credentials from the original archive.

## Deploy the backend (Render recommended)
The Express app is a long-running server, so deploy `backend/` as a Node web service (for example, on Render):
1. Push this repository to GitHub.
2. Create a Web Service and set **Root Directory** to `backend`.
3. Build command: `npm install`
4. Start command: `npm start`
5. Add the environment variables from `backend/.env.example` in the hosting dashboard. Use your rotated MongoDB URI for `DB_URI`.
6. Set `FRONTEND_URL` to your deployed Vercel frontend origin (for example `https://your-app.vercel.app`). Multiple origins can be comma-separated.
7. Confirm the backend responds at `/api/v1/...` endpoints. The app currently has no dedicated health endpoint.

## Deploy the frontend (Vercel)
1. Import the GitHub repository into Vercel.
2. Set **Root Directory** to `frontend`.
3. Framework preset: **Vite**.
4. Build command: `npm run build`
5. Output directory: `dist`
6. Add environment variable `VITE_API_URL` with the backend base URL, without a trailing slash (for example `https://your-backend.onrender.com`).
7. Redeploy after setting the environment variable.

## Run locally
1. Copy `backend/.env.example` to `backend/.env` and fill in real development credentials.
2. In a terminal: `cd backend && npm install && npm run dev`
3. In another terminal: `cd frontend && npm install`, copy `.env.example` to `.env`, then run `npm run dev`.
4. Open the Vite URL shown in the terminal.

## Notes
- The frontend Vite proxy forwards `/api` to `http://localhost:8080` during local development.
- Production API requests use `VITE_API_URL`.
- Payment, email, Cloudinary uploads, and AI routes require valid provider credentials; configure only the services you intend to use.
- Do not commit `.env` files or production secrets.
