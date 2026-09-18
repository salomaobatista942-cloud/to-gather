# To-Gather — Initial Independence Audit

This document records the first pass over the uploaded `To-Gather` source tree.

## Current authentication architecture

### Anonymous
Browser -> Pusher `/anonymLogin` -> UUID generation -> WorkAdventure JWT signed with `SECRET_KEY` -> browser localStorage -> WebSocket/API.

### OpenID Connect
Browser -> Pusher `/login-screen` -> configured OIDC issuer -> authorization-code + PKCE callback -> OIDC userinfo/access token -> WorkAdventure JWT signed locally with `SECRET_KEY` -> browser localStorage -> `/me` -> OIDC userinfo validation.

The WorkAdventure JWT is locally signed. The original WorkAdventure creator is not required to sign it.

## External dependencies found

These are configurable integrations rather than all being mandatory:

- OIDC identity provider
- LiveKit
- Jitsi / BigBlueButton
- STUN/TURN
- Matrix
- Sentry
- PostHog
- WorkAdventure telemetry
- external embedded integrations
- S3-compatible storage

The production compose previously referenced prebuilt WorkAdventure images under `thecodingmachine/workadventure-*`.

## Changes prepared in this package

`docker-compose.togather.yaml` was added. It builds the core application images directly from this repository:

- `play/Dockerfile`
- `back/Dockerfile`
- `uploader/Dockerfile`
- `map-storage/Dockerfile`

The production Back service explicitly sets `ENABLE_TELEMETRY=false`.

No credentials are embedded in the new configuration.

## Security items for the next hardening pass

1. JWT is stored in browser localStorage.
2. OIDC access tokens are embedded in the WorkAdventure JWT.
3. Invalid-token logging must never include the bearer token.
4. Logout redirect handling should be reviewed for bearer-token exposure.
5. Production secrets must be generated outside Git and injected by Coolify.
6. OIDC should point to an identity provider controlled by the To-Gather owner.
