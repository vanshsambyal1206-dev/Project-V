# PROJECT-V

A single-page point-cloud studio that runs entirely in the browser. Drop in up to four
photographs and each one is estimated for depth on-device, then scattered into a cloud of
points; a "drift line" blows the sand off one side of the frame and gathers it back into the
next picture.

No server, no upload, no build step — `index.html` is the whole app.

## Run it

Open `index.html` directly, or serve the folder so the depth worker can fetch its model:

```bash
python -m http.server 8080
# then visit http://localhost:8080
```

A local server is recommended. Browsers block `fetch()` of the model files from `file://`.

## What it does

- **Depth in the browser** — FastDepth packed as an 8-bit ONNX model, executed with
  ONNX Runtime Web inside a Web Worker (`depth/worker.js`).
- **Sand controls** — drift, splash, gather, depth and turn, plus a draggable drift line
  that decides which side of the frame fades.
- **Layers** — trackers, links, scan plane, trails and frame marks, each on its own switch.
- **Travel modes** — swarm (every point finds a new place) and melt (points find the
  nearest matching part), and a white/black paper toggle with negative or true tone.
- **Light** — pick a colour and light one spot inside the sand.
- **Output** — record a take, export a 2x PNG of the current view, or download the cloud
  as PLY for Blender and MeshLab.

## Keyboard

| Key | Action |
| --- | --- |
| `Space` | next picture |
| `S` | light |
| `B` | flip the paper |
| `R` | turn the element |
| `D` | download menu |
| `F` | full screen |
| `M` | travel mode |

## Layout

```
index.html            the app — markup, styles and runtime in one file
fonts/                Manrope + Noto Serif TC, self-hosted woff2
depth/                FastDepth model (base64 + wasm), ONNX Runtime, worker
favicon.ico
```

## Credits

Gather is made by DAO. This build stands on:

- **ONNX Runtime Web 1.17.3** — MIT, Microsoft Corporation
- **FastDepth** — MIT, Diana Wofk, Fangchang Ma, Tien-Ju Yang, Sertac Karaman, Vivienne Sze
- **MonocularDepth** (`com.bonjour-lab.monoculardepth`) — MIT, Bonjour lab
- **Depth Anything V2 Small** — Apache-2.0, fallback model

The full licence texts are reproduced in the in-app credits panel.
