# Base44 Dev Environment

## What this project is
A static HTML site (Spanish-language reels/entertainment page: `index.html`, `amp.html`) with local `.mp4` videos and an `ads.txt`. No build step, no backend, no dependencies.

## How it runs here
Served by `nginx:alpine` via `docker-compose.base44.yml`, bind-mounting the repo at `/usr/share/nginx/html` (read-only). Host port 3000 → container 80.

- No live-reload dev server needed: static files are served directly by nginx. Edits to HTML/CSS/assets are visible on browser refresh.
- Call `reload_preview` after edits only if you want to force the preview iframe to refresh.

## Verify it works
```
docker compose -f docker-compose.base44.yml up -d --build
docker compose -f docker-compose.base44.yml ps
curl -sf -H "Host: external-preview.example.com" http://localhost:3000/
```
The curl must return the `index.html` content.

## Secrets
None required. The page references external ad scripts (AdSense, Adsterra) that work without credentials in the browser.
