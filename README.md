# 8D Audio Mix — Web Studio

**Turn any song into 8D audio — right in your browser.**

🔗 **Live: [https://8d-audiomix.netlify.app](https://8d-audiomix.netlify.app/)**

**Author:** Kotti Satyanarayana

---

## What this is

A complete 8D audio studio that lives in a **single file: `index.html`**.

Drop in a track and it starts orbiting around your head. Choose a preset or dial every
parameter by hand, listen live, then render and download the result as MP3 or WAV —
all without installing anything, signing up, or uploading a single byte.

**No build step. No dependencies. No server. No tracking.** The one file you deploy is
the entire application.

---

## Features

| | |
|---|---|
| **Orbits any track** | Drop in MP3, WAV, M4A, AAC, OGG, FLAC or Opus |
| **Live preview** | Play as you tweak — every slider updates the sound instantly |
| **25 presets** | From *Subtle* and *Sleep* to *Vertigo*, *Space* and *Headphone test* |
| **36 controls** | Feel, motion, space, tone and output — all live |
| **Slow-mo** | Drop the speed to 0.5× for slowed-and-pitched-down audio, or push it to 1.5× |
| **Reverb on/off** | Kill the tail entirely, or dial it up to six seconds |
| **6 orbit shapes** | Circle, ellipse, figure-8, pendulum, spiral, Lissajous |
| **Orbit visualiser** | Top-down view showing exactly where the sound is right now |
| **A/B bypass** | One click to hear the dry track against the 8D version |
| **MP3 export** | 128 / 192 / 256 / 320 kbps, or "match source" to keep your file size |
| **WAV export** | 16-bit, 24-bit or 32-bit float |
| **Size preview** | Shows the exact output size before you render |
| **100% private** | Your audio never leaves your device — everything runs in the tab |
| **Works offline** | No CDN, no fonts, no external requests. Load it once, use it anywhere |
| **Responsive** | Full studio on desktop, tidy centred dial and docked controls on mobile |
| **Remembers you** | Your settings and preset are restored on your next visit |

---

## How to use it

**1. Add a track**
Open the site and drop an audio file onto the drop zone — or click it to browse your
device. It decodes and starts playing straight away. Your file stays on your machine.

**2. Pick a preset**
Start with **Classic** for the familiar 8D feel. **Subtle** is best for real listening;
**Save preset** keeps whatever you dial — set your own slowed amount, hit Save, and you get
it back with one click (it stays in your browser as a dashed *My Preset* chip).

**Reset** puts every control back to the defaults — speed included — and the change is live: the track speeds back up as you click it.

**Slowed + Reverb** is the one that makes a song sound dreamy — it drops the pitch 8%
(0.92×) and puts a big warm tail behind it. **Slowed** does the pitch drop with no reverb at
all, and **Reverb** gives you the hall tail at full speed, so you can pick which half of
the effect you want. **Space** and **Headphone test** push the effect
about as far as it goes. Every preset
shows a one-line description of what it does, and the panel underneath shows the live
numbers behind it.

**3. Dial it in**
Everything under **Controls** applies immediately while the track plays:

- **Feel** — **Speed (slow-mo)**: below 1.00 slows the song and drops the pitch together; and the **Reverb** switch
- **Motion** — how fast it orbits, how wide and how deep it travels, which path it takes
- **Space** — head shadow, interaural delay, reverb size and depth, crossfeed, mono bass
- **Tone** — bass and air
- **Output** — trim, normalise, soft limiter

Use **A/B · dry** to check your work against the untouched audio, and **Shuffle** if you
want a fresh setting built for you.

**4. Render and download**
Choose MP3 or WAV, set the bitrate or bit depth, name the file, and hit
**Render & download**. Rendering runs several times faster than real time and the file
downloads directly to your device.

🎧 **Use headphones.** This is the one thing that matters. On speakers both ears hear
both drivers, the level and delay differences cancel out, and the effect collapses back
to the middle of the room.

---

## Presets

| | | |
|---|---|---|
| Classic | Subtle | Wide |
| Intimate | Figure-8 | Pendulum |
| Spiral | Vertigo | Chaos |
| Slowed | Reverb | Slowed + Reverb |
| Nightcore | — | — |
| Hall | Cathedral | Cave |
| Tunnel | Space | Underwater |
| Rave | Sleep | Café |
| Lo-fi | Boom bap | Headphone test |

Each preset sets **every** parameter, not just one or two. Measured over a full render,
Subtle and Sleep stay deliberately gentle while Wide and Space push right to the edge.

---

## Export formats

**MP3** is the default, and the right choice most of the time.

| format | sizes | notes |
|---|---|---|
| MP3 | 128 · 192 · 256 · 320 kbps · *match source* | Small files, identical duration |
| WAV | 16 · 24 · 32-bit float | Uncompressed and lossless |

### Why a WAV is so much bigger than your MP3

Nothing is going wrong — WAV simply isn't compressed:

```
8 MB MP3   ≈ 3m20s at ~320 kbps   (compressed: discards what you can't hear)
53 MB WAV  = the same 3m20s       (raw PCM: 44,100 samples/sec × 2ch × 3 bytes)
```

The duration and the audio are identical; the WAV just stores every sample
uncompressed. The size panel shows all three numbers **before** you render, and
**"match source"** automatically picks the MP3 bitrate that reproduces your input
file's size.

---

## Technical notes

- **One file.** `index.html` is ~276 KB and entirely self-contained: styles, markup,
  engine and the MP3 encoder are all inlined. Copy it anywhere and it works.
- **The engine** is a hand-written DSP chain — bass/air shelving, head-shadow filters,
  fractional-delay interaural time difference, a pinna notch, a Freeverb-style reverb,
  crossfeed, mono bass and a soft limiter — running on the Web Audio API.
- **Mastering-safe output.** Everything normalises to **−1.0 dBFS true peak** — the real
  inter-sample peak, not the sample peak — which is the standard ceiling for lossy
  delivery. That headroom is why the MP3s never crackle.
- **AudioWorklet.** Live playback runs the engine in an `AudioWorklet` for click-free,
  glitch-free control. On `file://` or non-secure hosts it quietly falls back to an older
  path; over HTTPS (like this deployment) you always get the fast one.
- **MP3 encoding** is LAME compiled to JavaScript and bundled inside the file — which is
  why MP3 export works with no server and no ffmpeg.
- **Privacy.** There is no backend, no analytics and no upload. Decoding, processing and
  encoding all happen locally in your browser tab.

### Browser support

Works in current Chrome, Edge, Firefox and Safari (14.1+). MP3 encoding is the most
demanding part; WAV export works everywhere.

---

## Deploying it yourself

Because the whole studio is one static file, any static host can serve it:

- **Netlify** — drag `index.html` onto [app.netlify.com/drop](https://app.netlify.com/drop)
- **GitHub Pages, Cloudflare Pages, Vercel** — upload the file to the repo root
- **Your own server** — copy it into any web directory

Make sure `index.html` sits at the **root** of what you publish, so the site's main URL
serves it directly. HTTPS is recommended: it enables the faster AudioWorklet playback
path and guarantees downloads behave in every browser.

---

## License

Free to use, modify and share. The bundled MP3 encoder is LAME, compiled to JavaScript,
distributed under the LGPL (see `vendor/lame.min.js` in the full project).

---

**Built by Kotti Satyanarayana.**
Live at **[8d-audiomix.netlify.app](https://8d-audiomix.netlify.app/)** — headphones on. 🎧
