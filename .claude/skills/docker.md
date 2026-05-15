# Docker / Demo Setup

## Standard Demo Startup

- Ask user for the demo setup location if not specified
- Compare requested version with local images: `docker images | grep tbe-server` — pull if behind
- Update version in `docker-compose.yml` if needed
- When deploying a build first tome always replace`application-demo.yml` with the reference config from https://youtrack.jetbrains.com/articles/IDES-A-567/Reference-config-for-application-demo.yaml unless asked otherwise
- Wait for all containers healthy: `docker compose ps`
- Add certificates in system trust store per `README.md`
- Ask user to run commands to add certificates (giving sudo required), and what command exactly
- After each redeploy, refresh Chrome MCP's NSS cert (no sudo) — system trust store alone isn't read by Chromium:
  `certutil -D -d sql:$HOME/.pki/nssdb -n tbe-demo-localhost 2>/dev/null; certutil -A -d sql:$HOME/.pki/nssdb -t "C,," -n tbe-demo-localhost -i /usr/local/share/ca-certificates/server-ssl-cert.crt`
- If asked to login to UI make sure to enable ide-services-ui skill
