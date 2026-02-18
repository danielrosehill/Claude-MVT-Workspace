# MVT Workspace Setup

Run a complete setup of the MVT scanning environment. Assume the user is starting from scratch.

## Process

### Phase 1: System Check

Check the following and report status for each:

1. **Python 3**: Check if Python 3.8+ is available (`python3 --version`). If not, install it via the system package manager.
2. **pip**: Check if pip is available (`pip3 --version`). Install if missing.
3. **ADB**: Check if ADB is installed (`adb version`). If not, install via `sudo apt install android-tools-adb` (or equivalent for the detected package manager).
4. **MVT**: Check if `mvt-android` is available. If not, install it with `pip3 install mvt` (use `pipx` if available, otherwise a user-level pip install with `--user` or a venv).

Report the status of each component clearly before proceeding.

### Phase 2: Install Missing Components

Install any missing components identified in Phase 1. Ask the user for confirmation before running `sudo` commands.

### Phase 3: Download Indicators of Compromise

1. Check if an `iocs/` directory exists in the workspace root
2. If not, clone Amnesty International's indicators:
   ```
   git clone https://github.com/AmnestyTech/investigations.git iocs
   ```
3. If it exists, pull the latest updates:
   ```
   cd iocs && git pull
   ```

### Phase 4: Device Connection Check

1. Run `adb devices` to check for connected devices
2. If a device is listed, report its serial number and connection status
3. If no device is found, guide the user through:
   - Enabling Developer Options (Settings > About Phone > tap Build Number 7 times)
   - Enabling USB Debugging (Settings > Developer Options > USB Debugging)
   - Connecting the device via USB
   - Accepting the authorization prompt on the device
4. Once connected, gather device info:
   - `adb shell getprop ro.product.model`
   - `adb shell getprop ro.build.version.release`
   - `adb shell getprop ro.product.manufacturer`

### Phase 5: Save Context

Save the environment profile to `context/environment.md` with:
- Date of setup
- Python version
- MVT version (`mvt-android version`)
- ADB version
- Device model, manufacturer, and Android version (if connected)
- IOC source and download date

### Phase 6: Summary

Print a clear summary showing:
- All installed components and versions
- Device connection status
- IOC status
- Ready/not ready status for scanning
- Next step: suggest running `/scan` if everything is ready
