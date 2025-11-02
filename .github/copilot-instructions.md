# Soul Lab — Kids Beat Studio

## Project Overview
Soul Lab is a **standalone single-file web application** for teaching kids music production through Hip-Hop, R&B, Soul, and Jazz beat-making. Built entirely with vanilla JavaScript and Tone.js, it runs directly in the browser without a build system or external dependencies beyond the Tone.js CDN.

**Core Philosophy**: Educational simplicity meets authentic sound design. Kids should swap "ingredients" (808s vs live drums, bass types, keys, guitars, horns) to understand how iconic Hip-Hop/R&B sounds are constructed.

## Architecture

### Single-File Design Pattern
- **Everything lives in one HTML file**: `index.html` (or similar)
- Inline `<style>` block contains all CSS (custom design system, no frameworks)
- Inline `<script>` block contains all JavaScript logic
- **No build step, no bundler, no package.json** — open file in browser to run
- Tone.js loaded via CDN: `<script defer src="https://unpkg.com/tone@14.8.49/build/Tone.js"></script>`

### State Management
```javascript
const State = {
  bpm: 90, swing: 0, humanize: false, vinyl: false,
  key: 'C', scale: 'minorPent',
  kit: 'live', // 'live' or '808'
  bass: 'elec', // 'elec' or 'synth'
  tracks: [] // Array of {id, name, color, steps[16]}
};
```
- **Global mutable state object** — not React, not Redux
- Direct DOM manipulation via `document.getElementById()` and event listeners
- Pattern changes trigger `renderSequencer()` to rebuild grid HTML

### Audio Architecture (Tone.js)
Drums use **pre-loaded samples** from `downloads/for app/`, melodic instruments are **synthesized**:

1. **Drum Kits** — Two sets of samples, swappable via UI:
   - `live`: Acoustic drum samples (live-kick.wav, live-snare.wav, live-hats.wav, live-perc.wav)
   - `808`: Electronic drum samples (808-kick.wav, 808-snare.wav, 808-hats.wav, 808-perc.wav)
   - Loaded via `Tone.Player` at initialization from `downloads/for app/`
   
2. **Bass** — Two types:
   - `elec`: MonoSynth with triangle wave (plucky bass guitar emulation)
   - `synth`: MonoSynth with square wave + filter envelope (sub-bass)

3. **Melodic Instruments**:
   - **Keys**: PolySynth with sine waves → Rhodes-ish sound
   - **Guitar**: PluckSynth (Karplus-Strong physical modeling)
   - **Horns**: Synth with sawtooth wave + lowpass filter (brass stab)

4. **FX Chain**:
   ```javascript
   FX.reverb → FX.chorus → FX.comp → Destination
   ```
   - Shared reverb (3.5s decay) for space
   - Chorus on keys for shimmer
   - Compressor on all drums/bass for glue
   - Optional vinyl crackle (pink noise + highpass filter)

5. **Sample Loading**:
   - Pre-loaded drum samples from `downloads/for app/` directory
   - `Tone.Player` instances created at init for all drum sounds
   - `triggerStep()` uses samples for drums, synths for melodic instruments
   - Samples organized by kit type (live drums, 808s, etc.)

### Sequencer Design
- **16-step grid** per track (1 bar of 16th notes)
- 9 tracks: Kick, Snare, Hats, Perc, Pad (sample-only), Bass, Keys, Guitar, Horns
- Pattern stored as `steps: [true, false, false, ...]` (16 booleans per track)
- Playback via `Tone.Transport.scheduleRepeat(callback, '16n')`
- **Drum sounds come from pre-loaded samples**, melodic instruments use Tone.js synths
- **Musical intelligence**:
  - Scale system (`minorPent`, `dorian`, `minor`, `mixolydian`) 
  - Key transposition via `midiFromKey(key, semitone)`
  - Bass plays root note (-1 octave), keys play triads, guitar/horns play scale degrees

### Preset System
Four genre-based presets demonstrating different Hip-Hop/R&B eras:
- **Boom-Bap Soul** (De La Soul era): 92 BPM, swing, live drums, Dorian mode
- **Jazzy R&B** (Neo-Soul): 86 BPM, live drums, guitar + keys, Mixolydian
- **Trap-Soul** (Modern): 140 BPM, 808s, synth bass, rapid hi-hats
- **Chicago Soul-Hop**: 94 BPM, live drums, horns + keys

Each preset calls helper functions:
```javascript
pattern(['kick'], [0,4,8,12]); // Set steps for track
clear(['gtr','horn']); // Empty tracks
setKit('live'); setBass('elec'); // Swap instruments
```

## Key Conventions & Patterns

### Adding New Instruments
1. **Create synth builder function**:
   ```javascript
   function buildMyInstrument() {
     return new Tone.Synth({...config}).connect(FX.reverb);
   }
   ```

2. **Add to TRACKS array**:
   ```javascript
   { id:'myinst', name:'My Instrument', color:'#hexcode' }
   ```

3. **Handle in `triggerStep()`**:
   ```javascript
   case 'myinst': 
     MyInst.node.triggerAttackRelease(scaleNote(2), '8n', time); 
     break;
   ```

4. **Add UI toggle/selector** in left panel HTML

### Musical Scale Logic
- All melodic instruments use `scaleNote(degree, octave)` helper
- Degree maps to scale array: `scales.minorPent = [0,3,5,7,10]` (semitones)
- Example: In C minor pentatonic, degree 2 → 5 semitones → F
- Bass always plays degree 0 (root), keys play triads (0,2,4)

### Pattern Manipulation
```javascript
// Randomize a row (25% probability per step)
t.steps = t.steps.map(() => Math.random() < 0.25);

// Set specific pattern
row('kick').steps = Array(16).fill(false);
[0,4,8,12].forEach(c => row('kick').steps[c] = true);
```

### Sample Loading Pattern
```javascript
// At initialization
const Samples = {
  live: { kick: null, snare: null, hats: null, perc: null },
  kit808: { kick: null, snare: null, hats: null, perc: null }
};

async function loadSamples() {
  const basePath = 'downloads/for app/';
  // Load live drum kit
  Samples.live.kick = new Tone.Player(`${basePath}live-kick.wav`).toDestination();
  Samples.live.snare = new Tone.Player(`${basePath}live-snare.wav`).toDestination();
  // ... repeat for all samples
  
  // Wait for all buffers to load
  await Tone.loaded();
}
```
- Call `loadSamples()` before first playback
- Samples replace synthesized drums entirely
- Keep synths for melodic instruments (keys, guitar, horns, bass)

### UI Rendering Pattern
```javascript
function renderSequencer() {
  seqEl.innerHTML = ''; // Wipe old grid
  State.tracks.forEach(t => {
    // Build row div with label + 16 step cells
    // Attach onclick handlers to toggle steps
  });
}
```
- Called after every pattern change
- Each step cell gets `onclick` to toggle `t.steps[s]` boolean
- Playhead animation via `.classList.toggle('playhead', i===col)`

## Development Workflow

### Testing Changes
1. Edit the HTML file in VS Code
2. Open in browser (or use Live Server extension)
3. Click Play ▶️ to start Tone.Transport
4. Adjust BPM, swap kits, edit patterns in real-time
5. Check browser console for Tone.js errors

### Debugging Audio Issues
- **No sound?** Check `await Tone.start()` called (browser autoplay policy)
- **Timing glitches?** Verify `scheduleLoop()` and `applyTransport()` logic
- **Clicks/pops?** Adjust envelope attack times (try 0.001→0.01)
- **CPU spikes?** Reduce reverb decay or dispose unused synths

### Adding Genre Presets
1. Copy existing preset function structure
2. Set BPM, swing, key, scale to match genre feel
3. Use `pattern()` helper to place kicks, snares, hats
4. Add melodic patterns with `pattern(['bass'], [steps])`
5. Register in `PRESETS` object and add button in HTML

## Educational Design Principles

### Kid-Friendly UX
- **Visual feedback**: Color-coded tracks, playhead animation
- **Instant gratification**: Click step → hear it next bar
- **No wrong answers**: All scales are consonant, randomize button encourages exploration
- **Preset learning**: "Why does Trap-Soul sound different?" → Fast BPM + 808s

### Music Theory Integration
- Scale selector teaches modes without complexity
- Key transposition shows how same pattern sounds different
- Swing control demonstrates groove/feel (quantization vs human timing)
- Instrument swapping teaches timbre and arrangement

### Classroom-Ready Features
- No account/login required
- Pre-loaded professional drum samples (no upload needed)
- Works offline after initial load (cache Tone.js + samples)
- No inappropriate content/sounds
- Shareable via single HTML file + samples folder

## Common Tasks

### Loading Drum Samples
The app expects pre-loaded samples in `downloads/for app/`:
- **Live kit**: `live-kick.wav`, `live-snare.wav`, `live-hats.wav`, `live-perc.wav`
- **808 kit**: `808-kick.wav`, `808-snare.wav`, `808-hats.wav`, `808-perc.wav`

When kit is swapped (`setKit('live')` or `setKit('808')`), `triggerStep()` should reference the appropriate sample set.

### Change Default Preset
Find `PRESETS.boomBap();` at bottom of script and replace with desired preset name.

### Adjust Reverb Amount
```javascript
FX.reverb = new Tone.Reverb({ decay:3.5, wet:0.25 }).toDestination();
//                                           ^^^ 0=dry, 1=full wet
```

### Add More Steps (32-step sequencer)
1. Change `Array(16)` to `Array(32)` in track initialization
2. Update `grid-template-columns: repeat(16,1fr)` → `repeat(32,1fr)`
3. Modify `scheduleRepeat` to use `'32n'` if needed (or keep 16n for same grid)

### Implement Save/Load
```javascript
function savePattern() {
  const json = JSON.stringify(State);
  localStorage.setItem('soulLabSave', json);
}

function loadPattern() {
  const json = localStorage.getItem('soulLabSave');
  if (json) Object.assign(State, JSON.parse(json));
  applyUI(); // Sync UI to loaded state
}
```
Add buttons to trigger these functions. **Note**: Custom samples won't persist (blob URLs expire).

## Technical Constraints & Gotchas

- **Tone.js must load before script runs** → Use `defer` attribute on CDN script
- **Browser autoplay blocks audio** → Always call `await Tone.start()` on user interaction
- **Transport timing is scheduled in advance** → Use `time` parameter in callbacks, not `Tone.now()`
- **Dispose synths when swapping** → `oldSynth.dispose()` prevents memory leaks
- **CSS grid for sequencer** → Don't use table or flexbox, grid keeps cells square
- **No reactive framework** → Manual `renderSequencer()` calls needed after state changes

## File Structure Reference
```
soul-lab-/
├── index.html          # Main app (all code lives here)
├── downloads/
│   └── for app/        # Pre-loaded drum samples (.wav/.mp3)
│       ├── live-kick.wav
│       ├── live-snare.wav
│       ├── 808-kick.wav
│       └── ...
├── README.md           # Project description
└── .github/
    └── copilot-instructions.md  # This file
```

When adding features, maintain single-file architecture unless project outgrows it (>2000 lines). For modularity, use ES6 modules with `<script type="module">` before splitting files.

## Sound Design Notes

### Iconic Hip-Hop Drums
- **Boom-bap**: Tight kick (short decay), crispy snare (white noise), sparse hi-hats
- **Trap**: Sub-heavy 808 kick (long decay), layered snares, rapid hi-hat rolls (1/32 notes)
- **Live feel**: Humanize timing, add swing (10-20%), use MetalSynth for ride/crash

### Soul/R&B Characteristics  
- **Keys**: Sine/triangle waves, chorus FX, 7th chords (add degree 6 to triads)
- **Bass**: Plucky attack (short envelope attack), slides (portamento), root-fifth patterns
- **Horns**: Staccato stabs (short notes), octave jumps, sawtooth harmonics
- **Guitar**: Pluck synth with high resonance, delay FX for space

### Genre BPM Ranges
- Boom-bap: 85-95 BPM
- Neo-Soul/R&B: 75-95 BPM  
- Trap: 130-150 BPM (often halftime feel)
- Drill/Chicago: 60-70 BPM (feels like 120-140 with double-time hats)

## Future Enhancement Ideas
- **Song mode**: Chain multiple 16-step patterns (A/B/C sections)
- **Effects per track**: Individual reverb/delay sends
- **MIDI export**: Generate downloadable .mid file from patterns
- **Collaborative mode**: Share patterns via URL hash (encode state in base64)
- **Sample packs**: Curated presets using uploaded drum folders
- **Visual waveforms**: Show audio output via AnalyserNode + Canvas API
