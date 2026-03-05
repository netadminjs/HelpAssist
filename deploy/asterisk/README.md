# Asterisk Docker Prototype

This folder provides a fast Asterisk prototype for local testing with Docker Compose.

## Prerequisites

- Linux host with Docker Engine and Docker Compose plugin.
- Open host ports:
  - `5060/udp` and `5060/tcp` (SIP)
  - `10000-10100/udp` (RTP media)
  - `8088/tcp` (Asterisk HTTP/ARI)

## Start

```bash
cd deploy/asterisk
docker compose up -d
docker compose logs -f
```

## Test Endpoints

Configured SIP users in `config/pjsip.conf`:
- `6001` / `changeme6001`
- `6002` / `changeme6002`

Configured dialplan in `config/extensions.conf`:
- `600` = Echo test
- `700` = Playback test
- `800` = Placeholder helpdesk intake extension

## Useful Commands

```bash
cd deploy/asterisk
docker compose ps
docker exec -it helpassist-asterisk asterisk -rvvv
docker compose restart
docker compose down
```

## Git Workflow Recommendation

Use Git on the Linux machine. Recommended flow:

```bash
git clone git@github.com:netadminjs/HelpAssist.git
cd HelpAssist/deploy/asterisk
docker compose up -d
```

Why this is better than creating an ad-hoc local folder:
- version history,
- repeatable setup,
- easy rollback,
- easy to share/fix collaboratively.

If you need local-only overrides, keep them uncommitted or place them in ignored files.

