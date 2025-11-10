# Sentinel Security Dashboard

**Sentinel** is a student project exploring what a modern security monitoring console for an online game could look like.  
It is built with **Vite**, **React**, and **TypeScript**, and connects to a simulated security API (or a mock layer when offline).  
The goal is to learn how to design responsive dashboards, manage real-time data, and handle alert streams efficiently.

---

## 🚀 Getting Started

| Command | Description |
| --- | --- |
| `npm install` | Install dependencies (Node.js 20+) |
| `npm run dev` | Start the local dev server (default: `http://localhost:5173`) |
| `npm run build` | Type-check and build for production |
| `npm run preview` | Preview the production build locally |
| `npm test` | Run unit tests (Vitest + React Testing Library) |

You can configure environment variables such as the API URL or WebSocket URL in a `.env` file.  
If the backend is unreachable, the React Query hooks automatically fall back to **mock responses** so the UI remains functional.

---

## 🧭 Features

- **Dashboard Overview** – Key indicators, risk distribution, alert trends.  
- **Alert Stream** – Real-time WebSocket feed with filters and notifications.  
- **Player Profiles** – Search, risk insights, and detailed activity history.  
- **Analytics Section** – System performance and anomaly visualization.  
- **Light/Dark Mode** – Built into the theme provider.  
- **Offline Support** – Service worker and fallback page included.

---

## 🧩 Tech Stack

- **Framework:** React 18, React Router, Vite  
- **Data & State:** Axios, React Query 5, Suspense, custom WebSocket hook  
- **UI:** Material UI 6, Recharts, Notistack  
- **Tooling:** TypeScript (strict), ESLint 9, Prettier, Vitest, Storybook-ready  
- **Deployment:** Multi-stage Dockerfile + Nginx (see `docker/`)

security-dashboard/
├── public/ # Manifest, service worker, static assets
├── src/
│ ├── components/ # Layouts, charts, widgets, cards
│ ├── hooks/ # React Query hooks, WebSocket, local storage
│ ├── pages/ # Dashboard, Alerts, Players, Analytics
│ ├── services/ # API client, auth helpers
│ ├── styles/ # Theme and global styles
│ ├── types/ # Shared TypeScript models
│ └── utils/ # Constants, formatters, helpers
├── tests/ # Vitest setup and sample tests
├── docker/ # Dockerfile + Nginx configuration
└── README.md


---

## 🔗 API Contracts & Mock Fallback

| Endpoint | Purpose |
| --- | --- |
| `GET /api/security/dashboard` | Returns KPIs, anomaly data, and recent alerts |
| `GET /api/security/player-risk/:id` | Fetches detailed player risk profile |
| `GET /api/players/suspicious` | Lists players flagged for review |
| WebSocket (`VITE_WS_URL`) | Pushes alerts in real time |

Each API call is wrapped with a helper called `withMockFallback`, which provides curated mock data when the backend is down.  
This ensures demos and tests continue working smoothly.

---

## 🐳 Docker Support

docker build -t sentinel-dashboard -f docker/Dockerfile .
docker run -p 8080:80 --env-file .env sentinel-dashboard


The image builds the React app and serves it via Nginx.  
You can map `/api` to your own backend using the provided proxy configuration.

---

---

**Note:** This is a **student learning project**, created to practice modern front-end development concepts like real-time communication, state management, and UI design.  
Feel free to fork, improve, and adapt it to your own learning goals.  
