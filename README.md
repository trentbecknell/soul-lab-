# 🎵 Soul Lab — Kids Beat Studio

An interactive web-based music production app for teaching kids Hip-Hop and R&B beat-making. Swap ingredients like live drums vs 808s, different bass sounds, keys, guitars, and horns to create endless musical combinations.

## Features

- **4 Genre Presets**: Boom-Bap Soul, Jazzy R&B, Trap-Soul, Chicago Soul-Hop
- **16-step Sequencer**: Classic drum machine grid for easy beat creation
- **Instrument Swapping**: 
  - Live drums ↔ 808 kit
  - Electric bass ↔ Synth bass
  - Keys, Guitar, Horns (always available)
- **Musical Intelligence**: Key and scale selection for consonant melodies
- **Real-time Controls**: BPM, swing, humanize, vinyl crackle effects
- **Kid-Friendly**: Color-coded tracks, randomize buttons, instant gratification

## Quick Start

1. **Add Your Drum Samples** (optional):
   - Place 8 drum samples in `downloads/for app/`
   - See `downloads/for app/README.md` for file naming
   - App works with synthesized drums if samples are missing

2. **Open the App**:
   ```bash
   # Option 1: Open index.html directly in browser
   open index.html  # macOS
   xdg-open index.html  # Linux
   
   # Option 2: Use a local server (recommended)
   python3 -m http.server 8000
   # Then visit http://localhost:8000
   ```

3. **Start Making Beats**:
   - Click a preset to load a beat style
   - Click grid cells to add/remove drum hits
   - Press Play ▶️ to hear your creation
   - Swap instruments to change the vibe
   - Adjust tempo and swing to taste

## Usage Tips

- **Try presets first** to hear what's possible
- **Randomize buttons** (🎲) create instant variation
- **Live drums** = boom-bap, neo-soul vibes
- **808 kit** = modern trap, drill, hip-hop
- **Electric bass** = funky, plucky (like bass guitar)
- **Synth bass** = deep sub-bass for trap/electronic
- **Swing** adds groove and human feel (try 10-20%)
- **Key/Scale** changes the musical flavor without wrong notes

## Technology

- **Vanilla JavaScript** - No frameworks, just pure JS
- **Tone.js** - Web Audio API wrapper for synthesis and scheduling
- **Single HTML File** - Everything inline for easy sharing
- **No Build Step** - Edit and refresh to see changes

## File Structure

```
soul-lab-/
├── index.html              # Main app (all code)
├── downloads/
│   └── for app/           # Put your drum samples here
│       ├── live-kick.wav
│       ├── live-snare.wav
│       ├── 808-kick.wav
│       └── ...
├── README.md              # This file
└── .github/
    └── copilot-instructions.md  # AI agent documentation
```

## Educational Use

Perfect for:
- Music production workshops
- Classroom beat-making sessions  
- After-school programs
- Summer camps
- Self-directed learning

**No login required** • **Works offline** (after first load) • **Shareable via single file**

## License

© 2025 Soul Lab (demo). Built for classrooms and kids workshops.