---
title: Architecture Cloudflare Network
source_raw: RAW/architecture/cloudflare-network.md
compiled_wiki_path: WIKI/architecture/cloudflare-network.md
compiled_at: 2026-05-05T06:28:12.235Z
type: system-note
tags: [aiagentnerd, compiled, architecture, cloudflare, networking, ssh]
---

# Architecture Cloudflare Network

## Summary
Defines the Cloudflare Tunnel, SSH access, and network port configuration for the AiAgentNerd server. This covers the standard exposure method and remote access patterns used to operate the infrastructure.

## Key Concepts
- **Cloudflare Tunnel**: Project-standard method for exposing services securely to the internet
- **SSH Access**: Command-line server administration access
- **Port Configuration**: Network port assignments for tunneled services and internal tooling

## Practical Use
- Use as the reference for how AiAgentNerd services are exposed externally
- Documents the SSH access pattern for server administration
- Guides decisions on port allocation and tunnel routing

## Implementation Notes
- Cloudflare Tunnel is the standard exposure method for the project
- Server access: `ssh nerd@nerd-server`
- Domain: `aiagentnerd.com`

## Related
- [[cloudflare-network]]
- [[ssh-ports]]
- [[2026-04-30T09-34-15-091Z-4d760d59-a6b6-4af0-b0ef-5d2e6ffe86cf]]
- [[hermes-knowledge-system-full-architecture]]
- [[knowledge-ingestion-system]]

## Source
- RAW: [[RAW/architecture/cloudflare-network]]
