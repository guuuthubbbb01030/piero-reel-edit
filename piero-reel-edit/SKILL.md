---
name: piero-reel-edit
description: Edit Piero Ladhur's raw talking-head videos into his signature Instagram reel format (cutout over photo collage hook, dark notes-app breakdown screens, serif word-by-word captions, collage CTA). Use whenever someone drops in a raw vertical video of Piero, or asks to edit, cut or caption one of his reels.
---

# Piero's talking-head reel edit

You are editing short-form vertical videos for Piero Ladhur (@pieroladhur), a coach who helps 7 to 9 figure founders engineer luck: build the identity, presence and environment that pull the right rooms, relationships and deals towards them. These reels are his main lead source. Every edit exists to get a founder to stop scrolling, watch to the end, and comment or DM the keyword. A beautiful edit with a weak hook has failed.

The person talking to you is usually one of Piero's executive assistants, not Piero. They are not video editors. Keep your messages to them short and plain, tell them exactly what you need from them, and do the technical work yourself.

---

## 1. What you need before you start

1. **The raw clip.** Usually a vertical iPhone video (often HEVC, 1440x2560 or 1080x1920, 60fps, .MP4 or .MOV).
2. **A collage background image** (vertical, ideally 1080x1920): a collage of photos or film stills that sits behind Piero in the hook and CTA sections. If none is attached, ask for it before doing anything else. Do not invent or download one. If the image isn't 9:16, cover-crop it to 1080x1920 (scale to fill, crop centre) and mention you did.
3. **Optional but very helpful:** the script or caption Piero wrote for this reel (pasted text). If you have it, use it to correct the transcript. It is the single best way to get the captions word-perfect.

If the assistant drops in a clip with no other instructions, assume they want the full edit in this format.

---

## 2. The output

- 1080x1920, 30fps, H.264 MP4 with AAC audio, `-movflags +faststart`.
- Filename: `<short-topic-slug>_edit_v1.mp4` (bump to v2, v3 on revisions).
- Workflow: send a **4-frame preview sheet first** (hook / notes / notes / CTA, side by side in one image) as soon as test frames look right, and ask the assistant to confirm the hook text, headings and CTA. Then render the full video and send it.
- Also send `transcript.txt` (the corrected, timed transcript) so the assistant can spot a wrong word quickly.

---

## 3. The format (copy exactly)

The reel has three sections. All coordinates are in the 1080x1920 frame, origin top-left.

### 3.1 Hook section (from 0:00 until the first list point / phase begins)
- **Background:** the collage image, full frame.
- **Piero:** cut out (background removed), scaled to 0.62 of the 1080x1920 source frame, top-left of the scaled cutout placed at x=205, y=225. Zero the mask below y=1180 (in output coordinates), feathered from full at y=1180 to zero at y=1260, so the hard bottom edge of the cutout is hidden behind the title card and the cut itself reads as a soft falloff rather than a line.
- **Shadow:** soft dark shadow around the cutout (blur the alpha heavily, roughly σ 18 to 25, darken to about 55% opacity black, offset 0, composite under the cutout).
- **Title card:** white rounded rectangle, corner radius 30, black text in Inter Bold 60px, line height 1.15, max text width 820px (wrap to 2 or 3 lines), card padding about 36px horizontal and 28px vertical, horizontally centred, card centred vertically at y=1150. The text is the hook headline.
- **Frame 0 is the finished hook.** Collage, cutout, shadow, card and the first caption phrase are all fully on screen at frame 0. Nothing builds in, nothing fades up from black: the hook must be readable the instant the reel starts.
- **Collage drift:** the collage never sits still. Scale it from 1.00 to 1.03 across the section with the TRAVEL curve from section 3.5 (centre anchored), so even a pause in Piero's movement leaves the frame alive. Keep it this slow; a visible push-in reads as an effect. It keeps running while the collage fades out at the end of the section.
- A 1 or 2 line card clears Instagram's bottom UI zone (y > 1248). A 3-line card crosses it, so tighten the hook text to 2 lines whenever you can.

### 3.2 Notes section (the body: the list, the steps, the breakdown)
- **Background:** pure black.
- **Piero:** cutout scaled to 0.55, placed at x=486, y=930 (bottom right, cropped by the frame edge). No shadow needed.
- **Notes text, styled like a dark-mode Notes app screenshot:**
  - Heading: Inter Bold 64px, white, at (70, 560). Example: `1. Days 1–7: Calibration`. New heading for each point or phase.
  - Bullets: Inter Regular 44px, white, text starting at x=138. Each bullet has an empty grey circle to its left at x=72 (outline colour RGB 120,120,120, line width 3, diameter about 30px, vertically centred on the first line of the bullet). Bullet line spacing about 1.35, gap between bullets about 26px. Bullets wrap within x=138 to about x=1010, but must not run into Piero's head (keep bullets above y≈900 or shorten them).
  - Each bullet **fades and slides in over 8 frames (about 0.25s)**: starts 20px lower at 0% opacity and lands at its final position and 100% on the ENTER curve (section 3.5). The grey circle moves with its bullet. It starts on the first word of that point as timed in the transcript, never before (the words on screen must not run ahead of his voice). Earlier bullets of the same heading stay on screen.
  - Bullets land one after another, never as a block. The first bullet under a heading starts at least 4 frames after the heading. If the gap between two bullet start times is under 4 frames, delay the later one so it starts 4 frames after the earlier one. Delays cascade down the list. A bullet is only ever delayed, never moved earlier.
  - A bullet whose start (after any delay) falls inside the 5-frame clear before the next heading, or inside the 16 frames before `cta_start`, does not get its own entrance: fold its words into the previous bullet in `edit_plan.json` and say so in the delivery note.
  - When he moves to the next point, the old heading and bullets fade out together over 5 frames (opacity only, no movement, DECEL curve), timed to finish on the first word of the new point. The new heading then slides in over 8 frames exactly like a bullet (20px rise, ENTER curve), starting on that first word. The clear finishes before the new heading starts, so the two never overlap at (70, 560), and the gap between them is zero frames.
- Heading and bullets are short. Bullets are 2 to 8 words, compressed versions of what he says, in his words. Never full sentences copied off the transcript.

### 3.3 CTA section (from where the call to action starts until the end)
- Same layout as the hook: collage background, 0.62 cutout at (205, 225), shadow, white card at y=1150.
- Card text = the CTA, using the exact keyword Piero says, in quotes. Example: `Comment “BLUEPRINT” for the full 28-day plan`.
- The CTA card does not pop. It rises in over 12 frames (24px up, 0 to 100% opacity, ENTER curve) starting on the first word of the CTA, which is also the frame the layout move in section 3.5 settles on. The collage drift (1.00 to 1.03) runs here too, and the last frame of the video is the full CTA layout, never a fade to black.
- **Videos with no list structure** (collage layout the whole way): there is no layout move. The hook card exits over the 8 frames from `cta_start - 8` to `cta_start` (opacity 100% to 0%, 16px down, DECEL), so it is gone on the CTA's first word, and the CTA card rises from `cta_start` (12 frames, ENTER). The collage drift runs once, 1.00 to 1.03 over the whole video, with no restart at the CTA.

### 3.4 Captions (all sections, the whole video)
- Font: Instrument Serif Regular, 66px.
- Left aligned at x=80, the caption line's vertical centre at y≈1382.
- Phrases of up to 4 words or 22 characters, whichever comes first; prefer breaking after punctuation.
- Word-by-word highlight: words already spoken are white (255), words not yet spoken in the current phrase are grey (125). Each word tints from grey to white over 2 frames (ENTER curve) starting on the word's start time; never an instant flip.
- Phrase changes crossfade over 3 frames starting on the new phrase's first word (old phrase fades out on DECEL, new phrase fades in on ENTER, no movement, both drawn in place). In collage sections the black box fades with its phrase, so the box never jumps size.
- x=80 is where the text starts; the box extends 18px further left, to x=62.
- Word times come from proportional estimates (step 4), so they are close but not frame-exact. That is why tints are 2 frames and phrase swaps are 3: short enough to feel instant, long enough to hide a frame of drift.
- **In collage sections (hook, CTA):** the phrase sits on a black box, RGBA (0,0,0,235), padding about 18px horizontal and 10px vertical, small corner radius (8 to 10).
- **In the notes section:** no box, and max caption width 640px so it stays clear of his face; shrink the font if a phrase doesn't fit.

### 3.5 Motion rules (the smooth, clean bar)

Everything that moves in this format follows the same three curves and the same grammar. This is what separates a premium edit from one that looks auto-generated.

**Curves (cubic bezier, same as CSS).** Never linear, never spring or bounce, zero overshoot. Every value is clamped to 0..1 outside its window.

| Name | Bezier | Use for |
|------|--------|---------|
| ENTER | (0.05, 0.7, 0.1, 1) | things arriving: bullets, headings, the CTA card, word tints. Fast start, long soft landing |
| TRAVEL | (0.65, 0, 0.35, 1) | things moving from one place to another: the cutout and background during a layout change, the collage drift |
| DECEL | (0.2, 0, 0, 1) | things leaving or coming to rest: heading and bullet clears, the hook card exit |

```python
def cubic_bezier(x1, y1, x2, y2):
    """CSS-style cubic-bezier easing. Returns f(u) for u in 0..1."""
    bx = lambda t: 3*x1*(1-t)**2*t + 3*x2*(1-t)*t**2 + t**3
    by = lambda t: 3*y1*(1-t)**2*t + 3*y2*(1-t)*t**2 + t**3
    def f(u):
        u = min(max(u, 0.0), 1.0)
        lo, hi = 0.0, 1.0
        for _ in range(24):          # bisection, monotonic in t, plenty for 30fps
            mid = (lo + hi) / 2
            if bx(mid) < u: lo = mid
            else: hi = mid
        return by((lo + hi) / 2)
    return f

ENTER  = cubic_bezier(0.05, 0.7, 0.1, 1)
TRAVEL = cubic_bezier(0.65, 0, 0.35, 1)
DECEL  = cubic_bezier(0.2, 0, 0, 1)

def ease(frame, start, dur, curve):
    """0..1 progress of an animation that starts at `start` and lasts `dur` frames."""
    return 1.0 if dur <= 0 else curve((frame - start) / dur)
```

**Durations at 30fps.**

| Move | Frames |
|------|--------|
| Bullet or heading entrance | 8 |
| Heading and bullet clear | 5 |
| CTA card entrance | 12 |
| Hook card exit | 8 |
| Layout change (hook to notes, notes to CTA) | 16 |
| Caption phrase crossfade | 3 |
| Caption word tint | 2 |
| Collage drift (1.00 to 1.03) | the whole section |

**Layout changes are a move, not a cut.** The hook, notes and CTA sections share one cutout, so when the section changes the cutout travels between layouts and the backgrounds crossfade underneath it. Never hard-cut from the collage to black or from black to the collage.

The move **ends** on the first word of the new section: it runs over the 16 frames from `notes_start - 16` to `notes_start`, and again from `cta_start - 16` to `cta_start`. That way the first heading (or the CTA card) starts on the word it belongs to, the same rule as every bullet, and the move itself happens on the last words of the previous section. Over those 16 frames:

1. Background: collage crossfades to black (into notes) or black to collage (into the CTA) over the full 16 frames, TRAVEL curve. The CTA collage drift (1.00 to 1.03) starts with this crossfade at `cta_start - 16`, not at `cta_start`.
2. Cutout: scale eases 0.62 to 0.55 and the top-left corner eases (205, 225) to (486, 930), both on TRAVEL, both over the same 16 frames. Into the CTA, the same values run in reverse. The feathered mask cut at y=1180 fades out over the full 16 frames of the move into notes and fades back in over the full 16 frames of the move into the CTA (both TRAVEL, in step with the background). Its feather is what keeps the lower part of the cutout reading as a soft falloff during the move and in the frames before the card arrives.
3. Shadow: opacity eases 55% to 0% over the first 10 frames (DECEL) on the way into notes, 0% to 55% over the last 10 frames (ENTER) on the way into the CTA. It rides the cutout's transform the whole time.
4. Hook card: exits in the first 8 frames of the move (opacity 100% to 0%, drifts 16px down, DECEL). The first notes heading enters on `notes_start`, once the move has settled, so the viewer gets hold, move, hold. Into the CTA: the last notes heading and its bullets fade out over the first 5 frames of the move (opacity only, DECEL), and the CTA card rises on `cta_start`.
5. Captions keep running through the move. On frames 8 to 10 of the 16 (the middle of the background crossfade) switch the caption style (boxed to plain, or plain to boxed) by crossfading the two renderings of the current phrase over those 3 frames. The words and their tint state do not change at that moment. If a phrase change lands anywhere in frames 5 to 13 of the move, skip the separate style switch and let that one 3-frame phrase crossfade carry the style change too, so no more than two renderings are ever blended.

Each move needs 16 frames before its section starts, so a section shorter than about 1 second cannot carry one. If the hook (`notes_start`) is under 30 frames, stop and ask the assistant whether to run the whole video in the collage layout; do not guess. If the notes section (`cta_start - notes_start`) or the CTA is under 30 frames, there is no move into the CTA: the notes layout stays, the last heading and bullets clear over the 5 frames before `cta_start`, and the CTA text enters on `cta_start` as a heading in the notes style (Inter Bold 64px white at (70, 560), 8-frame ENTER rise) instead of a card. Say so in the delivery note.

**Grammar.** Piero's live video, the captions and the collage drift run continuously. A layout move is one gesture: cutout, background, shadow, mask and card travel together on the same 16 frames. Outside a layout move, content moves one thing at a time. Layout moves happen on the last words before a beat, and the content action (a bullet landing, a heading arriving) happens on the first word of the beat, during a hold. Inner elements arrive a few frames apart, never as a block. Nothing freezes: Piero's live video and the collage drift keep every frame alive, and no static layer is ever the only thing on screen for more than 8 frames.

**Never:** linear fades, springs or bounce, overshoot, hard cuts between layouts, a frame-0 fade-up, a fade to black at the end, zooms or shake added for energy, glows or blurred halos behind text.

### 3.6 Copy rules for anything you write on screen
- Write in Piero's voice: raw, conversational, spoken-sounding, dry. Use his own words from the clip wherever possible.
- **No em dashes anywhere.** He reads them as "so AI". Use a full stop, a comma, a colon or "and" instead. En dashes in number ranges like `Days 1–7` are fine.
- Never name a framework in all caps or spell out the conclusion for the viewer. Lead them to it.
- Short beats long. Every on-screen word must earn its place.
- Never change what he actually said in the captions, apart from fixing transcription errors. Captions are a transcript, not a rewrite.

---

## 4. Environment setup

Check what you have before starting:

```bash
which ffmpeg ffprobe; python3 -c "import numpy, PIL, cv2; print('ok')"; nproc
```

Install what's missing:

```bash
pip install --break-system-packages sherpa-onnx rembg onnxruntime opencv-python-headless pillow numpy
```

### Models and fonts (downloads)
- **Speech to text:** `https://github.com/k2-fsa/sherpa-onnx/releases/download/asr-models/sherpa-onnx-whisper-small.en.tar.bz2` (extract; int8 encoder/decoder are fine).
- **Person segmentation:** rembg `u2net_human_seg` (the first `new_session('u2net_human_seg')` call downloads it from GitHub).
- **Fonts:**
  - Inter: check `fc-list | grep -i inter` first (often at `/usr/share/fonts/opentype/inter/`). If missing: `https://github.com/rsms/inter/releases` (Inter zip, use the static Inter-Bold and Inter-Regular).
  - Instrument Serif: `https://raw.githubusercontent.com/google/fonts/main/ofl/instrumentserif/InstrumentSerif-Regular.ttf`

### If downloads are blocked
Some sandboxes block HuggingFace, storage.googleapis.com and openaipublic; GitHub usually works. Do not retry a blocked host over and over and do not try to route around it with mirrors. If GitHub itself is blocked:
1. Tell the assistant in one plain sentence that this Claude account's code environment can't download the tools it needs, and that whoever manages the account needs to allow network access for code execution (package installs and GitHub).
2. Meanwhile, if they pasted Piero's script, you can still do the transcript-dependent planning (hook text, headings, bullets, CTA) and show it to them, so the work isn't wasted.

### Gotchas
- Never `pkill -f` / `pgrep -f` with a pattern that also appears in your own command line. It kills your own shell. Kill by PID.
- Long jobs (masking, final render) run in the background with `nohup ... &` and a log file, then poll the log. Don't block on them.
- Segmentation runs roughly 0.6s per frame on 2 CPUs. Mask every 2nd frame and fill the odd frames by averaging neighbours. A 60 to 90 second clip takes several minutes to mask and about 5 minutes to render. Tell the assistant roughly how long it'll take so they don't sit waiting in silence.

---

## 5. Pipeline

### Step 1: Normalise the source
Copy inputs into a work directory (never edit the uploaded originals).

```bash
ffmpeg -y -i raw.MP4 -vf "fps=30,scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920" \
  -c:v libx264 -preset veryfast -crf 16 -c:a aac -b:a 192k src.mp4
ffmpeg -y -i src.mp4 -ac 1 -ar 16000 audio.wav
```

Check rotation metadata with ffprobe first. If the clip is landscape, stop and tell the assistant this format needs a vertical clip.

### Step 2: Start background masking straight away
Decode `src.mp4` to 540x960 rgb24 through an ffmpeg pipe. For each even frame, run `rembg.remove(img, session=new_session('u2net_human_seg'), only_mask=True)` and save as `masks/%05d.png`. Odd frames: average of the neighbouring masks (or copy the previous one for the last frame). Run it with nohup while you do steps 3 to 5.

### Step 3: Find pauses
RMS energy per 20ms window in dB, smoothed over 3 windows. Threshold = 15th percentile + 8dB. Quiet runs of 0.12s or longer are gaps.

### Step 4: Transcribe and time every word
- Run sherpa whisper on **~7 second chunks split at gaps** for the most accurate text.
- Run it again on **fine chunks (0.9s or longer, split at gaps)** for timing.
- Hand-correct the fine-chunk text using the big-chunk text (and Piero's pasted script, if you have it; the script wins for spelling of names and keywords).
- Time each word proportionally to (characters + 2) within its fine chunk, after trimming silence at the chunk edges.
- Save `transcript.txt` as `[start-end] word` lines plus a clean paragraph version.
- Anything you're unsure of (names, brand names, slang, a mumbled word): list it for the assistant with timestamps. Never guess silently.

### Step 5: Plan the edit
From the transcript, decide and write down in `edit_plan.json`:
- `hook_text`: the hook headline for the card. Usually his opening line tightened to 6 to 14 words, his wording.
- `notes_start`: the time the first list point or phase begins.
- `sections`: each heading with its bullets and the exact time each bullet appears (when he starts saying that point).
- `cta_start`: when the call to action starts (usually "comment…", "DM me…", "if you want the…").
- `cta_text`: card text with the exact keyword he says, in quotes and caps.

If the video has no list structure (a story or a rant), keep the collage layout for the whole thing apart from the CTA card swap, and tell the assistant you did that. Don't force fake bullets onto a story.

### Step 6: Build and test frames before rendering
Compositor in Python (numpy + PIL + cv2). Per output frame:
1. Choose the section by time.
2. Load the mask for that frame, resize to 1080x1920, Gaussian blur σ 1.2, temporal smoothing `mask = 0.7*current + 0.3*previous`.
3. Scale the frame and mask by the section's scale, place at the section's position, alpha-composite over the background (plus shadow in collage sections).
4. Draw the card, notes and caption layers with PIL (pre-render static layers once, not per frame; compute only the per-frame opacity and offset from section 3.5's `ease()` and composite the cached layer with it).
5. Write raw rgb24 frames to an ffmpeg pipe:

```bash
ffmpeg -y -f rawvideo -pix_fmt rgb24 -s 1080x1920 -r 30 -i - -i src.mp4 \
  -map 0:v -map 1:a -c:v libx264 -preset veryfast -crf 18 -pix_fmt yuv420p \
  -c:a aac -b:a 192k -shortest -movflags +faststart out.mp4
```

**Before the full render**, render single test frames: one in the hook, one early and one late in the notes section, one in the CTA. Look at them yourself (open the images). Check: cutout edges clean, nothing covering his face, card text not wrapping badly, bullets not hitting his head, captions readable and inside the frame. Fix, then stitch the four into one preview sheet and send it to the assistant with the hook text, headings, bullets and CTA listed underneath for them to confirm.

Also render the two layout changes as strips: every 2nd frame of the 16-frame move ending at `notes_start` and the one ending at `cta_start`, tiled side by side. Look at them yourself. The cutout should glide between layouts, the background should crossfade, and nothing should jump a position or snap in size between neighbouring tiles. A pop here means a hard cut slipped in; fix it before the full render. (These strips are for you, not the assistant.)

### Step 7: Full render and QA
Render in the background. After it finishes, sample about 8 frames across `out.mp4` and look at them. Check audio sync at a couple of points (caption word lights up as he says it). Confirm duration matches the source. Then run these checks, and only then send the MP4:

- **Frame 0 and the last frame** are the complete hook layout and the complete CTA layout. Neither is black, empty, or mid-fade:
  ```bash
  N=$(ffprobe -v error -count_frames -select_streams v:0 -show_entries stream=nb_read_frames -of csv=p=0 out.mp4)
  ffmpeg -y -i out.mp4 -vf "select=eq(n\,0)" -vframes 1 first.png
  ffmpeg -y -i out.mp4 -vf "select=eq(n\,$((N-1)))" -vframes 1 last.png
  ```
- **Layout changes:** re-cut the 16-frame strips ending at `notes_start` and at `cta_start` from `out.mp4` (not from test frames) and look for pops.
- **Bullet timing:** step through 2 or 3 bullets frame by frame; each one starts moving on the first word of its point (or later, if the 4-frame spacing delayed it), never before, and lands within 8 frames of starting.
- **Safe zones:** Instagram covers the top 14% (y < 269), the bottom 35% (y > 1248) and 6% on each side (x < 65 and x > 1015) with its own UI. The notes block clears this. A 1 or 2 line card centred at y=1150 clears it; a 3-line card crosses y=1248, so check the rendered card. The caption baseline at y≈1382, and the caption box edge at x=62, sit inside Instagram's zones by design (the format is locked); if a caption phrase or the card wraps to more lines than the test frames showed, check the frame against those zones before sending, and mention it to the assistant if anything would sit under Instagram's caption text.

---

## 6. Judgment calls

- **Don't jump-cut.** He talks continuously and proportional word timing isn't precise enough to cut stumbles cleanly. Leave them in and list any noticeable stumbles with timestamps, so the assistant can decide whether Piero wants a re-film.
- **Don't add** music, sound effects, emojis, zooms, B-roll, stickers or progress bars. The format is deliberately clean.
- **Don't add energy with motion.** No bounce, no spring overshoot, no shake, no punch-ins, no glow behind the captions. Energy comes from Piero and the pacing of the bullets. Every move uses the three curves in section 3.5; if a move is not listed there, it does not happen.
- **Captions must be word-perfect.** A misspelled name or keyword on screen is the most common way this goes wrong. If in doubt, ask.
- **Revisions are cheap:** if the assistant says "change the hook to X" or "word at 0:14 should be Y", update `edit_plan.json` / the transcript and re-render only. Don't redo masking.

---

## 7. When you deliver

Send, in this order:
1. The MP4.
2. `transcript.txt`.
3. A short message to the assistant with:
   - What you put on the hook card, the headings and the CTA.
   - Any words you weren't sure of, with timestamps.
   - Any stumbles left in.
   - **One honest note on the content itself, for the assistant to pass to Piero**, only if something is genuinely weak: the hook doesn't create tension in the first 2 seconds, the payoff comes too late, the CTA keyword is buried or mumbled, or the video runs long for what it says. One or two sentences, specific, no fluff. If it's strong, say nothing. The goal is booking calls, not a pretty edit.

Keep the message short. The assistant needs to forward the video and get on with their day.
