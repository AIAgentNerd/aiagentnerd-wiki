---
title: Cloudflare Network
source_raw: RAW/cloudflare-network.md
compiled_wiki_path: WIKI/infrastructure/cloudflare-network.md
compiled_at: 2026-04-24T14:36:37.140Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, cloudflare, networking, ssh]
---

# Cloudflare Network

## Summary
Server external connectivity is handled via Cloudflare Tunnel, encompassing SSH remote access and network port configuration for exposed services.

## Key Concepts
- **Cloudflare Tunnel** — Secure, outbound-only reverse proxy tunnel enabling external access without a public IP.
- **SSH Access** — Remote administrative shell access to the server through the tunnel fabric.
- **Port Configuration** — Network port assignments and exposure rules that define which services are reachable.

## Details
The networking stack relies on Cloudflare Tunnel to route traffic from the internet to the server. SSH is configured for remote management within this tunnel architecture. Port configuration governs service exposure, determining how traffic is mapped and which endpoints are accessible.

## Practical Notes
- Audit the tunnel dashboard and local configuration to verify SSH and application port mappings.
- Limit exposed ports to the minimum required for operations.
- Confirm tunnel daemon health if SSH or services become unreachable.

## Source
- RAW: [[RAW/cloudflare-network]]

## Related
- [[Networking Ports and IPs]]
- [[ssh-ports]]
- [[git-obsidian-setup]]
- [[hermes-setup]]
- [[test-nginx]]
