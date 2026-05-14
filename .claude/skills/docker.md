# Docker / Demo Setup

## Standard Demo Startup

- Ask user for the demo setup location if not specified
- Compare requested version with local images: `docker images | grep tbe-server` — pull if behind
- Update version in `docker-compose.yml` if needed
- When deploying a build first tome always replace`application-demo.yml` with the reference config from https://youtrack.jetbrains.com/articles/IDES-A-567/Reference-config-for-application-demo.yaml unless asked otherwise
- Wait for all containers healthy: `docker compose ps`
- Verify certificates in system trust store per `README.md`
- Ask user to run commands to add certificates (giving sudo required), and what command exactly
- If asked to login to UI make sure to enable ide-services-ui skill
