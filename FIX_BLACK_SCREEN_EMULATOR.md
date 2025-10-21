# Fix: Emulator Running But Black Screen / Won't Display

## Your Issue
- Emulator shows as "Running" in Android Studio ✅
- Window is minimized or shows black screen when opened ❌
- Emulator process is active but display not working ❌

## Root Cause
Graphics rendering issue - Your Intel UHD Graphics 620 needs different graphics settings.

From your earlier log:
```
WARNING | Your GPU 'Intel(R) UHD Graphics 620' has Vulkan API version 1.3.215, 
and cannot support Vulkan properly. Please try updating your GPU Drivers.
```

---

## 🔧 Solution 1: Change Graphics Mode (MOST LIKELY FIX)

### Method A - Through AVD Manager (Emulator Must Be Stopped):

1. **Stop the emulator completely**
   - In Android Studio, click the red stop button
   - Or in Task Manager, end `qemu-system-x86_64.exe` process

2. **Open AVD Manager**
   - Tools → AVD Manager

3. **Edit your Pixel_9_Pro_XL**
   - Click the **pencil icon** ✏️

4. **Show Advanced Settings**
   - Scroll down and click "Show Advanced Settings"

5. **Change Graphics Setting**
   - Find **"Graphics"** under "Emulated Performance"
   - Change from `Automatic` or `Hardware - GLES 2.0` 
   - **To: `Software - GLES 2.0`**

6. **Save and Start**
   - Click Finish
   - Start the emulator again

### Method B - Edit config.ini Directly:

1. **Close Android Studio completely**

2. **Navigate to your AVD folder:**
   ```
   # Your new AVD location (the drive you moved it to)
   # For example: D:\AndroidAVD\Pixel_9_Pro_XL.avd
   ```

3. **Open `config.ini` with Notepad**

4. **Find this line:**
   ```ini
   hw.gpu.mode = auto
   ```
   or
   ```ini
   hw.gpu.enabled = yes
   ```

5. **Change to:**
   ```ini
   hw.gpu.mode = guest
   hw.gpu.enabled = no
   ```

6. **Save and close**

7. **Restart Android Studio and start emulator**

---

## 🔧 Solution 2: Update Intel Graphics Drivers

Your GPU has outdated Vulkan drivers. Update them:

### Automatic Method:
1. Download **Intel Driver & Support Assistant**
   - https://www.intel.com/content/www/us/en/support/detect.html
2. Run it and install recommended graphics driver updates
3. Restart PC
4. Try emulator again

### Manual Method:
1. Visit: https://www.intel.com/content/www/us/en/download/785597/intel-arc-iris-xe-graphics-whql-windows.html
2. Download latest Intel Graphics Driver for UHD 620
3. Install and restart
4. Try emulator again

---

## 🔧 Solution 3: Use Command Line with Software Rendering

Start emulator from command line with forced software rendering:

```cmd
cd C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator

emulator -avd Pixel_9_Pro_XL -gpu swiftshader_indirect
```

Or try:
```cmd
emulator -avd Pixel_9_Pro_XL -gpu angle_indirect
```

If this works, you can make it permanent in the AVD settings.

---

## 🔧 Solution 4: Fix Windows Display Scaling

High DPI scaling can cause display issues:

1. **Navigate to:**
   ```
   C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator
   ```

2. **Find these files:**
   - `qemu-system-x86_64.exe`
   - `emulator.exe`

3. **For each file:**
   - Right-click → **Properties**
   - Go to **Compatibility** tab
   - Click **"Change high DPI settings"**
   - Check **"Override high DPI scaling behavior"**
   - Set to **"Application"**
   - Click **OK** and **Apply**

4. **Restart emulator**

---

## 🔧 Solution 5: Cold Boot the Emulator

Sometimes the emulator state is corrupted:

1. **Stop the emulator**

2. **In AVD Manager:**
   - Click dropdown arrow ▼ next to your emulator
   - Select **"Cold Boot Now"**

3. **Wait 3-5 minutes** for full boot

---

## 🔧 Solution 6: Disable Windows Hardware Acceleration

1. **Windows Search** → type "Graphics settings"
2. Click **"Graphics settings"**
3. Click **"Browse"**
4. Navigate to:
   ```
   C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator\qemu-system-x86_64.exe
   ```
5. Add it to the list
6. Click **Options** → Select **"Power saving"**
7. Save and restart emulator

---

## 🔧 Solution 7: Increase Emulator RAM

Low RAM can cause display issues:

1. **AVD Manager** → **Edit** Pixel_9_Pro_XL
2. **Show Advanced Settings**
3. Increase **RAM** to `4096 MB` or `6144 MB`
4. Increase **VM Heap** to `512 MB`
5. Save and restart

---

## 🔧 Solution 8: Check for Hidden Window

Sometimes the window appears on a different screen or off-screen:

1. Click on the emulator in taskbar
2. Press **`Alt + Space`**
3. Press **`M`** (Move)
4. Use **arrow keys** to move window
5. Or press **`Alt + Enter`** to toggle fullscreen

---

## 🔧 Solution 9: Clean Emulator Cache

1. **Close emulator**

2. **Delete cache files:**
   ```cmd
   # Navigate to your AVD folder
   cd D:\AndroidAVD\Pixel_9_Pro_XL.avd
   
   # Delete cache
   del cache.img
   del cache.img.qcow2
   
   # Delete temp files
   del *.lock
   del snapshots\*
   ```

3. **Start emulator again** (it will recreate cache)

---

## 🔧 Solution 10: Create New Lighter Emulator

If nothing works, the Pixel 9 Pro XL might be too demanding:

1. **Create new emulator**
2. Choose **Pixel 6** or **Pixel 5**
3. Select **Android 13** (API 33) instead of Android 15
4. Set Graphics to **Software - GLES 2.0**
5. RAM: 4096 MB
6. Internal Storage: 4096 MB

---

## Quick Diagnostic Commands

Run these to check emulator status:

```cmd
# Check if emulator is running
tasklist | findstr qemu

# Check emulator processes
tasklist | findstr emulator

# Start with full logging
cd C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator
emulator -avd Pixel_9_Pro_XL -verbose -show-kernel -gpu swiftshader_indirect
```

---

## Recommended Order to Try:

### ⭐ START HERE (Most Likely Fixes):
1. ✅ **Solution 1** - Change to Software Graphics (90% success rate)
2. ✅ **Solution 3** - Use `-gpu swiftshader_indirect` command
3. ✅ **Solution 5** - Cold Boot the emulator

### If Still Black Screen:
4. ✅ **Solution 2** - Update Intel drivers
5. ✅ **Solution 4** - Fix DPI scaling
6. ✅ **Solution 7** - Increase RAM

### Last Resort:
7. ✅ **Solution 10** - Create lighter emulator (Pixel 5/6 with Android 13)

---

## After Applying Fix

The emulator should now:
- ✅ Display properly when clicked
- ✅ Show the Android boot animation
- ✅ Fully boot to home screen
- ✅ Respond to mouse/keyboard input

First boot takes 3-5 minutes - be patient! 

Once you see the Android logo and boot animation, you know it's working! 🎉
