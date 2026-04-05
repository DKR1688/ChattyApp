# ChattyApp

Full-stack chat application with:
- `frontend`: React + Vite
- `backend`: Node.js + Express + Socket.IO + MongoDB

## Prerequisites

- Node.js 18+ (Node 22 works)
- npm
- MongoDB running locally on `127.0.0.1:27017`

## Backend Environment

Create `backend/.env`:

```env
PORT=5001
NODE_ENV=development
MONGODB_URI=mongodb://127.0.0.1:27017/chat_app
JWT_SECRET=change_this_local_dev_secret
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
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
