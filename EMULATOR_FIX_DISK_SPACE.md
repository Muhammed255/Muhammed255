# Android Emulator Fix - Disk Space Issue

## The Exact Problem

```
FATAL | Not enough space to create userdata partition. 
Available: 7625.23 MB at C:\Users\MohamedAbdelazim\.android\avd\..\avd\Pixel_9_Pro_XL.avd
Need: 9830.40 MB
```

**Your emulator needs 9.6 GB but only 7.4 GB is available on your C: drive.**

---

## Solution Options

### ✅ Option 1: Free Up Space on C: Drive (Quickest)

1. **Clean up disk space on C: drive:**
   - Empty Recycle Bin
   - Run Disk Cleanup (search "Disk Cleanup" in Windows)
   - Delete temporary files: `Win + R` → type `temp` → Delete all files
   - Delete Windows update files
   - Uninstall unused programs

2. **Free at least 3-4 GB additional space** (need total ~10 GB free)

3. **Restart the emulator**

---

### ✅ Option 2: Reduce Emulator Storage Size (Recommended)

Reduce the internal storage requirement from the default 9.6 GB:

1. Open **Android Studio**
2. Go to **Tools** → **AVD Manager**
3. Click the **pencil icon** (Edit) next to Pixel_9_Pro_XL
4. Click **Show Advanced Settings**
5. Scroll down to **Memory and Storage** section
6. Change **Internal Storage** from `9830 MB` to `4096 MB` (4 GB) or `6144 MB` (6 GB)
7. Click **Finish**
8. Try starting the emulator again

---

### ✅ Option 3: Move AVD Location to Another Drive (Best Long-term)

Move your Android Virtual Devices to a drive with more space (e.g., D: drive):

#### Steps:

1. **Close Android Studio completely**

2. **Create new AVD directory on another drive:**
   ```cmd
   mkdir D:\AndroidAVD
   ```

3. **Copy existing AVDs (if you want to keep them):**
   ```cmd
   xcopy "C:\Users\MohamedAbdelazim\.android\avd" "D:\AndroidAVD" /E /I /H
   ```

4. **Set environment variable:**
   - Right-click **This PC** → **Properties** → **Advanced system settings**
   - Click **Environment Variables**
   - Under **User variables**, click **New**
   - Variable name: `ANDROID_AVD_HOME`
   - Variable value: `D:\AndroidAVD`
   - Click **OK** on all windows

5. **Alternative: Create system-level environment variable via Command Prompt (as Administrator):**
   ```cmd
   setx ANDROID_AVD_HOME "D:\AndroidAVD"
   ```

6. **Restart Android Studio**

7. **Verify the new location:**
   - Open Android Studio → Tools → AVD Manager
   - Create a new Pixel 9 Pro XL (or your AVDs should appear from the copied location)

---

### ✅ Option 4: Reduce Data Partition Size via config.ini

Manually edit the AVD configuration:

1. **Close Android Studio**

2. **Navigate to:**
   ```
   C:\Users\MohamedAbdelazim\.android\avd\Pixel_9_Pro_XL.avd
   ```

3. **Open `config.ini` with Notepad**

4. **Find and modify these lines:**
   ```ini
   disk.dataPartition.size=9830MB
   ```
   
   **Change to:**
   ```ini
   disk.dataPartition.size=4096MB
   ```

5. **Save the file**

6. **Start the emulator**

---

### ✅ Option 5: Use a Lighter Device Profile

Instead of Pixel 9 Pro XL, create a lighter emulator:

1. **AVD Manager** → **Create Virtual Device**
2. Choose a lighter device:
   - **Pixel 5** (2340x1080)
   - **Pixel 6** (2400x1080)
   - Or any device with smaller screen/storage requirements
3. Select **Android 13** or **Android 14** (not 15/36)
4. Configure with:
   - RAM: 4096 MB
   - Internal Storage: 4096 MB
   - VM Heap: 512 MB

---

## Quick Command to Check Available Space

```cmd
# Check available space on C: drive
wmic logicaldisk get size,freespace,caption
```

---

## Recommended Actions (In Order)

### Immediate Fix:
1. ✅ **Try Option 2 first** (Reduce storage to 4GB via AVD Manager) - Takes 2 minutes
2. If that doesn't work, **Try Option 1** (Free up 3-4 GB on C: drive)

### Long-term Solution:
3. ✅ **Implement Option 3** (Move AVD to another drive) - Prevents future issues

---

## After Applying Fix

Start the emulator again:
```cmd
cd C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator
emulator -avd Pixel_9_Pro_XL
```

The emulator should now start successfully! 🎉

---

## Additional Notes

### Why does Pixel 9 Pro XL need so much space?
- High-resolution display (1344 x 2992)
- Latest Android 15 (API 36) system image
- Google Play Store integration
- Default storage partition size

### Can 4GB internal storage cause issues?
- No, 4GB is sufficient for most development and testing
- You can still install apps and test functionality
- If you need more space later, you can increase it

### Warning
Once you reduce the storage size, you cannot easily increase it without recreating the AVD.
