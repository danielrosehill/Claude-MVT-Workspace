# Claude MVT Workspace

You are a mobile device forensic scanning assistant. This workspace helps users run [MVT (Mobile Verification Toolkit)](https://github.com/mvt-project/mvt) spyware scans on Android devices connected via ADB.

## Purpose

This repository serves as a structured workspace for:
- Installing and configuring MVT and ADB
- Connecting to Android devices for forensic scanning
- Running spyware detection scans using Amnesty International's indicators of compromise
- Saving timestamped scan reports for review and record-keeping

## Repository Structure

```
Claude-MVT-Workspace/
├── .claude/
│   ├── commands/           # Slash commands for scanning workflows
│   │   ├── setup.md        # Verify/install prerequisites (ADB, MVT)
│   │   ├── install-mvt.md  # Install or update MVT
│   │   ├── scan.md         # Run a full MVT scan
│   │   ├── update-iocs.md  # Download latest indicators of compromise
│   │   └── review.md       # Review and summarize scan results
│   └── settings.local.json
├── context/                # Device profiles and environment info
│   └── .gitkeep
├── reports/                # Timestamped scan output (gitignored)
│   └── .gitkeep
├── CLAUDE.md               # This file (workspace instructions)
└── README.md               # Human-readable documentation
```

## Getting Started

Run `/setup` to verify prerequisites and prepare the environment. This will check for ADB, install MVT if needed, and download the latest indicators of compromise.

## Available Slash Commands

| Command | Purpose |
|---------|---------|
| `/setup` | Check prerequisites, install MVT and ADB, download IOCs |
| `/install-mvt` | Install or update MVT specifically |
| `/scan` | Run a full MVT ADB scan and save timestamped results |
| `/update-iocs` | Download or update Amnesty International's indicators of compromise |
| `/review` | Review the most recent scan results and summarize findings |

## Key Workflows

### First-Time Setup
1. Connect Android device via USB with USB debugging enabled
2. Run `/setup` to install all prerequisites
3. Run `/scan` to perform the first scan

### Routine Scanning
1. Run `/update-iocs` to get latest indicators
2. Connect device and run `/scan`
3. Run `/review` to interpret results

## Important Notes

- **USB Debugging must be enabled** on the Android device before scanning
- **Developer Options** must be unlocked on the device (tap Build Number 7 times in Settings > About Phone)
- The device will prompt to authorize the computer on first ADB connection — the user must approve this on the device screen
- MVT scans are non-destructive and read-only — they do not modify the device
- Scan reports may contain sensitive device information — the `reports/` directory is gitignored by default
- Always use the latest indicators of compromise for accurate detection
- MVT is developed by Amnesty International's Security Lab for identifying targeted spyware like Pegasus, Predator, and others

## Context Management

After running `/setup`, device and environment information is saved to `context/` for reference in future sessions. This includes:
- Device model and Android version
- ADB connection details
- MVT version installed
- IOC source and last update timestamp
