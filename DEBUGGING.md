# 🔧 Debugging Guide - No Sound Issue

## Quick Fixes (Try These First)

### 1. Test Audio Button
I just added a **🔊 Test Audio** button below the Play/Stop buttons.

**Steps:**
1. Refresh the browser page
2. Click **🔊 Test Audio** button
3. You should hear a beep + kick drum
4. If you hear it → audio works! Issue is with pattern/sequencer
5. If you don't hear it → audio is blocked by browser

### 2. Check Browser Console
Press **F12** (or right-click → Inspect → Console tab)

**Look for these messages:**
- ✅ `Tone.js audio context started` - Good!
- ✅ `All drum samples loaded` - Samples work
- ✅ `Using synth drums` - Fallback is OK
- ✅ `Step 0: X instruments triggered` - Pattern is playing
- ❌ Any red errors - Copy and send to me

### 3. Browser Audio Permissions

**Chrome/Edge:**
- Look for speaker icon 🔇 in address bar
- Click it and allow audio

**Firefox:**
- Click shield/lock icon in address bar
- Check "Autoplay" is allowed

**Safari:**
- Settings → Websites → Auto-Play
- Allow for localhost/your domain

### 4. Check System Volume
- Is your computer volume up?
- Are headphones plugged in correctly?
- Try adjusting volume while clicking Test Audio button

## Detailed Diagnostics

### Open Browser Console (F12) and Check:

**On Page Load:**
```
Should see:
🎵 Soul Lab initialized!
📊 Current pattern: [shows which tracks have steps]
💡 Click "Test Audio" button first...
```

**When You Click Test Audio:**
```
Should see:
🔊 Testing audio...
✅ Test kick triggered
✅ Audio test complete
```

**When You Click Play:**
```
Should see:
🎵 Tone.js audio context started
▶️ Playback started
🥁 Kick (synth) at step 0
🎸 Bass: E1 at step 0
(etc...)
```

### If Console Shows Errors:

**"The AudioContext was not allowed to start"**
- Browser blocking audio
- Solution: Click Test Audio button (requires user interaction)

**"Failed to load resource: 404"**
- Can't find sample files
- This is OK! App uses synth drums as fallback
- Add your samples to `downloads/for app/` later

**"Cannot read property 'triggerAttackRelease' of undefined"**
- Synth not initialized
- Refresh page
- Check if Tone.js CDN loaded (Network tab in DevTools)

## Visual Checks

### Pattern Should Look Like This:
```
Kick:  ● _ _ _ ● _ _ _ ● _ _ _ ● _ _ _
Snare: _ _ _ _ ● _ _ _ _ _ _ _ ● _ _ _
Hats:  ● _ ● _ ● _ ● _ ● _ ● _ ● _ ● _
Bass:  ● _ _ ● _ _ _ ● _ _ ● _ _ _ _ _
Keys:  ● _ _ _ _ _ _ _ ● _ _ _ _ _ _ _
```

If all cells are empty (○ ○ ○...), the preset didn't load!

**Fix:** Click any preset button (🟣 Boom-Bap Soul)

### Playhead Should Move
When playing, you should see a green outline moving across the grid.

**If playhead doesn't move:**
- Transport not started
- Check console for errors
- Try clicking Stop, then Play again

## Still No Sound?

### Try This Test Sequence:

1. **Refresh the page** (Ctrl+R / Cmd+R)
2. **Open console** (F12)
3. **Click "🔊 Test Audio"** → Should hear beep
4. **Click "🟣 Boom-Bap Soul"** → Pattern loads
5. **Click "▶️ Play"** → Should hear drums/bass/keys
6. **Watch console** → Should see "triggered" messages

### Copy and Send Me:
If still broken, copy this info:

1. **Browser**: (Chrome/Firefox/Safari/Edge + version)
2. **OS**: (Windows/Mac/Linux)
3. **Console output**: (copy all messages)
4. **Does Test Audio work?**: (Yes/No)
5. **Does playhead move?**: (Yes/No)
6. **Are grid cells filled?**: (Yes/No)

## Common Solutions

### No Sound BUT Console Shows Activity:
→ **Volume/output device issue**
- Check system mixer/volume
- Try different headphones/speakers
- Check browser isn't muted

### No Sound AND No Console Messages:
→ **Tone.js didn't load**
- Check internet connection (Tone.js loads from CDN)
- Try opening: https://unpkg.com/tone@14.8.49/build/Tone.js
- If that fails, internet/firewall blocking CDN

### Playhead Moves But No Sound:
→ **Audio context issue**
- Click Test Audio first
- Check browser console for red errors
- Try different browser

### Test Audio Works But Play Button Doesn't:
→ **Pattern/sequencer issue**
- Click a preset button
- Check if grid has filled cells (●)
- Check console for "triggered" messages

---

**Let me know what you see in the console and I'll help fix it!** 🎵
