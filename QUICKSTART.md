# 🎵 Soul Lab — Quick Reference

## Testing Your App

**Server is running on port 8080!**

Open in your browser:
- Local: http://localhost:8080
- Or open `index.html` directly (drag into browser)

## Next Steps

### 1. Add Your Drum Samples
Copy your drum samples to `downloads/for app/` with these exact names:

**Live Kit:**
- `live-kick.wav`
- `live-snare.wav`
- `live-hats.wav`
- `live-perc.wav`

**808 Kit:**
- `808-kick.wav`
- `808-snare.wav`
- `808-hats.wav`
- `808-perc.wav`

### 2. Test the Features

**Presets (top left):**
- 🟣 Boom-Bap Soul (De La Soul vibes) - 92 BPM, swing, live drums
- 🟡 Jazzy R&B (Neo-Soul) - 86 BPM, guitar + keys
- 🔵 Trap-Soul (Modern) - 140 BPM, 808s, rapid hats
- 🟢 Chicago Soul (Drill) - 94 BPM, horns + drums

**Controls:**
- ▶️ **Play/Pause** - Start/stop playback
- ⏹️ **Stop** - Stop and reset to beginning
- 🗑️ **Clear All** - Reset all patterns

**Instrument Swapping (top of sequencer):**
- 🥁 Live Drums ↔ 🎛️ 808 Kit
- 🎸 Bass Guitar ↔ 🧪 Synth Bass

**Each Track Has:**
- 🎲 Randomize button - instant variation
- 16 step grid - click to toggle beats

**Global Settings:**
- **BPM** (60-160) - Speed of the beat
- **Swing** (0-60%) - Groove/shuffle feel
- **Humanize** - Slight timing variation
- **Vinyl Crackle** - Lo-fi aesthetic
- **Key** - Musical root note
- **Scale** - Minor Pentatonic, Dorian, Minor, Mixolydian

## How to Use

### Quick Start Workflow:
1. Click a preset (🟣 Boom-Bap Soul is great to start)
2. Press ▶️ Play
3. Click grid cells to modify the beat
4. Try 🎲 randomize buttons for instant changes
5. Swap 🥁 Live Drums ↔ 🎛️ 808 Kit to hear difference
6. Adjust BPM and Swing to taste
7. Click 🗑️ Clear All to start fresh

### Building From Scratch:
1. Start with kick on beats 1 and 3 (steps 0, 8)
2. Add snare on beats 2 and 4 (steps 4, 12)
3. Fill in hi-hats (every other step for classic feel)
4. Add bass notes (try every 4 steps)
5. Layer keys or guitar sparingly
6. Add percussion for flavor

## Tips for Kids

- **No wrong answers!** The scale system keeps everything musical
- **Randomize is your friend** - click 🎲 on any track for ideas
- **Less is more** - sparse beats often groove better
- **Copy the presets** - load a preset, then modify it
- **Experiment with swapping** - same beat, different drums = different vibe
- **Fast BPM** (130+) = trap/drill, **Slow BPM** (80-95) = boom-bap/soul

## Troubleshooting

**No sound?**
- Click Play button (browsers block audio until user interaction)
- Check browser console (F12) for errors
- Samples missing? App uses fallback synth drums

**Samples not loading?**
- Check file names match exactly (case-sensitive)
- Supported formats: .wav, .mp3, .ogg
- Look in browser console for "✅ All drum samples loaded"

**Timing sounds off?**
- Try reducing Swing to 0
- Disable Humanize
- Refresh page to reset Tone.js

## Customization Ideas

- **Add more presets** - Copy a preset function and modify
- **Change colors** - Edit `:root` CSS variables
- **Add instruments** - Follow pattern in code
- **32 steps** - Change `Array(16)` to `Array(32)`
- **More tracks** - Add to TRACKS array

---

**Have fun making beats! 🎶**
