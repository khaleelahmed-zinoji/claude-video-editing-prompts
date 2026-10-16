# How I edited a reel with Claude Code (the exact prompts)

Here's exactly how I made that reel. I recorded ONE take on my phone, then edited the whole thing with Claude Code just by typing what I wanted. No editing app, no timeline.

Below are the exact prompts I used, in order. Copy them and swap in your own details 👇

## The prompts ✳️

1. "Here's my recording and script. Make a 9:16 reel: edited version on top, my original take underneath."
2. "Zoom in on my face slowly. Make it dramatic: halo, speed lines, a light flare."
3. "Put my logo in my hand in 3D, then throw it at the camera and crack the glass."
4. "Put my name on the wall behind me as a neon sign. Split the scene into layers: wall, me, text. Hide me, then bring me back."
5. "Shrink me to the right and list what we do, ticking each item as I say it."
6. "Swap the office for Dubai at night, like I'm standing on the road. Add a shooting star where I look up."
7. "Float our client work around me in 3D."
8. "Turn the last frame into my thumbnail."
9. "Cut the pauses but leave a little breathing room. Keep the framing steady."

Then I just watched it and gave notes in plain words, like I would to an editor.

## The setup 🛠️

- Claude Code (from Anthropic) does the editing.
- HyperFrames turns each scene into a web page and renders it as an MP4.
- Record in front of a plain wall or green screen, in one take, good light.

**Tip:** describe the result you want, not the steps. "Make it dramatic" works better than listing effects.

---

## Installing HyperFrames, step by step 🧩

HyperFrames is a free, open-source tool by HeyGen ([github.com/heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)). Every scene is an HTML page with animation, and HyperFrames records it frame by frame into a video. You don't install it globally: you run it with `npx`, which always fetches the right version.

*Written for HyperFrames v0.8.164.*

### Step 1: Install Node.js (version 22 or newer)

HyperFrames needs Node.js 22+. Check what you have:

```bash
node -v
```

If it says `v22` or higher, skip ahead. Otherwise install the current LTS:

- **Mac:** `brew install node` (needs [Homebrew](https://brew.sh)), or download from [nodejs.org](https://nodejs.org)
- **Windows:** download the installer from [nodejs.org](https://nodejs.org)
- **Linux:** use your package manager or [nodejs.org](https://nodejs.org/en/download)

### Step 2: Install FFmpeg (needed to render the MP4)

- **Mac:** `brew install ffmpeg`
- **Ubuntu / Debian:** `sudo apt install ffmpeg`
- **Windows:** download from [ffmpeg.org/download.html](https://ffmpeg.org/download.html) and add it to your PATH

Check it worked:

```bash
ffmpeg -version
```

### Step 3 (optional): Install Whisper for automatic word timing

If you start a project from a video, HyperFrames transcribes it word by word so animations land on the exact words you say. On a Mac:

```bash
brew install whisper-cpp
```

### Step 4: Install Claude Code

Follow the official guide: [docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code). You can also use Claude Code inside the Claude desktop app.

### Step 5: Create your project

In the folder where you keep your videos:

```bash
npx hyperframes init my-reel --resolution portrait --video ./my-take.mov
```

- `my-reel` is the project folder it creates.
- `--resolution portrait` makes a 1080×1920 vertical video (use `landscape` for YouTube 16:9).
- `--video` brings in your recording and transcribes it. Leave it out to start from a blank project.

This also installs the HyperFrames skills that teach Claude Code how to build videos. To install or refresh them on their own:

```bash
npx hyperframes skills
```

### Step 6: Check everything is ready

```bash
npx hyperframes doctor
```

This checks Node, FFmpeg, Chrome, disk space and memory. Ticks are good; anything marked "optional" can be ignored. If the Chrome check fails, download the rendering browser with:

```bash
npx hyperframes browser ensure
```

### Step 7: Edit by talking to Claude

```bash
cd my-reel
claude
```

Now paste the prompts above, one at a time. Watch the result, then give notes in plain words.

### Step 8: Preview and render

Watch it in the browser while you work:

```bash
npx hyperframes preview
```

Render the final MP4:

```bash
npx hyperframes render -o renders/my-reel.mp4 -q delivery
```

### If something goes wrong

| Problem | Fix |
|---|---|
| "FFmpeg not found" | Install FFmpeg (step 2), then open a new terminal window |
| Errors about the Node version | Update Node.js to 22 or newer (step 1) |
| Chrome won't download or render fails at launch | `npx hyperframes browser ensure --force` |
| Not sure what's wrong | `npx hyperframes doctor` |
| Want to check your project for mistakes | `npx hyperframes check` |

---

If you want this kind of AI automation for your own business, from content to WhatsApp and customer follow-ups, that's what we build at Ainora: [ainora.ai](https://ainora.ai)
