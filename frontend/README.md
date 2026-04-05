# Frontend (React + Vite)

## Install

From project root:

```bash
npm install --prefix frontend
```

## Run

```bash
npm run dev --prefix frontend
```

Frontend runs at `http://localhost:5173`.

Set environment variables in `frontend/.env` (or copy `frontend/.env.example`):

```env
VITE_API_URL=http://localhost:5001/api
VITE_SOCKET_URL=http://localhost:5001
```

For full project setup (backend + frontend), see the root README:
- [../README.md](../README.md)
