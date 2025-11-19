# ESP32 Development Setup Guide for macOS Silicon (M2)

**Target Hardware:** Lolin32 Lite (ESP32)
**Target OS:** macOS (Apple Silicon M2)
**ESP-IDF Version:** v5.1.x or v5.2.x
**ESP-ADF Version:** v2.7+

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Install ESP-IDF](#install-esp-idf)
3. [Install ESP-ADF](#install-esp-adf)
4. [Verify Installation](#verify-installation)
5. [Troubleshooting](#troubleshooting)
6. [Quick Start](#quick-start)

---

## Prerequisites

### System Requirements

- **macOS 11.0+** (Monterey or later)
- **Apple Silicon M2** (native ARM64 support)
- **5 GB disk space** minimum
- **Xcode Command Line Tools**

### Install Homebrew (if not already installed)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install Required Dependencies

```bash
brew install python@3.11 git wget cmake ninja
```

Verify Python installation:
```bash
python3 --version
# Expected: Python 3.11.x or 3.12.x
```

---

## Install ESP-IDF

### Step 1: Clone ESP-IDF Repository

Choose a location for your development tools (e.g., `~/esp`):

```bash
mkdir -p ~/esp
cd ~/esp
git clone -b release/v5.1 https://github.com/espressif/esp-idf.git
cd esp-idf
```

**Note:** Use `release/v5.2` if you prefer v5.2 instead:
```bash
git clone -b release/v5.2 https://github.com/espressif/esp-idf.git
```

### Step 2: Install Python Virtual Environment & Dependencies

```bash
cd ~/esp/esp-idf
python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

### Step 3: Run the Installation Script

```bash
./install.sh
```

This installs ESP-IDF tools (compiler, debugger, etc.) optimized for Apple Silicon.

**Expected output:**
```
Installing ESP-IDF tools to /Users/YOUR_USERNAME/.espressif
```

### Step 4: Set Up Environment Variables

Add the following to your shell profile (`~/.zshrc` or `~/.bash_profile`):

```bash
# ESP-IDF
export IDF_PATH=~/esp/esp-idf
export IDF_TOOLS_PATH=~/.espressif
alias get_idf='. $IDF_PATH/export.sh'
```

Apply changes:
```bash
source ~/.zshrc
```

Verify setup:
```bash
get_idf
```

You should see:
```
Checking Python compatibility...
Python compatibility checks passed.
```

---

## Install ESP-ADF

### Step 1: Clone ESP-ADF Repository

```bash
cd ~/esp
git clone -b release/v2.7 https://github.com/espressif/esp-adf.git
cd esp-adf
```

### Step 2: Link ESP-IDF with ESP-ADF

ESP-ADF needs to know where ESP-IDF is located. Set the environment variable:

```bash
# Add to ~/.zshrc
export ADF_PATH=~/esp/esp-adf
export IDF_PATH=~/esp/esp-idf
```

Apply changes:
```bash
source ~/.zshrc
```

### Step 3: Install ADF-Specific Python Dependencies

```bash
cd ~/esp/esp-adf
pip install -r requirements.txt
```

### Step 4: Test ADF Setup

```bash
cd ~/esp/esp-adf/examples/get-started/hello_world
idf.py set-target esp32
idf.py menuconfig
# (Just navigate to exit, don't change anything)
```

You should see the menuconfig interface. If this works, ADF is properly configured.

---

## Verify Installation

### Test 1: Check ESP-IDF Version

```bash
get_idf
python -c "import esp_idf_version; print(esp_idf_version.get_version())"
```

Expected: `ESP-IDF v5.1.x` or `v5.2.x`

### Test 2: Check Compiler

```bash
xtensa-esp32-elf-gcc --version
```

Expected: `xtensa-esp32-elf-gcc (esp-2024...)`

### Test 3: Build a Simple IDF Example

```bash
cd ~/esp/esp-idf/examples/get-started/hello_world
idf.py build
```

Should complete without errors.

### Test 4: Build a Simple ADF Example

```bash
cd ~/esp/esp-adf/examples/get-started/hello_world
idf.py set-target esp32
idf.py build
```

Should complete without errors.

---

## Troubleshooting

### Issue: "Command not found: idf.py"

**Solution:** Make sure you've sourced the IDF environment:
```bash
source $IDF_PATH/export.sh
# Or use the alias
get_idf
```

### Issue: "Python version mismatch"

**Solution:** Ensure Python 3.11+ is being used:
```bash
which python3
python3 --version
# If not correct, deactivate and reactivate venv
deactivate
source ~/esp/esp-idf/venv/bin/activate
```

### Issue: "xtensa-esp32-elf-gcc not found"

**Solution:** The tools path is not set correctly. Verify:
```bash
echo $IDF_TOOLS_PATH
ls -la ~/.espressif/tools/
```

If empty, re-run:
```bash
cd ~/esp/esp-idf
./install.sh
```

### Issue: "ADF examples fail to build"

**Ensure backward compatibility is enabled** (for IDF 5.1 with ADF v2.7):

```bash
idf.py menuconfig
# Navigate to: Component config > IDF SoC HAL and Low-level Peripheral Drivers
# Enable: "Backward compatibility: use 'driver' instead of HAL"
# Save and exit
```

### Issue: "Port not found when flashing"

**Solution:** Identify your USB device:
```bash
ls /dev/tty.* | grep -i usb
# Example output: /dev/tty.usbserial-1410
```

Then flash with explicit port:
```bash
idf.py -p /dev/tty.usbserial-1410 flash
```

---

## Quick Start

Once installed, here's the typical workflow:

### Create a New Project

```bash
cd ~/projects
cp -r ~/esp/esp-adf/examples/get-started/hello_world ./my_audio_app
cd my_audio_app
```

### Set Target & Configure

```bash
get_idf  # Activate IDF environment
idf.py set-target esp32
idf.py menuconfig
```

### Build

```bash
idf.py build
```

### Flash to Device

```bash
idf.py -p /dev/tty.usbserial-1410 flash
```

### Monitor Serial Output

```bash
idf.py -p /dev/tty.usbserial-1410 monitor
```

**Tip:** To exit the monitor, press `Ctrl+]`

### Combined Build, Flash & Monitor

```bash
idf.py -p /dev/tty.usbserial-1410 build flash monitor
```

---

## Environment Setup Summary

Add this to your `~/.zshrc` for future sessions:

```bash
# ============================================
# ESP Development Environment
# ============================================

# ESP-IDF Configuration
export IDF_PATH=~/esp/esp-idf
export IDF_TOOLS_PATH=~/.espressif

# ESP-ADF Configuration
export ADF_PATH=~/esp/esp-adf

# Convenience aliases
alias get_idf='. $IDF_PATH/export.sh'
alias get_adf='. $ADF_PATH/export.sh'

# Auto-activate IDF on shell startup (optional)
# source $IDF_PATH/export.sh
```

---

## Additional Resources

- [ESP-IDF Official Documentation](https://docs.espressif.com/projects/esp-idf/en/latest/)
- [ESP-ADF Official Documentation](https://docs.espressif.com/projects/esp-adf/en/latest/)
- [Lolin32 Lite Documentation](https://docs.wemos.cc/en/latest/d32/d32.html)
- [ESP32 I2S Audio Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/i2s.html)

---

## Next Steps

Once installation is complete:

1. **Review the [Device Implementation](../../trd/001-minimum-viable-implementation.md#device-implementation)** section of the TRD
2. **Set up I2S audio** using the INMP441 microphone and MAX98357A amplifier pins
3. **Test WebSocket connectivity** with your backend
4. **Review [Audio Configuration](../../trd/001-minimum-viable-implementation.md#audio-configuration)** (16kHz, 16-bit PCM mono)

---

**Last Updated:** November 2024
**Tested On:** macOS 14.x / 15.x (Apple Silicon M2)
