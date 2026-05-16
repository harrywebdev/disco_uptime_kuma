# Uptime Kuma on Disco.cloud

[Uptime Kuma](https://github.com/louislam/uptime-kuma) deployed to a self-hosted [Disco.cloud](https://disco.cloud) server.

- Image: `louislam/uptime-kuma:1`
- Public port: `3001`
- Persistent volume: `uptime-kuma-data` mounted at `/app/data` (SQLite DB, configs, screenshots)
- Domain: **<your_domain.com>**

## Prerequisites

1. A Disco server already set up (see [Set up your Server](https://disco.cloud/docs/get-started/set-up-your-server)).
2. The `disco` CLI installed locally and authenticated against your server.
3. This repo pushed to GitHub (Disco deploys from a GitHub repo).

## DNS

Point `<your_domain.com>` at your Disco server before adding the domain — Disco will provision a Let's Encrypt certificate on first deploy.

Create an `A` record:

```
<your_domain.com>.   A   <your-disco-server-ip>
```

## Deploy

Push this repo to GitHub, then from your machine:

```bash
disco projects:add \
  --name uptime-kuma \
  --github <your-gh-user>/uptime_kuma \
  --domain <your_domain.com>
```

That single command pulls the repo, reads `disco.json`, starts the container, attaches the volume, and provisions TLS for `<your_domain.com>`.

If the repo is public and your GitHub account isn't connected to Disco, append `--deployPublicRepo`.

## Updates

On every push to `main`, redeploy with:

```bash
disco deploy --project uptime-kuma
```

Or pin to a specific commit:

```bash
disco deploy --project uptime-kuma --commit <sha>
```

## First-run setup

Open https://<your_domain.com> and create the admin account. All state lives in the `uptime-kuma-data` volume and survives redeploys.
