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

## Antivirus notice

Windows Defender and some antivirus software may flag `tally-connector-windows-amd64.exe` as suspicious. This is a **false positive** — the connector is safe, but because it's a new, unsigned executable that makes outbound network connections, heuristic scanners err on the side of caution.

**Why it happens:**
- The `.exe` is not code-signed (EV certification is planned)
- The app polls a cloud server over HTTPS (heuristic scanners flag this as "beaconing")
- Go binaries bundle their own runtime, which looks different from typical Windows apps

**How to fix it:**

1. **Windows Defender SmartScreen** — Click "More info" → "Run anyway" when the SmartScreen popup appears
2. **Microsoft Defender** — Go to **Windows Security → Virus & threat protection → Protection history**, find the blocked item, and select **Allow**
3. **Other antivirus** — Add `tally-connector-windows-amd64.exe` to your antivirus exclusion list
4. **Browser download block** — In Chrome/Edge, click the download bar and select "Keep" or "Keep anyway"

The connector is open-source and the source code is available for audit at [mole-ai-release/MoleAI-connector](https://github.com/mole-ai-release/MoleAI-connector).

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
