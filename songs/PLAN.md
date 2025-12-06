# Music AI Video Generator - Complete Workflow Guide

## Overview

This system transforms AI-generated music (with lyrics and mood descriptions) into narrative story-based music videos with characters and storylines. It's adapted from the Pokemon Natural Geographic workflow and maintains the same "Smart Agent + Dumb Scripts" architecture.

## Quick Start

**What you need:**
- AI-generated music file (MP3/WAV)
- Lyrics (text file)
- Mood/genre description
- Optional: styling notes

**What you'll get:**
- Professional music video (2-4+ minutes)
- Character-driven narrative synced to your music
- Beat-synchronized cuts
- Cinematic quality output

---

## 7-Stage Workflow

### Stage 1: Song Analysis & Story Generation (15 min)
**Prompt:** `songs/prompts/1_song_analysis.md`

1. Analyze song structure (intro/verse/chorus/bridge/outro)
2. Extract emotional arc from lyrics
3. Generate 3-5 story concepts with characters
4. Select your preferred story

**Output:** `{artist}/{song}/01_song_analysis.md`

---

### Stage 2: Character & Scene Design (20 min)
**Prompts:** `songs/prompts/2_character_design.md` + `3_scene_breakdown.md`

1. Create detailed character descriptions
2. Define emotional states for each character
3. Break story into 10-20 scenes
4. Map lyrics to visual moments

**Output:**
- `{artist}/{song}/02_character_design.md`
- `{artist}/{song}/03_scene_breakdown.md`

---

### Stage 3: Asset Generation (10-15 min automated)
**Prompts:** `songs/prompts/4_asset_specification.md` + `4.5_generate_assets_agent.md`

**Phase 1:** Generate core character assets + environments
- **Review checkpoint:** Approve core characters before proceeding

**Phase 2:** Generate character variations (using cores as references)
- Ensures consistency across scenes

**Phase 3:** Create composites (character + environment)
- Ready for video generation

**Scripts used:**
- `scripts/generate_asset.py` (Gemini image generation)
- `scripts/create_composite.py` (layering)

**Output:** `{artist}/{song}/assets/` with characters, environments, composites

---

### Stage 4: Beat Mapping (10 min)
**Prompt:** `songs/prompts/5_beat_mapping.md`

1. Run audio analysis (BPM, beat grid, song structure)
2. Map scenes to song timeline
3. Align scene changes to beat boundaries
4. Generate timing JSON

**Script:** `scripts/analyze_audio.py`

**Output:** `{artist}/{song}/05_beat_mapping.json`

---

### Stage 5: Video Prompt Engineering (15 min)
**Prompt:** `songs/prompts/6_video_prompts.md`

1. Create motion prompts for each scene
2. Focus on ONE micro-movement per scene ("breathing photograph")
3. Describe textures in motion (fabric, hair, light)
4. Follow priority: action → details → environment → camera

**Output:** `{artist}/{song}/06_video_prompts.md`

---

### Stage 6: Video Generation (2-4 hours automated)
**Prompt:** `songs/prompts/6.5_generate_videos_agent.md`

1. Upload composites to catbox.moe
2. Generate 10-second clips with Kling 2.5
3. Download generated videos

**Script:** `scripts/generate_video.py`

**Output:** `{artist}/{song}/videos/scene_01.mp4` through `scene_N.mp4`

---

### Stage 7: Final Assembly (3-5 min automated)
**Prompt:** `songs/prompts/7_assemble_final_agent.md`

1. Trim videos to beat timings
2. Concatenate all clips
3. Overlay original song audio
4. Output final MP4

**Script:** `scripts/assemble_music_video.py`

**Output:** `{artist}/{song}/{song_title}_final.mp4`

---

## Folder Structure

```
songs/
├── PLAN.md                            ← You are here
├── prompts/                           ← Workflow prompt files
│   ├── 1_song_analysis.md
│   ├── 2_character_design.md
│   ├── 3_scene_breakdown.md
│   ├── 4_asset_specification.md
│   ├── 4.5_generate_assets_agent.md
│   ├── 5_beat_mapping.md
│   ├── 6_video_prompts.md
│   ├── 6.5_generate_videos_agent.md
│   └── 7_assemble_final_agent.md
└── {artist_name}/                     ← Your song projects
    └── {song_title}/
        ├── input/                     ← Put your music files here
        │   ├── audio.mp3
        │   ├── lyrics.txt
        │   └── mood.txt
        ├── 01_song_analysis.md        ← Generated files
        ├── 02_character_design.md
        ├── 03_scene_breakdown.md
        ├── 04_assets.md
        ├── 05_beat_mapping.json
        ├── 06_video_prompts.md
        ├── assets/                    ← Generated images
        │   ├── characters/
        │   ├── environments/
        │   └── composites/
        ├── videos/                    ← Generated video clips
        └── {song_title}_final.mp4     ← Final output
```

---

## Key Principles

### 1. "Breathing Photograph" Philosophy
Each scene is ONE static moment with subtle motion:
- ✅ Fabric moving in breeze
- ✅ Hair shifting slightly
- ✅ Eyes blinking slowly
- ❌ Running sequences
- ❌ Complex actions
- ❌ Camera whips

### 2. Lore-Grounding Principle
Every visual decision must cite the source material:
- ✅ "Eyes close during lyric: 'shut my eyes and dream'" (cite lyric)
- ✅ "Dark atmosphere matches 'haunted by your ghost'" (cite lyric)
- ❌ "Character randomly smiles" (not in lyrics or mood)

### 3. Visual Atmosphere Block
Define ONCE, use everywhere:
```
"Abandoned grand ballroom, midnight moonlight through broken stained glass,
dust particles suspended in light shafts, cold stone floors, vintage 1920s
decay, dramatic chiaroscuro lighting, cinematic 35mm anamorphic lens..."
```

This block prepends to every asset prompt for consistency.

### 4. Phased Asset Generation
Why: Character variations must look like the SAME character

**Phase 1:** Generate core character (review before continuing)
**Phase 2:** Use core as reference for all variations (ensures consistency)
**Phase 3:** Combine with environments (ready for video)

### 5. Beat-Synchronized Cuts
Scene changes ONLY occur on beat boundaries:
- Verse → Chorus transition aligns with downbeat
- Emotional peaks align with musical peaks
- Timing feels natural and rhythmic

---

## Comparison to Pokemon Workflow

| Aspect | Pokemon | Music Video |
|--------|---------|-------------|
| **Input** | Species name | Audio + lyrics + mood |
| **Duration** | Fixed 90 seconds | Variable 2-4+ minutes |
| **Audio Source** | Generated (ElevenLabs) | Original song |
| **Timing** | 8-second fixed blocks | Beat-synced variable |
| **Structure** | Documentary 3-act | Song structure (verse/chorus) |
| **Characters** | Pokemon creatures | Human/abstract characters |
| **Narration** | Voiceover | Lyrics only (no VO) |
| **Sound Effects** | Generated | None (song complete) |

---

## Cost & Time Estimates

### Per Music Video (3-minute song, 18 scenes)

**Cost:**
- Images: ~30 assets × $0.05 = $1.50
- Videos: ~18 clips × $0.30 = $5.40
- **Total: ~$6.90 per video**

**Time:**
- Active work (manual stages): 60-80 minutes
- Automated wait time: 2-4 hours
- **Total: 3-5 hours** (mostly automated)

---

## Dependencies

### Python Packages
```bash
# Existing (already installed for Pokemon workflow)
google-generativeai>=0.8.0    # Gemini image generation
pillow>=10.0.0                # Image processing
requests>=2.31.0              # HTTP requests
python-dotenv>=1.0.0          # Environment variables

# New (for music video workflow)
librosa>=0.10.0               # Audio analysis (BPM, beats)
soundfile>=0.12.0             # Audio file I/O
```

### External Tools
- FFmpeg + FFprobe (video processing)

### API Keys Required
```bash
GEMINI_API_KEY=your_key_here           # Google Gemini (image generation)
KIE_API_KEY=your_key_here              # Kling 2.5 (video generation)
```

---

## Scripts Reference

### Reusable Scripts (No changes needed)
- `scripts/generate_asset.py` - Generate images with Gemini
- `scripts/create_composite.py` - Overlay characters on environments
- `scripts/generate_video.py` - Generate videos with Kling 2.5

### New Scripts (Music-specific)
- `scripts/analyze_audio.py` - Beat detection, BPM analysis
- `scripts/sync_scenes_to_audio.py` - Map scenes to timeline
- `scripts/assemble_music_video.py` - FFmpeg video assembly

---

## Example Workflow: "Neon Dreams"

**Song:** 3-minute electronic track (BPM 128)

1. **Song Analysis (15 min):**
   - Generated 3 stories (cyberpunk romance, AI awakening, digital escape)
   - Selected: "AI awakening"

2. **Character Design (20 min):**
   - Ada (holographic AI), Marcus (programmer)
   - 16 scenes planned

3. **Asset Generation (12 min):**
   - Phase 1: Core Ada + Marcus + 6 environments → Approved
   - Phase 2: 8 character variations
   - Phase 3: 16 composites

4. **Beat Mapping (10 min):**
   - Detected 128 BPM, mapped 16 scenes to timeline

5. **Video Prompts (15 min):**
   - Wrote motion prompts for all 16 scenes

6. **Video Generation (3 hours):**
   - Generated 16 clips (automated)

7. **Assembly (4 min):**
   - Final video: `neon_dreams_final.mp4`

**Total:** 4 hours (1 hour active work)

---

## Troubleshooting

### Issue: Character consistency problems
**Solution:** Ensure Phase 1 core asset is approved before Phase 2. All variations must use the core as reference.

### Issue: Beat timing feels off
**Solution:** Manually adjust `05_beat_mapping.json` scene timings. Scene changes should align with downbeats.

### Issue: Motion looks unnatural
**Solution:** Follow "breathing photograph" principle. One subtle movement per scene. Avoid complex actions.

### Issue: Video generation fails
**Solution:** Check composite image is 1920x1080 (16:9). Verify motion prompt is clear and under 200 words.

---

## Review Checkpoints

The workflow includes 5 review points:

1. **After song analysis:** Approve story concept
2. **After character design:** Approve character descriptions
3. **After Phase 1 assets:** Approve core character images
4. **After beat mapping:** Verify scene timings feel natural
5. **After video prompts:** Approve motion descriptions

These checkpoints enable iterative refinement at each stage.

---

## Next Steps

1. Install new dependencies: `pip install librosa soundfile`
2. Create your first song project folder: `songs/{artist}/{song}/input/`
3. Add your music files: `audio.mp3`, `lyrics.txt`, `mood.txt`
4. Run Stage 1: `songs/prompts/1_song_analysis.md`
5. Follow the 7-stage workflow

---

## Additional Resources

- Pokemon workflow (for reference): `prompts/` folder
- Example prompts: Study Pokemon prompt files for patterns
- Script documentation: See `scripts/README.md` (to be created)

---

**Last Updated:** 2025-12-05
**Version:** 1.0.0
