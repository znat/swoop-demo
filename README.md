# swoop-demo

A [gitpulse](https://github.com/znat/gitpulse) demo that monitors contributions to
`conversationHEALTH/redcrawl` and publishes them as an editorial story feed.

- **Live site:** https://znat.github.io/swoop-demo/ (password protected)
- **What it does:** A daily GitHub Actions job (`.github/workflows/monitor.yml`) runs
  `gitpulse analyze` + `gitpulse build` against the redcrawl git history, generating
  AI-narrated stories with illustrations, and deploys an encrypted static site to Pages.
- **Backfill:** First run covers all contributions since **May 4, 2026**
  (`analysis.bootstrapDays` in `.gitpulse.json`).

## Password protection

The published site is encrypted client-side (AES-GCM). Visitors enter the password to
unlock it in the browser — nothing is decrypted server-side. The password is stored as the
`GITPULSE_PASSWORD` repository secret and shared out-of-band.

## Secrets (Settings → Secrets and variables → Actions)

| Secret | Purpose |
| --- | --- |
| `TARGET_TOKEN` | Fine-grained PAT with `Contents: read` + `Metadata: read` on `conversationHEALTH/redcrawl` (checkout + PR/release queries) |
| `OPENAI_API_KEY` | MiniMax API key (text model `MiniMax-M3`) |
| `GOOGLE_API_KEY` | Gemini key for story illustrations |
| `BLOB_READ_WRITE_TOKEN` | Vercel Blob token for hosting illustrations |
| `GITPULSE_PASSWORD` | Site unlock password |

Run manually any time via **Actions → Monitor redcrawl → Run workflow**.
