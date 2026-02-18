# Install or Update MVT

Install or update the Mobile Verification Toolkit (MVT) on this system.

## Process

### Step 1: Check Current Installation

1. Check if `mvt-android` is already installed and get its version
2. Check which Python environment is active
3. Check if `pipx` is available (preferred installation method)

### Step 2: Install or Update

**If MVT is not installed:**

Try installation methods in this order of preference:

1. **pipx** (if available): `pipx install mvt`
2. **pip with venv**: Create a venv at `.venv` in the workspace root if one doesn't exist, activate it, then `pip install mvt`
3. **pip user install** (fallback): `pip3 install --user mvt`

**If MVT is already installed:**

1. Show current version
2. Check for updates: `pip3 install --upgrade mvt` (or `pipx upgrade mvt`)
3. Show new version after upgrade

### Step 3: Verify Installation

1. Run `mvt-android version` to confirm it works
2. Run `mvt-android check-adb --help` to confirm ADB integration is functional
3. Update `context/environment.md` with the current MVT version

### Step 4: Report

Print:
- Installation method used
- MVT version installed
- Whether this was a fresh install or upgrade
- Any warnings or issues encountered
