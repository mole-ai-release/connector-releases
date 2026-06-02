# MoleAI Tally Connector

Desktop connector that bridges [MoleAI](https://moleai.com) cloud with Tally Prime running on your local machine.

```
MoleAI Cloud ──HTTPS──▶ tally-connector.exe ──HTTP──▶ Tally Prime (localhost:9000)
```

The connector polls MoleAI every 30 seconds, picks up pending sync jobs, and pushes them as vouchers to your local Tally. No public IP or firewall changes needed.

## Download

Get the latest `tally-connector-windows-amd64.exe` from [Releases](https://github.com/mole-ai-release/connector-releases/releases).

Available for:
- **Windows** (amd64, arm64, 386) — `.exe`
- **Linux** (amd64, arm64)
- **macOS** (amd64, arm64 — Intel & Apple Silicon)

## Setup (first time)

1. **Double-click** `tally-connector-windows-amd64.exe`
2. Enter your **pairing code** when prompted
3. Get a pairing code from **MoleAI → Settings → Tally ERP → Pair Connector**
4. Paste the code and press Enter
5. Done — the connector is linked to your account and will start syncing

## Usage

```
tally-connector.exe                        # Normal mode — keep window open
tally-connector.exe -register <code>       # Register with pairing code
tally-connector.exe -silent                # No console output (run in background)
tally-connector.exe -cloud-url <url>       # Custom cloud URL (self-hosted)
```

## Files (stored in `%APPDATA%/tally-connector/`)

| File | Purpose |
|------|---------|
| `config.json` | Cloud URL, machine ID, poll interval |
| `jobs.json` | Processed job IDs (prevents double-sync) |
| `api_key.dat` | API key for cloud authentication |

## Requirements

- **Tally Prime** with the Tally Developer API enabled (port 9000)
- **Windows** (primary target; Linux/macOS also available)
- The machine must be able to reach `https://api.moleai.com` (outbound HTTPS)

## Source Code

The connector source is at [mole-ai-release/MoleAI-connector](https://github.com/mole-ai-release/MoleAI-connector).
