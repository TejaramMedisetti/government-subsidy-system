# Frontend – React SPA

React 18 · Vite 5 · React Router 6 · Axios · Lucide icons

The full project documentation (workflow, roles, API reference, setup) is in the [root README](../README.md). This file covers the frontend only.

## Run

```bash
cp .env.example .env     # Windows: copy .env.example .env
npm install
npm run dev              # http://localhost:3000
```

The Spring Boot backend must be running (default `http://localhost:8080`).

| Script | Purpose |
| :--- | :--- |
| `npm run dev` | Dev server with hot reload on port 3000 |
| `npm run build` | Production build into `dist/` |
| `npm run preview` | Serve the production build locally |

## Environment variables

| Variable | Default | Purpose |
| :--- | :--- | :--- |
| `VITE_API_BASE_URL` | `http://localhost:8080` | Backend base URL |
| `VITE_ENABLE_DEMO_LOGIN` | `true` | One-click demo logins + role switcher. Set to `false` for public deployments; the demo credentials are then removed from the bundle |

## Structure

```
src/
├── components/   layout (header, sidebar, banner), common UI, tables, charts, workflow stepper
├── constants/    roles, application statuses, navigation per role
├── context/      AuthContext (session, login/logout), ToastContext
├── pages/        auth/  beneficiary/  officer/  admin/
├── routes/       AppRoutes, ProtectedRoute (role guards)
├── services/     api.js (Axios instance + interceptors) and one service per backend controller
└── utils/        formatters and storage helpers
```

## Notes

- The Axios instance attaches the JWT from `localStorage` and unwraps the backend's `ApiResponse` envelope. A `401` clears the session and redirects to `/login?expired=true`.
- Route guards only improve the UX; the backend enforces every permission.
- For a deployed build, either serve the SPA from the same origin as the API or restrict CORS on the backend to your frontend origin.
