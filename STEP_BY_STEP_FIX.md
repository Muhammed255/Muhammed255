# 📱 Step-by-Step: Fix Emulator Black Screen

## Your Current Situation
```
✅ Virtualization enabled in BIOS
✅ AVD moved to another drive  
✅ Emulator starts and shows "Running"
❌ BLACK SCREEN - Can't see Android
```

## The Fix: Change Graphics to Software Mode

---

## 📋 Step-by-Step Instructions

### ⏹️ STEP 1: Stop the Emulator
```
In Android Studio → Click the RED SQUARE STOP BUTTON
Wait until status changes from "Running" to stopped
```

---

### 🔧 STEP 2: Open AVD Manager
```
Android Studio Top Menu Bar:
Tools → AVD Manager

OR

Click the phone icon in the top toolbar
```

---

### ✏️ STEP 3: Edit Your Emulator
```
Find: Pixel_9_Pro_XL
Click: The PENCIL ICON ✏️ (on the right side)
```

---

### ⚙️ STEP 4: Show Advanced Settings
```
Scroll to the BOTTOM of the window
Click: "Show Advanced Settings" button
```

---

### 🎨 STEP 5: Change Graphics Setting
```
Scroll down to find section: "Emulated Performance"

Look for:
┌─────────────────────────────────┐
│ Graphics:  [Dropdown ▼]         │
└─────────────────────────────────┘

Click the dropdown, you'll see:
  - Automatic
  - Hardware - GLES 2.0
  - Software - GLES 2.0  ⬅️ SELECT THIS ONE
  - Software - GLES 1.1

SELECT: Software - GLES 2.0
```

---

### ✅ STEP 6: Save Changes
```
Scroll to the BOTTOM
Click: "Finish" button
```

---

### ▶️ STEP 7: Start Emulator
```
Click the GREEN PLAY BUTTON ▶️ next to Pixel_9_Pro_XL
```

---

### ⏰ STEP 8: Wait for Boot (IMPORTANT!)
```
FIRST BOOT TAKES 3-5 MINUTES!

You will see:
1. [0:00 - 0:30] Emulator window opens
2. [0:30 - 2:00] Black screen (this is NORMAL)
3. [2:00 - 3:00] White Android logo appears
4. [3:00 - 4:00] "Android" text with dots animation
5. [4:00 - 5:00] Home screen appears! ✅

DO NOT CLOSE IT! Just wait patiently.
```

---

## ⚠️ Common Mistakes

### ❌ Don't Do This:
- Closing emulator after 1 minute thinking it's broken
- Changing multiple settings at once
- Starting emulator while another is running
- Not scrolling down to see "Show Advanced Settings"

### ✅ Do This:
- Wait full 5 minutes for first boot
- Change ONLY Graphics setting
- Make sure previous emulator is fully stopped
- Be patient - software rendering is slower

---

## 🎯 Expected Results

### After Changing to Software Graphics:

**Pros:**
- ✅ Display works properly
- ✅ Can see Android interface
- ✅ Fully functional emulator
- ✅ No crashes

**Cons:**
- ⏱️ Slightly slower performance
- ⏱️ Longer boot time (3-5 min vs 1-2 min)
- Still perfectly usable for development!

---

## 🆘 If Still Black After 5 Minutes

### Try Cold Boot:

1. **Stop emulator** (red stop button)

2. **In AVD Manager:**
   - Find your emulator
   - Click **dropdown arrow** ▼ (right side)
   - Select **"Cold Boot Now"**

3. **Wait another 5 minutes**

---

## 💻 Alternative Method: Command Line

If AVD Manager method doesn't work, try this:

### Open Command Prompt:
```cmd
cd C:\Users\MohamedAbdelazim\AppData\Local\Android\Sdk\emulator

emulator -avd Pixel_9_Pro_XL -gpu swiftshader_indirect
```

This forces software graphics from the command line.

---

## ✨ Success Checklist

You'll know it's working when:
- [ ] Emulator window stays open
- [ ] You see Android boot logo (white background)
- [ ] You see "Android" text with animated dots
- [ ] Home screen appears with app icons
- [ ] You can click and interact with the screen

---

## 📞 Still Having Issues?

If black screen persists after trying software graphics:

### Check These:
1. **Is the window hidden?**
   - Press `Alt + Space` then `M`, use arrow keys
   
2. **RAM too low?**
   - Increase to 4096 MB in AVD settings
   
3. **Drivers outdated?**
   - Update Intel Graphics drivers
   
4. **Emulator too heavy?**
   - Try creating Pixel 5 with Android 13 instead

See **FIX_BLACK_SCREEN_EMULATOR.md** for detailed solutions.

---

## 🎉 You're Done!

Once you see the Android home screen, you're all set! The emulator is ready for app development and testing.

**Pro Tip:** Subsequent boots will be faster (30-60 seconds) once the emulator is set up.
