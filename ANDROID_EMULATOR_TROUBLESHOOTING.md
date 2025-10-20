# Android Emulator - Process Termination Error Fix

## Issue
Pixel 9 Pro XL emulator in Android Studio terminates immediately after starting with a "process has terminated" error.

## Common Causes & Solutions

### 1. **Enable Hardware Virtualization (Most Common Fix)**

#### For Intel CPUs (VT-x):
1. Restart your PC and enter BIOS/UEFI (usually press F2, F10, Del, or Esc during boot)
2. Look for virtualization settings:
   - Intel Virtualization Technology (VT-x)
   - Intel VT-d
3. Enable these options
4. Save and exit BIOS

#### For AMD CPUs (AMD-V):
1. Restart your PC and enter BIOS/UEFI
2. Look for:
   - SVM Mode (Secure Virtual Machine)
   - AMD-V
3. Enable these options
4. Save and exit BIOS

#### Verify Virtualization is Enabled (Linux):
```bash
# Check if virtualization is enabled
egrep -c '(vmx|svm)' /proc/cpuinfo
# If output is > 0, virtualization is supported

# Check if KVM is available
kvm-ok
# or
ls -la /dev/kvm
```

### 2. **Install Required KVM Components (Linux)**

```bash
# Check if KVM is installed
sudo apt-get update
sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils

# Add your user to kvm group
sudo adduser $USER kvm
sudo adduser $USER libvirt

# Reboot after adding to groups
sudo reboot
```

### 3. **Increase RAM Allocation**

The Pixel 9 Pro XL requires significant resources:

1. Open Android Studio → Tools → AVD Manager
2. Click the pencil icon (Edit) for your Pixel 9 Pro XL
3. Click "Show Advanced Settings"
4. Adjust:
   - **RAM**: At least 4096 MB (4GB), preferably 8192 MB (8GB)
   - **VM Heap**: 512 MB or higher
   - **Internal Storage**: 4096 MB or higher

### 4. **Change Graphics Settings**

1. In AVD Manager → Edit your emulator
2. Under "Emulated Performance"
3. Try changing **Graphics** from:
   - `Automatic` → `Hardware - GLES 2.0`
   - OR if that fails → `Software - GLES 2.0`

### 5. **Use Compatible System Image**

Pixel 9 Pro XL might have compatibility issues:

1. In AVD Manager → Create a new virtual device
2. When selecting system image:
   - Try **Android 14** or **Android 13** instead of the latest version
   - Use **x86_64** images (NOT ARM unless you have ARM processor)
   - Download images with "Google APIs" or "Google Play"

### 6. **Check Android SDK Installation**

```bash
# From Android Studio Terminal:
cd $ANDROID_HOME/emulator

# Try running emulator from command line to see detailed error:
./emulator -avd Pixel_9_Pro_XL -verbose
```

### 7. **Clear Emulator Cache**

```bash
# Linux/Mac - Remove emulator cache
rm -rf ~/.android/avd/Pixel_9_Pro_XL.avd/cache/*

# Or completely recreate the AVD:
# 1. Delete the emulator from AVD Manager
# 2. Create a new one with the same specifications
```

### 8. **Update Android Emulator**

1. Android Studio → Tools → SDK Manager
2. SDK Tools tab
3. Check for updates:
   - Android Emulator
   - Android Emulator Hypervisor Driver (if on Windows)
   - Intel x86 Emulator Accelerator (HAXM) - for Intel CPUs

### 9. **Check System Requirements**

Minimum requirements for Pixel 9 Pro XL emulator:
- **CPU**: 64-bit processor with virtualization support
- **RAM**: 16GB system RAM (8GB minimum)
- **Disk Space**: 10GB+ free space
- **Graphics**: OpenGL 2.0+ compatible graphics card

### 10. **Run Emulator from Command Line (Debug Mode)**

```bash
# Navigate to Android SDK emulator directory
cd ~/Android/Sdk/emulator  # or your SDK path

# List available AVDs
./emulator -list-avds

# Run with verbose logging
./emulator -avd Pixel_9_Pro_XL -verbose -show-kernel -debug all

# Check the output for specific error messages
```

### 11. **Alternative: Create a Simpler Emulator**

If Pixel 9 Pro XL continues to fail, create a simpler device first:

1. AVD Manager → Create Virtual Device
2. Choose **Pixel 5** or **Pixel 6** instead
3. Select **Android 13** (API 33) with Google APIs
4. Configure with lower specs:
   - RAM: 4096 MB
   - Resolution: 1080x2340 (lower than Pixel 9 Pro XL)

### 12. **Check Emulator Logs**

```bash
# View emulator logs
cat ~/.android/avd/Pixel_9_Pro_XL.avd/emulator-log.txt

# Or in Android Studio:
# View → Tool Windows → Logcat
```

## Quick Checklist

- [ ] Virtualization enabled in BIOS
- [ ] KVM installed and user in kvm group (Linux)
- [ ] At least 4-8GB RAM allocated to emulator
- [ ] Graphics set to "Hardware - GLES 2.0" or "Software"
- [ ] Using x86_64 system image
- [ ] Android Emulator is up to date
- [ ] Sufficient disk space available
- [ ] No antivirus blocking emulator process

## Still Having Issues?

Run this diagnostic command and share the output:

```bash
# Get system info
echo "=== CPU Info ===" && lscpu | grep -i virtualization
echo "=== KVM Status ===" && ls -la /dev/kvm
echo "=== User Groups ===" && groups
echo "=== Emulator Version ===" && ~/Android/Sdk/emulator/emulator -version
```

## Most Likely Solution

Based on common issues, try these steps in order:

1. **Enable virtualization in BIOS** (Most common fix)
2. **Reduce RAM allocation** to 4096 MB
3. **Change Graphics to Software mode**
4. **Use Android 13 instead of 14/15**

If none of these work, share the output from running the emulator in verbose mode for more specific troubleshooting.
