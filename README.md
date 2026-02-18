# Claude MVT Workspace

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) workspace for running [MVT (Mobile Verification Toolkit)](https://github.com/mvt-project/mvt) spyware scans on Android devices connected via ADB.

MVT is developed by [Amnesty International's Security Lab](https://securitylab.amnesty.org/) and is used to detect indicators of compromise from targeted spyware such as Pegasus, Predator, and others.

## What This Is

This is a **Claude Code workspace** — a structured repository with slash commands and context files that turn Claude Code into a guided forensic scanning assistant. Clone this repo, open it in Claude Code, and use the slash commands to walk through the entire process from setup to scan review.

## Prerequisites

- A computer running Linux (tested on Ubuntu)
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI installed
- An Android device with USB debugging enabled
- A USB cable connecting the device to the computer

## Quick Start

```bash
git clone https://github.com/danielrosehill/Claude-MVT-Workspace.git
cd Claude-MVT-Workspace
claude
```

Then inside Claude Code:

1. **`/setup`** — Installs ADB, MVT, downloads indicators of compromise, and verifies device connection
2. **`/scan`** — Runs a full MVT scan and saves timestamped results to `reports/`
3. **`/review`** — Summarizes scan findings in plain language

## Available Commands

| Command | Description |
|---------|-------------|
| `/setup` | Install prerequisites (ADB, MVT, Python) and download IOCs |
| `/install-mvt` | Install or update MVT specifically |
| `/scan` | Run MVT ADB scan with timestamped report output |
| `/update-iocs` | Download latest Amnesty International indicators of compromise |
| `/review` | Review and summarize the most recent scan results |

## How It Works

- **MVT** checks an Android device (via ADB) against known indicators of compromise (IOCs) published by Amnesty International and other security researchers
- **Scan reports** are saved as timestamped directories in `reports/` (gitignored by default to protect sensitive data)
- **IOCs** are downloaded from Amnesty International's [mobileverification/mvt-indicators](https://github.com/AmnestyTech/investigations) repository

## Important Notes

- USB debugging must be enabled on the device (Settings > Developer Options > USB Debugging)
- Developer Options are unlocked by tapping "Build Number" 7 times in Settings > About Phone
- The device will prompt you to authorize the computer — tap "Allow" on the device
- Scans are **read-only** and do not modify the device
- Reports may contain sensitive device information — do not commit them to public repositories

## License

MIT

## Credits

- [MVT](https://github.com/mvt-project/mvt) by Amnesty International Security Lab
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) by Anthropic
