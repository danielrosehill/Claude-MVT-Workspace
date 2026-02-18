# Review Scan Results

Review and summarize the most recent MVT scan results in plain language.

## Process

### Step 1: Find Latest Report

1. Look in the `reports/` directory for timestamped subdirectories
2. Identify the most recent scan by directory name (sorted by timestamp)
3. If no reports exist, tell the user to run `/scan` first
4. If multiple reports exist, list them and ask which one to review (default to most recent)

### Step 2: Analyze Results

For each JSON output file in the report directory:

1. **Check for `_detected` files** — these contain matched indicators and are the highest priority
2. **Parse detection files**: For each detection, extract:
   - What was detected (indicator name/description)
   - Which app or artifact matched
   - The matched IOC details
3. **Parse non-detection files**: Summarize what was scanned:
   - SMS messages checked
   - Installed packages reviewed
   - Chrome history examined
   - Other artifact categories

### Step 3: Generate Summary

Provide a clear, non-technical summary:

**If detections were found:**
- List each detection with a plain-language explanation of what it means
- Explain the severity and implications
- Recommend next steps (e.g., contact Amnesty International's Security Lab, consult a security professional, preserve evidence)
- Provide links to relevant resources

**If no detections:**
- Confirm the scan was clean
- Note what was checked
- Remind the user that a clean scan doesn't guarantee absence of all spyware — only that no known indicators were matched
- Suggest periodic rescanning with updated IOCs

### Step 4: Report Card

Print a summary card:

```
=== MVT Scan Review ===
Scan Date:      [timestamp]
Device:         [model]
MVT Version:    [version]
IOC Date:       [date]
Artifacts:      [count] files analyzed
Detections:     [count] (or "None")
Status:         CLEAN / DETECTIONS FOUND
=======================
```

### Step 5: Optional — Save Summary

Offer to save the plain-language summary as a markdown file in the report directory:
`reports/YYYY-MM-DD_HH-MM-SS/summary.md`
