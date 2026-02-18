# Update Indicators of Compromise

Download or update the latest indicators of compromise (IOCs) used by MVT to detect known spyware.

## Process

### Step 1: Check Current IOC Status

1. Check if the `iocs/` directory exists in the workspace root
2. If it exists, check the last git commit date to see how stale the indicators are
3. Report the current status

### Step 2: Download or Update

**If `iocs/` does not exist:**

Clone Amnesty International's investigations repository which contains STIX2 indicator files:

```bash
git clone https://github.com/AmnestyTech/investigations.git iocs
```

**If `iocs/` already exists:**

Pull the latest updates:

```bash
cd iocs && git pull
```

### Step 3: Verify IOCs

1. Count the number of `.stix2` files found in the `iocs/` directory tree
2. List the indicator categories/directories available
3. Show the date of the most recent indicator file

### Step 4: Update Context

Update `context/environment.md` with:
- IOC source: AmnestyTech/investigations
- Last updated: current date/time
- Number of STIX2 indicator files available

### Step 5: Report

Print:
- Whether this was a fresh download or an update
- Number of indicator files available
- Date of newest indicators
- Suggestion to run `/scan` if a device is connected
