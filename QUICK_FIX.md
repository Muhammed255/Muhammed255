# 🚀 QUICK FIX - Pixel 9 Pro XL Emulator Won't Start

## Your Problem
```
FATAL | Not enough space to create userdata partition.
Available: 7.6 GB, Need: 9.8 GB
```

---

## ⚡ FASTEST FIX (2 Minutes)

### Step 1: Open AVD Manager
- Android Studio → **Tools** → **AVD Manager**

### Step 2: Edit Your Emulator
- Click the **pencil icon** ✏️ next to "Pixel_9_Pro_XL"

### Step 3: Reduce Storage
- Click **"Show Advanced Settings"**
- Scroll to **Memory and Storage** section
- Find **"Internal Storage"**
- Change from `9830 MB` to `4096 MB`
- Click **"Finish"**

### Step 4: Start Emulator
- Click the **play button** ▶️ to start your emulator
- It should now work! ✅

---

## Alternative: Move to D: Drive (If Available)

```cmd
# Run these commands in Command Prompt:
mkdir D:\AndroidAVD
setx ANDROID_AVD_HOME "D:\AndroidAVD"
```

Then restart Android Studio and recreate the emulator.

---

## Still Not Working?

### Check available space:
```cmd
dir C:\
```

### Or use PowerShell:
```powershell
Get-PSDrive C | Select-Object Used,Free
```

You need at least **10 GB free** on C: drive for the emulator to work with full storage.

---

## What This Does

- **Before:** Emulator tried to allocate 9.8 GB
- **After:** Emulator only needs 4 GB
- **Result:** Fits in your available 7.6 GB space ✅

You'll still be able to:
- Install and test apps
- Use all Android features
- Debug your applications
- 4GB is plenty for development!

---

## Next Steps After Fix

1. Start your emulator
2. Wait for Android to boot (first boot takes 2-3 minutes)
3. Start developing! 🎉

If you need more storage later, you can always create a new AVD with larger storage when you have more disk space.
