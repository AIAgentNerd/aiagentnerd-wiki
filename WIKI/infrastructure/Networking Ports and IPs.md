---
title: Web Networking Ports And IPs
source_raw: RAW/web/Networking Ports and IPs.md
compiled_wiki_path: WIKI/infrastructure/Networking Ports and IPs.md
compiled_at: 2026-05-05T07:08:57.785Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, networking, ports, ips, cloudflare, nginx]
---

# Web Networking Ports And IPs

## Summary
IP addresses and network ports govern how traffic reaches the AiAgentNerd server and how services are isolated from each other. This note documents the local/public IP distinction, the system's specific port allocations, request flow through Cloudflare Tunnel and NGINX, and interface binding behavior.

## Key Concepts
- **IP address**: network identifier for the server machine; **port**: identifier for a specific service or process on that machine
- `127.0.0.1` (localhost): loopback interface; reachable only from the same machine
- `0.0.0.0`: wildcard bind; listens on all network interfaces (localhost + LAN + tunnel)
- **Cloudflare Tunnel**: the standard ingress method that replaces direct public IP exposure and port forwarding
- **Reverse proxy**: NGINX terminates public HTTP/S traffic and forwards to internal ports

## Practical Use
- Standard port map for the stack:
  - `3100` — Hermes API / backend
  - `8080` — Static frontend UI (Python server)
  - `9119` — Hermes dashboard
  - `80` / `443` — NGINX public ingress
- External request flow: Browser → Cloudflare (DNS + HTTPS) → Cloudflare Tunnel → Server → NGINX → target port
- NGINX routes subdomains to internal ports; e.g., `x.aiagentnerd.com` → `localhost:8080`, `api.aiagentnerd.com` → `localhost:3100`
- Only one process may bind to a given port at a time; assign unique ports for new agents or services
- Verify a service is listening: `ss -ltnp | grep <port>`
- Keep backend ports (e.g., `3100`) internal; public exposure happens only through Cloudflare Tunnel on `443`

## Implementation Notes
- Hermes gateway binds to `http://0.0.0.0:3100`, making it reachable via localhost, LAN, and Cloudflare Tunnel
- Bind internal-only services to `127.0.0.1` unless LAN or tunnel access is explicitly required
- Cloudflare Tunnel configuration should route traffic to the server without exposing its public IP directly
- When scaling or adding agents, document new port assignments to prevent collisions

## Related
- [[ssh-ports]]
- [[cloudflare-network]]
- [[cloudflare-network]]
- [[test-nginx]]
- [[aiagentnerd-master-notes]]

## Source
- RAW: [[RAW/web/Networking Ports and IPs]]
