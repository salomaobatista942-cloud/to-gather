# To-Gather

This repository is the To-Gather fork based on WorkAdventure.

## Goal

Run the platform on infrastructure controlled by the To-Gather owner, with application images built from this repository.

## Production compose

Use:

`docker-compose.togather.yaml`

It builds Play, Back, Uploader and Map Storage locally from their Dockerfiles.

## Status

This is the first infrastructure-independence pass. Authentication and security hardening remain documented in `docs/togather/INDEPENDENCE-AUDIT.md`.

## Secrets

Never commit production secrets. Inject them through Coolify or another secret manager.
