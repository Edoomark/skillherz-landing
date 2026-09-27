# skillherz-landing

Cloudflare Worker (static assets) che serve le 4 landing page Skillherz sotto lo stesso sottodominio.

## Routing

- `landingpage.skillherz.com/imprese` → `imprese/index.html`
- `landingpage.skillherz.com/orientamento` → `orientamento/index.html`
- `landingpage.skillherz.com/studenti` → `studenti/index.html`
- `landingpage.skillherz.com/talentmatching` → `talentmatching/index.html`
- `landingpage.skillherz.com/studenti/consenso` → `studenti/consenso.html`

## Deploy

Push su `main` → build automatico via Cloudflare Workers Builds (`npx wrangler deploy`).
