---
title: Setup Ssh Ports
source_raw: RAW/setup/ssh-ports.md
compiled_wiki_path: WIKI/infrastructure/ssh-ports.md
compiled_at: 2026-04-30T10:03:25.666Z
type: system-note
tags: [aiagentnerd, compiled, infrastructure, ssh, ports, cloudflare, networking, setup]
---

# Setup Ssh Ports

## Summary
This note documents SSH access, networking ports, and Cloudflare Tunnel configuration for the AiAgentNerd server. It captures the primary access method, internal service port layout, and how the tunnel exposes subdomains without exposing the server directly.

## Key Concepts
- SSH access to the server via `ssh nerd@nerd-server`
- Cloudflare Tunnel is the standard exposure method for all web services
- Internal services bind to localhost ports, never exposed directly to the internet
- Subdomains (e.g., `deck.aiagentnerd.com`) are routed through the tunnel

## Practical Use
- Log into the server using `ssh nerd@nerd-server`
- Understand that no ports except SSH (and perhaps monitoring) are open directly
- Reference this note when adding new services to map their local ports through the tunnel

## Implementation Notes
- **SSH Command**: `ssh nerd@nerd-server`
- **Tunnel Domain**: `aiagentnerd.com`
- **Tunnel Standard**: Cloudflare Tunnel used for all HTTP traffic; no port forwarding or iptables rules for web services.
- **Internal Ports**: Services run on ephemeral or fixed localhost ports as configured in their respective service files; they are not documented here—see individual service notes.

## Related
- [[cloudflare-network]]
- [[hermes-setup]]
- [[Networking Ports and IPs]]
- [[acr-dashboard-ui-b5cd7aa5-335b-4342-8461-29717600d1fa]]
- [[acr-overview-da74bd9b-66f7-4705-a7f5-11c50645f812]]

## Source
- RAW: [[RAW/setup/ssh-ports]]
