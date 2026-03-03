# Assets

## Game demo GIF (for README)

GitHub does not show `<video>` tags in READMEs, so the demo is shown as an **animated GIF** that displays like the other screenshots.

To generate or update `demo.gif` from `iSoftBet.mp4`:

1. Install [FFmpeg](https://ffmpeg.org/download.html) (add it to your PATH).

2. From this `assets` folder, run:

**Quick (first 12 seconds, smaller file):**
```bash
ffmpeg -i iSoftBet.mp4 -t 12 -vf "fps=10,scale=800:-1:flags=lanczos" -y demo.gif
```

**Better quality, smaller size (two-pass with palette):**
```bash
ffmpeg -i iSoftBet.mp4 -t 12 -vf "fps=10,scale=800:-1:flags=lanczos,palettegen" -y palette.png
ffmpeg -i iSoftBet.mp4 -i palette.png -t 12 -lavfi "fps=10,scale=800:-1:flags=lanczos[x];[x][1:v]paletteuse" -y demo.gif
del palette.png
```

Keep `demo.gif` under **~10 MB** so it loads quickly on GitHub (use `-t 8` or `scale=640:-1` if needed).

3. Commit and push `demo.gif`. The README will then show the animated demo inline.
