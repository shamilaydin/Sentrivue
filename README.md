# Sentrivue

Sentrivue is a Security Operations Center (SOC) dashboard that connects to a [Wazuh](https://wazuh.com/) deployment and turns its alerts, agents, and logs into a live, visual monitoring interface. It was built as a Holberton final project.

## Features

- **Overview** — real-time summary of agent health, alert volume, and severity breakdown.
- **Attack Map** — geolocates alert source IPs and renders them on an interactive 3D globe.
- **Incidents** — a triage view of Wazuh alerts grouped and ranked by severity.
- **Logs** — searchable, filterable stream of raw Wazuh Indexer events.
- **Settings** — configure and test the connection to the Wazuh Manager and Indexer.

## Tech stack

- [React 19](https://react.dev/) + [Vite](https://vitejs.dev/)
- [Tailwind CSS 4](https://tailwindcss.com/)
- [Framer Motion](https://www.framer.com/motion/) for animation
- [Recharts](https://recharts.org/) for charts
- [react-globe.gl](https://github.com/vasturiano/react-globe.gl) / [Three.js](https://threejs.org/) for the Attack Map globe
- [React Router](https://reactrouter.com/)
- Vercel serverless functions (`api/`) that proxy requests to the Wazuh Manager and Indexer APIs, keeping credentials off the client

## Project structure

```
src/
  pages/        Overview, Attack Map, Incidents, Logs, Settings
  components/    Shared UI components
  services/      Wazuh API client logic
  hooks/         Custom React hooks
  data/          Static/reference data
  utils/         Helper functions
api/
  wazuh.js       Proxy to the Wazuh Manager API
  indexer.js     Proxy to the Wazuh Indexer (OpenSearch) API
```

## Getting started

### Prerequisites

- Node.js 18+
- A reachable Wazuh Manager and Indexer (see [Wazuh's docs](https://documentation.wazuh.com/) for setup)

### Setup

```bash
npm install
cp .env.example .env.local
```

Edit `.env.local` with your Wazuh deployment's details:

```
WAZUH_URL=https://<wazuh-manager-host>:55000
WAZUH_INDEXER_URL=https://<wazuh-indexer-host>:9200
WAZUH_INDEXER_USER=<indexer-user>
WAZUH_INDEXER_PASSWORD=<indexer-password>
```

`.env.local` is git-ignored — these credentials never leave your machine and are never sent to the browser; the dev server proxy injects them server-side.

### Run

```bash
npm run dev
```

Then open the printed local URL in your browser.

### Other scripts

```bash
npm run build             # production build
npm run preview           # preview the production build
npm run lint               # lint the codebase
npm run check:wazuh-tls    # verify TLS connectivity to the Wazuh Indexer
```

## License

MIT — see [LICENSE](LICENSE).
