# ⚡ QUICK FIX - Black Screen / Emulator Won't Display

## Problem
✅ Emulator shows "Running" in Android Studio  
❌ Black screen or window won't display properly

## Cause
Your Intel UHD Graphics 620 can't handle Hardware graphics mode.

---

## 🚀 FASTEST FIX (Takes 3 Minutes)

### Step 1: Stop the Emulator
- Click the **red stop button** in Android Studio
- Or close the emulator window

### Step 2: Open AVD Manager
- **Tools** → **AVD Manager**

### Step 3: Edit Graphics Settings
1. Click **pencil icon** ✏️ next to "Pixel_9_Pro_XL"
2. Click **"Show Advanced Settings"** (scroll to bottom)
3. Find **"Graphics"** under "Emulated Performance" section
4. Change from `Automatic` or `Hardware - GLES 2.0`
5. **To: `Software - GLES 2.0`** ⬅️ THIS IS THE FIX
6. Click **"Finish"**

### Step 4: Start Emulator
- Click the **play button** ▶️
- **Wait 3-5 minutes** for first boot
- You should now see the Android boot animation! ✅

---

## Alternative: Start with Command (If Above Doesn't Work)

```cmd
cd C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator

emulator -avd Pixel_9_Pro_XL -gpu swiftshader_indirect
```

This forces software rendering from command line.

---

## If Window is Hidden/Off-Screen

1. Click emulator icon in Windows taskbar
2. Press **`Alt + Space`** then **`M`**
3. Use **arrow keys** to move window back
4. Or press **`Alt + Enter`** to fullscreen

---

## What This Does

**Before:**
- Emulator tries to use Hardware GPU acceleration
- Intel UHD 620 with old Vulkan drivers can't handle it
- Result: Black screen / no display

**After:**  
- Emulator uses Software rendering
- Works on any GPU
- Slightly slower but fully functional
- Result: Working display! ✅

---

## Still Black After Changing to Software?

Try **Cold Boot**:
1. In AVD Manager
2. Click **dropdown arrow** ▼ next to emulator name
3. Select **"Cold Boot Now"**
4. Wait 5 minutes for complete boot

---

## Success Signs

You'll know it's working when you see:
1. ⚪ Android logo (white background)
2. 🔵 "Android" text with animation
3. 🏠 Android home screen

**Be patient!** First boot with software rendering takes 3-5 minutes.

---

## Next Steps

Once working:
1. Update your Intel Graphics drivers for better performance
2. Consider creating a lighter emulator (Pixel 5 instead of Pixel 9 Pro XL)
3. See `FIX_BLACK_SCREEN_EMULATOR.md` for more optimization tips

Good luck! 🎉
