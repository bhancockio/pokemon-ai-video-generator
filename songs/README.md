# Music AI Video Generator - Quick Start

## Setup for a New Song

### 1. Create Song Folder Structure

```bash
# Replace {artist} and {song} with your values
mkdir -p songs/{artist}/{song}/input
```

Example:
```bash
mkdir -p songs/taylor_swift/wildest_dreams/input
```

### 2. Add Your Input Files

Place these files in `songs/{artist}/{song}/input/`:

- **audio.mp3** - Your song audio file
- **lyrics.txt** - Song lyrics (one verse/chorus per section)
- **mood.txt** - Brief description (genre, themes, visual style)

Example `mood.txt`:
```
Genre: Cinematic Pop
Themes: Nostalgia, fleeting romance, golden hour aesthetics
Visual Style: 1950s Hollywood glamour, warm desert landscapes
Mood: Bittersweet, dreamy, romantic
```

### 3. Follow the 7-Stage Workflow

Use the prompt files in `songs/prompts/` in order:

1. **Stage 1** - `1_song_analysis.md` (15 min manual)
   - Analyzes song structure
   - Generates 3-5 story concepts
   - You select one

2. **Stage 2** - `2_character_design.md` (15 min manual)
   - Creates detailed character descriptions
   - Defines visual atmosphere

3. **Stage 3** - `3_scene_breakdown.md` (20 min manual)
   - Breaks story into scenes
   - Maps lyrics to visuals

4. **Stage 4** - `4_asset_specification.md` + `4.5_generate_assets_agent.md` (15 min automated)
   - Creates asset manifest
   - Generates all images (characters, environments, composites)

5. **Stage 5** - `5_beat_mapping.md` (10 min semi-automated)
   - Analyzes audio for beats/BPM
   - Maps scenes to precise timestamps

6. **Stage 6** - `6_video_prompts.md` + `6.5_generate_videos_agent.md` (3-4 hours automated)
   - Creates motion prompts for each scene
   - Generates all video clips with Kling 2.5

7. **Stage 7** - `7_assemble_final_agent.md` (5 min automated)
   - Assembles final music video
   - Syncs video to audio

### 4. Output

Final video will be saved as:
```
songs/{artist}/{song}/{song}_final.mp4
```

## Example Complete Workflow

```bash
# 1. Create folder
mkdir -p songs/my_artist/my_song/input

# 2. Add your files
cp ~/Downloads/my_song.mp3 songs/my_artist/my_song/input/audio.mp3
# Create lyrics.txt and mood.txt

# 3. Start Stage 1
# Open songs/prompts/1_song_analysis.md and follow instructions

# 4. Continue through all 7 stages
# Each stage builds on the previous one
```

## File Structure After Completion

```
songs/my_artist/my_song/
├── input/
│   ├── audio.mp3
│   ├── lyrics.txt
│   └── mood.txt
├── 01_song_analysis.md
├── 02_character_design.md
├── 03_scene_breakdown.md
├── 04_assets.md
├── 05_beat_mapping.json
├── 06_video_prompts.md
├── assets/
│   ├── characters/
│   ├── environments/
│   └── composites/
├── videos/
│   └── scene_*.mp4
└── my_song_final.mp4
```

## Prerequisites

- Python 3.10+ with dependencies installed (`uv sync`)
- FFmpeg installed
- Gemini API key (for image generation)
- Kling AI account (for video generation)
- API keys configured in `.env`

## Time Estimate

- Active work: ~1.5 hours (manual stages)
- Automated processing: ~4-5 hours (asset + video generation)
- Total: ~5-6 hours per song

## Tips

- Review outputs at each stage before proceeding
- Adjust and regenerate if needed
- Start with a 2-3 minute song for first test
- Keep lyrics file formatted clearly (verse/chorus labels)
