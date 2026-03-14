# Carcassonne v1.23 - 2026 TTS Compatibility Fix

Updated version of the best Carcassonne mod for Tabletop Simulator, fixed to work with modern TTS (2024+).

## 🎮 What This Is

This is the comprehensive Carcassonne mod that was removed from Steam Workshop, now updated to work with current versions of Tabletop Simulator. It includes virtually every expansion and is heavily automated - by far the best way to play Carcassonne online.

## 🐛 What Was Fixed

The original mod stopped working in TTS 2024+ due to API changes:
- Green placement markers weren't appearing when picking up tiles
- Tile placement validation broken (tiles not snapping to grid)
- Figure placement errors
- Coroutine errors in the console

All fixed in this version!

## 📥 Installation

### Easy Method (For Beginners)

**Step 1: Download the file**
- Click on `Carcassonne-v1.23.json` above
- Click the "Download" button (or right-click "Raw" → "Save Link As")

**Step 2: Find where to put it**

**On Windows:**
1. Open File Explorer
2. In the address bar, type: `%USERPROFILE%\Documents\My Games\Tabletop Simulator\Saves`
3. Press Enter
4. Copy `Carcassonne-v1.23.json` into this folder

**On Mac:**
1. Open Finder
2. Press **Cmd+Shift+G** (Go to Folder)
3. Type: `~/Library/Tabletop Simulator/Mods/Workshop/`
4. Press Enter
5. Copy `Carcassonne-v1.23.json` into this folder

**Step 3: Restart Tabletop Simulator**
- **IMPORTANT:** Completely quit TTS (don't just reload)
  - Windows: Alt+F4 or File → Exit
  - Mac: Cmd+Q
- Start TTS again

**Step 4: Load the game**
1. In TTS, click **Games** (top menu)
2. Click **Saved Games**
3. Find "Carcassonne v1.23" and click it
4. Click **Load**

Done! The green markers should now appear when you pick up tiles.

### Advanced Method (Using Git)

If you're comfortable with git:

```bash
# Clone this repository
git clone https://github.com/yourusername/TTSCarcassonne.git

# Copy the mod file to TTS directory
# On Mac:
cp TTSCarcassonne/Carcassonne-v1.23.json ~/Library/Tabletop\ Simulator/Mods/Workshop/

# On Windows (in PowerShell):
# copy TTSCarcassonne\Carcassonne-v1.23.json "$env:USERPROFILE\Documents\My Games\Tabletop Simulator\Saves\"

# Completely quit and restart TTS
```

## 🎲 How to Play

1. Start a new game or load saved games
2. **For AI opponents:** Most expansions work, but Abbey & Mayor doesn't support AI (original limitation)
3. **For human multiplayer:** Everything works great in pass-and-play or online multiplayer
4. Green markers will appear showing valid tile placements when you pick up a tile during your turn

## 🔧 Technical Details (For Developers)

Tabletop Simulator underwent breaking Lua API changes between 2023 and 2026. This update addresses three critical issues:

### 1. Object Type String Change
**Before (2020-2023):** `'Card(Clone) (LuaGameObjectScript)'`  
**After (2024+):** `'Card(Clone) (LuaObject)'`

Updated all object type detection code to use the new naming convention (10 occurrences).

### 2. Coroutine API Deprecation  
**Before:** `startLuaCoroutine(self, 'showHintMarkers')`  
**After:** `coroutine.wrap(showHintMarkers)()`

TTS deprecated the built-in coroutine system in favor of standard Lua coroutines.

### 3. Physics Engine Timing
Increased delays for modern physics processing:
- `TILE_PLACEMENT_DELAY`: 1.0s → 2.5s
- `FIGURE_PLACEMENT_DELAY`: 2.0s → 3.0s

### Apply the Fix Yourself

If you have an older version and want to apply the fix manually:

```bash
# Use the provided Perl script (requires Perl installed)
perl fix_carcassonne_api.pl < old-version.json > fixed-version.json
```

Or manually edit the LuaScript in the JSON:
1. Find all instances of `'Card(Clone) (LuaGameObjectScript)'` → replace with `'Card(Clone) (LuaObject)'`
2. Find `startLuaCoroutine(self, 'showHintMarkers')` → replace with `coroutine.wrap(showHintMarkers)()`  
3. Update timing constants as shown above

## ❓ Troubleshooting

**Green markers still not appearing:**
- Make sure you **completely quit** TTS (not just reload)
- Verify the file is in the correct location
- Check TTS console (` key) for errors

**"Mod not found" when loading:**
- The file must be in the Saves or Workshop folder (not both)
- File name must be exactly `Carcassonne-v1.23.json`

**Tile placement still broken:**
- Try during your actual turn (not setup phase)
- Make sure you're picking up the tile from the draw pile, not manually placing

**For other issues:**
- Open TTS console with the ` key (backtick, above Tab)
- Look for red error messages
- Feel free to open an issue on this repo

## ✅ Tested With
- Tabletop Simulator v13.3+ (2024-2026)
- macOS Sonoma & Windows 11
- 2-6 player games (pass-and-play and online multiplayer)
- All expansions except AI with Abbey & Mayor

## 🙏 Credits
- **Original mod:** DinnerBuffet - https://github.com/DinnerBuffet/TTSCarcassonne
- **Continued development:** mmann78 - https://github.com/mmann78/TTSCarcassonne  
- **2026 compatibility fix:** williammandeville

This mod represents hundreds of hours of work from the community. Huge thanks to everyone who contributed to making this the definitive way to play Carcassonne online.

## 📜 Note
This is a preservation effort for a mod that was removed from Steam Workshop. We're keeping it alive for personal use among friends and family who enjoyed it during the pandemic and beyond.
