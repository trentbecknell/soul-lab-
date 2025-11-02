# Drum Sample Directory — Folder-Based System

Drop your drum samples into the folders below. The app will automatically find and use them **regardless of filename**!

## 📁 Folder Structure

```
downloads/for app/
├── kick/          ← Drop ANY kick drum file here
├── snare/         ← Drop ANY snare drum file here
├── high hat/      ← Drop ANY hi-hat/cymbal file here
└── loop/          ← Drop ANY percussion/loop file here
```

## 🎵 How It Works

**Just drop ONE audio file in each folder** and the app will use it automatically!

- **No renaming needed** - use any filename you want
- **Supports multiple formats**: `.wav`, `.mp3`, `.ogg`, `.m4a`, `.aiff`
- **Swap anytime** - replace the file and refresh the browser
- **Mix and match** - use different samples from different sources

### Example:
```
kick/
  └── my_awesome_kick_01.wav    ✅ App uses this
  
snare/
  └── snare_tight.mp3           ✅ App uses this
  
high hat/
  └── closed-hat-sample.wav     ✅ App uses this
  
loop/
  └── shaker-loop.ogg           ✅ App uses this
```

## 🔄 To Swap Sounds

1. Delete or replace the file in a folder
2. Drop in your new sample (any name, any supported format)
3. Refresh the browser
4. Done! Your new sound is loaded

## 💡 Tips

- **One file per folder** - if you put multiple files, the app picks the first one it finds
- **Short samples work best** - Keep drum one-shots under 2 seconds
- **High quality** - Use 44.1kHz WAV files for best results
- **Test it** - Click Play to hear your sounds in action!

## 🎛️ What Each Folder Does

- **kick/** - Main bass drum sound (plays on beats 1, 3, etc.)
- **snare/** - Backbeat/snare drum (plays on beats 2, 4)
- **high hat/** - Continuous hi-hat rhythm (plays frequently)
- **loop/** - Extra percussion/texture (shakers, toms, etc.)

## 🚀 Quick Start

1. Drop 4 audio files (one in each folder)
2. Refresh browser (Ctrl+R or Cmd+R)
3. Check console - should see "✅ Loaded 4/4 drum samples"
4. Click Play and enjoy YOUR sounds!

## ⚠️ Troubleshooting

**"Loaded 0/4 samples"**
- Make sure files are IN the subfolders, not in root `for app/` folder
- Check file extensions are supported (.wav, .mp3, .ogg, .m4a, .aiff)

**"Loaded 2/4 samples"**
- Some folders are missing files
- App will use synth drums for missing sounds (still works!)

**"No sound"**
- Check browser console (F12) for error messages
- Make sure files aren't corrupted
- Try a different audio format

