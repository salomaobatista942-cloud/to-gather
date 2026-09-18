# To-Gather — Coolify deployment

## Build source

Use the Git repository containing this project and the compose file:

`docker-compose.togather.yaml`

The compose file builds the To-Gather application services from source instead of pulling the original WorkAdventure application images.

## Required production secrets

Set these in Coolify, not in Git:

- `SECRET_KEY`
- `ROOM_API_SECRET_KEY`
- `MAP_STORAGE_API_TOKEN` (or derive it from `SECRET_KEY`)
- database/storage credentials when those services are enabled
- OIDC client secret when OIDC is enabled
- LiveKit/Jitsi/BBB credentials only when those integrations are enabled

## Domain

Set:

`DOMAIN=your-domain.example`

The same domain is used by the single-domain production routing rules.

## Authentication

For a first private deployment, configure an OIDC provider that you control. Keep `OPENID_CLIENT_ID`, `OPENID_CLIENT_SECRET`, and `OPENID_CLIENT_ISSUER` in Coolify environment variables.

## Telemetry

The To-Gather compose explicitly sets:

`ENABLE_TELEMETRY=false`

No installation telemetry should be sent to the original WorkAdventure statistics service by this compose configuration.

## Important

Do not commit a real `.env` file or production secrets to Git.
