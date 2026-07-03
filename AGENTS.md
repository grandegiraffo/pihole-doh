# AGENTS.md

## Scope
- This repository is only infrastructure: a Docker Compose stack for Pi-hole + Cloudflared + Watchtower.
- The runtime entrypoint is `compose.yaml` (there is no application package/build system).

## Required setup
- Set `PIHOLE_WEBPASSWORD` before first start; `compose.yaml` falls back to insecure `changeme`.
- Keep secrets in `.env` (gitignored); use `.env.example` as the template.

## Canonical commands
- Validate config: `docker compose config`.
- Start with health gating: `docker compose up --detach --wait`.
- Stop and remove persisted state: `docker compose down -v` (also removes named volumes).

## Wiring constraints (easy to break)
- Keep `pihole` dependent on Cloudflared health: `depends_on.cloudflared.condition: service_healthy`.
- Preserve static container IP mapping on network `pihole`:
  - `pihole` = `172.42.0.2`
  - `cloudflared` = `172.42.0.3`
  - `watchtower` = `172.42.0.4`
- Pi-hole upstream DNS is intentionally pinned to Cloudflared: `PIHOLE_DNS_=172.42.0.3#5053`.

## Focused verification
- Cloudflared endpoint: `curl -sf http://172.42.0.3:49312/metrics`.
- Pi-hole endpoint: `curl -sf http://172.42.0.2/admin`.

## CI mismatch to know
- CI removes `53:53` mappings before startup to avoid DNS port conflicts on shared runners.
