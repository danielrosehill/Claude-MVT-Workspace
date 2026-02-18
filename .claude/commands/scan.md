# Run MVT Spyware Scan

Run a full MVT scan on the connected Android device via ADB and save timestamped results.

## Process

### Step 1: Pre-Flight Checks

Verify before scanning:

1. **MVT installed**: Confirm `mvt-android` is available
2. **ADB connected**: Run `adb devices` and confirm exactly one device is connected and authorized
   - If no device: stop and guide the user to connect their device
   - If "unauthorized": tell the user to check their device screen for the authorization prompt
   - If multiple devices: ask the user which device to scan (by serial number)
3. **IOCs available**: Check if the `iocs/` directory exists and contains STIX2 indicator files
   - Look for `.stix2` or `.json` files in `iocs/`
   - If missing, suggest running `/update-iocs` first

### Step 2: Prepare Output Directory

Create a timestamped output directory:

```
reports/YYYY-MM-DD_HH-MM-SS/
```

Use the current date and time for the directory name.

### Step 3: Run the Scan

Run the MVT ADB scan:

```bash
mvt-android check-adb --output /path/to/reports/YYYY-MM-DD_HH-MM-SS/ --iocs /path/to/iocs/**/*.stix2
```

**Important:**
- Find all `.stix2` files in the `iocs/` directory tree and pass them via `--iocs`
- If no STIX2 files are found, run the scan without `--iocs` (it will still collect artifacts but won't match against known indicators)
- Stream the output so the user can see progress
- The scan may take several minutes depending on device content

### Step 4: Post-Scan Summary

After the scan completes:

1. List all output files generated in the report directory
2. Check for any files with `_detected` suffix — these indicate potential matches against IOCs
3. Provide a brief summary:
   - Total artifacts checked
   - Number of detections (if any)
   - Location of the full report
4. If detections were found, flag them prominently and suggest running `/review` for detailed analysis
5. If no detections, confirm the scan was clean

### Step 5: Update Context

Append a scan log entry to `context/scan-history.md` with:
- Scan timestamp
- Device scanned (model + serial)
- MVT version used
- IOC source date
- Result summary (clean / N detections)
- Report path
