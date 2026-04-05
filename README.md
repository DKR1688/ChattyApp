# ChattyApp

Full-stack chat application with:
- `frontend`: React + Vite
- `backend`: Node.js + Express + Socket.IO + MongoDB

## Prerequisites

- Node.js 18+ (Node 22 works)
- npm
- MongoDB running locally on `127.0.0.1:27017`

## Backend Environment

Create `backend/.env` (or copy from `backend/.env.example`):

```env
PORT=5001
NODE_ENV=development
MONGODB_URI=mongodb://127.0.0.1:27017/chat_app
JWT_SECRET=change_this_local_dev_secret
CLIENT_URL=http://localhost:5173
CLIENT_URLS=http://localhost:5173
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
SERVE_FRONTEND=false
```

Create `frontend/.env` (or copy from `frontend/.env.example`):

```env
VITE_API_URL=http://localhost:5001/api
VITE_SOCKET_URL=http://localhost:5001
```

## Install Dependencies

From project root:

```bash
npm install --prefix backend
npm install --prefix frontend
```

## Run Locally

Open 2 terminals.

1. Start backend:

```bash
npm run start --prefix backend
```

2. Start frontend:

```bash
npm run dev --prefix frontend
```

## App URLs

- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:5001/api`

## Common Fix (Port 5001 Busy)

If backend shows `EADDRINUSE: 5001`, run in PowerShell:

```powershell
$pid = (netstat -ano | findstr :5001 | findstr LISTENING | ForEach-Object { ($_ -split '\s+')[-1] } | Select-Object -First 1)
if ($pid) { taskkill /PID $pid /F }
```

## Deploy On Render (Frontend + Backend)

Deploy as 2 services from the same repository:

1. Backend: **Web Service**
- Root Directory: `backend`
- Build Command: `npm install`
- Start Command: `npm run start`
- Environment Variables:
  - `NODE_ENV=production`
  - `PORT=10000` (or leave blank and let Render provide `PORT`)
  - `MONGODB_URI=...`
  - `JWT_SECRET=...`
  - `CLIENT_URL=https://<your-frontend>.onrender.com`
  - `CLIENT_URLS=https://<your-frontend>.onrender.com`
  - `CLOUDINARY_CLOUD_NAME=...`
  - `CLOUDINARY_API_KEY=...`
  - `CLOUDINARY_API_SECRET=...`
  - `SERVE_FRONTEND=false`

2. Frontend: **Static Site**
- Root Directory: `frontend`
- Build Command: `npm install && npm run build`
- Publish Directory: `dist`
- Environment Variables:
  - `VITE_API_URL=https://<your-backend>.onrender.com/api`
  - `VITE_SOCKET_URL=https://<your-backend>.onrender.com`

After frontend gets its final URL, update backend `CLIENT_URL`/`CLIENT_URLS` with that exact URL and redeploy backend once.
