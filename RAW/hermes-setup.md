Hermes runs with PM2 and OpenRouter as part of the AiAgentNerd backend service.
# Hermes Setup

Hermes is the backend gateway for AiAgentNerd. It runs through PM2 as the hermes process and listens on port 3100. It connects to OpenRouter for LLM calls and supports wiki compilation, chat routes, and automation logic.

Important details:
- backend folder: /home/nerd/aiagentnerd
- wiki folder: /home/nerd/aiagentnerd-wiki
- process manager: PM2
- restart command: pm2 restart hermes --update-env
- logs command: pm2 logs hermes
- API port: 3100
Hermes exposes an API on port 3100 and integrates OpenRouter for LLM calls.
