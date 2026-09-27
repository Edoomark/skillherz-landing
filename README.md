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

## Worker temporaneo `skillherz-studenti` (redirect legacy)

Il 2026-09-27 le landing sono state consolidate in questo worker. In precedenza la pagina consenso studenti era servita da un worker separato all'URL:

```
https://skillherz-studenti.sviluppo-4bd.workers.dev/consenso
```

Quell'URL è stato inviato via mail ai genitori ed è valido per la conferma del consenso fino a 30 giorni. Per non rompere i link già spediti è stato ridistribuito un worker minimale `skillherz-studenti` che fa solo un 302 verso `landingpage.skillherz.com/studenti/consenso` preservando la query string (token e scelta).

- Sorgente: `/tmp/skillherz-studenti-redirect/` (fuori dal repo, deploy manuale via `wrangler deploy`).
- Nessun path oltre `/consenso` → 404.
- **DA CANCELLARE dopo il 2026-10-27** (30 giorni dal cutover): dashboard Cloudflare → Workers → `skillherz-studenti` → Delete, oppure `wrangler delete` dalla cartella sorgente.

La cella `I5` della scheda `Campagne` del foglio contatti punta già al nuovo URL `https://landingpage.skillherz.com/studenti/consenso`, quindi le mail nuove non usano più il dominio legacy.
