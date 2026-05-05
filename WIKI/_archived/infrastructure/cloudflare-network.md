---
title: Architecture Cloudflare Network
source_raw: RAW/architecture/cloudflare-network.md
compiled_wiki_path: WIKI/infrastructure/cloudflare-network.md
compiled_at: 2026-04-30T09:58:45.860Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, cloudflare, networking, ssh, architecture]
status: archived
archived_at: 2026-05-05T06:28:12.241Z
reclassified_to: architecture/cloudflare-network.md
---

# Architecture Cloudflare Network

## Summary
AiAgentNerd uses Cloudflare Tunnel as the standard method to expose internal services (Deck, X Post App, etc.) to the public internet without opening firewall ports. SSH access to the server is provided via `nerd@nerd-server`, and internal services listen on localhost ports that are mapped to public subdomains through the tunnel.

## Key Concepts
- **Cloudflare Tunnel**: Primary exposure mechanism; all public-facing services are routed through Cloudflare’s edge, providing HTTPS and DDoS protection without direct port forwarding.
- **SSH Access**: Server administration is performed via SSH to `nerd@nerd-server` using key-based authentication.
- **Internal Port Mapping**: Services run on localhost ports (e.g., Deck on 3000, backend API on 4000) and are mapped to subdomains (e.g., `deck.aiagentnerd.com`) via the tunnel configuration.

## Practical Use
- Access the Deck dashboard at `deck.aiagentnerd.com` (tunneled).
- Access the X Post App at `x-post.aiagentnerd.com` (tunneled).
- SSH into the server: `ssh nerd@nerd-server`.
- No need to open firewall ports or manage direct IP exposure; all traffic is secured through Cloudflare.

## Implementation Notes
- The Cloudflare Tunnel client (likely `cloudflared`) runs on the server and maintains a persistent outbound connection to Cloudflare’s edge.
- Each service is assigned a subdomain in Cloudflare DNS, and the tunnel configuration maps those subdomains to the corresponding localhost port.
- Internal ports are defined in each service’s configuration (e.g., Deck on 3000, backend on 4000); exact ports may vary per deployment.
- SSH uses standard key-based authentication; ensure the appropriate public key is added to `~/.ssh/authorized_keys` on the server.
- The tunnel automatically handles TLS termination and can be monitored via the Cloudflare dashboard.

## Related
- [[ssh-ports]]
- [[Networking Ports and IPs]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]
- [[agent-control-room-acr-fb05e0f0-c846-45b2-9728-dd7bd55af8ca]]

## Source
- RAW: [[RAW/architecture/cloudflare-network]]
