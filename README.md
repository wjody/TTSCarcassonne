# Carcassonne v1.23 - 2026 TTS API Compatibility Fix

This is a compatibility patch for the Carcassonne Tabletop Simulator mod that fixes broken functionality in TTS 2024 and later.

## ⚠️ Important Note
This mod was removed from Steam Workshop due to licensing. This repository provides fixes for users who already have the mod saved locally but found it stopped working in modern TTS versions.

## 🐛 Problems This Fixes
- **Green placement markers not appearing** when picking up tiles
- **Tile placement validation not working** (tiles not snapping to grid)
- **Figure placement errors** after placing tiles
- Coroutine errors: "attempt to yield from outside a coroutine"

## 📥 Installation

### For users who already have the mod:

**Windows:**
1. Download `Carcassonne-v1.23.json` from this repository
2. Replace the file at: `%USERPROFILE%\Documents\My Games\Tabletop Simulator\Saves\`
3. **Completely quit TTS** (not just reload - use Alt+F4 or close completely)
4. Restart TTS and load the mod

**Mac:**
1. Download `Carcassonne-v1.23.json` from this repository  
2. Replace the file at: `~/Library/Tabletop Simulator/Mods/Workshop/`
3. **Completely quit TTS** (Cmd+Q - not just reload)
4. Restart TTS and load the mod

## 🔧 Technical Details

Tabletop Simulator underwent breaking Lua API changes between 2023 and 2026. This patch addresses three critical issues:

### 1. Object Type String Change
**Old (2020-2023):** `'Card(Clone) (LuaGameObjectScript)'`  
**New (2024+):** `'Card(Clone) (LuaObject)'`

All object type detection code was updated to use the new naming convention.

### 2. Coroutine API Deprecation
**Old:** `startLuaCoroutine(self, 'showHintMarkers')`  
**New:** `coroutine.wrap(showHintMarkers)()`

The TTS built-in coroutine system was replaced with standard Lua coroutines.

### 3. Physics Engine Timing
Increased delays for modern physics engine:
- `TILE_PLACEMENT_DELAY`: 1s → 2.5s
- `FIGURE_PLACEMENT_DELAY`: 2s → 3s

## 📝 Changes Made

All changes were made to the `LuaScript` section in `Carcassonne-v1.23.json`:

1. Updated 10 occurrences of object type string matching
2. Replaced deprecated `startLuaCoroutine` calls with `coroutine.wrap`
3. Increased timing constants for placement validation

## ✅ Tested With
- Tabletop Simulator 2024-2026
- macOS (should also work on Windows/Linux)
- 2-player pass-and-play (Abbey & Mayor expansion works!)

## 🙏 Credits
- Original mod by DinnerBuffet: https://github.com/DinnerBuffet/TTSCarcassonne
- Continued by mmann78: https://github.com/mmann78/TTSCarcassonne  
- 2026 compatibility fixes by williammandeville

## 📜 License
This is a compatibility patch only. All original mod assets and code retain their original licensing.

## 🎮 Known Limitations
- AI games do not work with Abbey & Mayor expansion (original limitation, not related to this fix)
- This is not an endorsement to pirate the game - buy official Carcassonne if you want to support the creators!
