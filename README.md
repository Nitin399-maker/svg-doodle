# ✍️ SVG Animator — AI Hand‑Drawn SVG Animation Generator

This is a **single‑page web app** that:
- Generates **clean SVG** from a natural‑language prompt using an LLM
- Converts the SVG into a **hand‑drawn / sketch style**
- 🎬 Animates strokes using **anime.js** so it looks like the drawing is being created in real time

---

## ✨ Features

- 🗣️ **Prompt → SVG** via LLM (`/chat/completions` style endpoint)
- 🎚️ **Configurable** roughness, stroke width, duration, animation type, and stroke color
- 🧪 **Demo gallery** from `config.json`
- 🌙 **Dark mode** toggle
- ✅ Validates generated SVG before allowing animation (rejects invalid XML/SVG)

---

## 🗂️ Project Structure

Typical folder layout:

```
svg-animator/
├─ index.html
├─ script.js
├─ config.json
└─ README.md
```

- `index.html`: UI + controls + output canvas fileciteturn0file0L1-L220  
- `script.js`: LLM config, demo loading, SVG generation, roughening, animation logic fileciteturn0file1L1-L260  
- `config.json`: Demo cards (title/description/prompt/svg) fileciteturn0file2L1-L40  

---

## ✅ Requirements

You only need:
- A modern browser (Chrome/Edge/Firefox)
- A local static server (because `script.js` is loaded as an ES Module)

No build step is required because libraries are loaded from CDNs.
---


## 🔐 Configure the LLM Provider

1. Open the app.
2. Click **Advanced Settings → Config LLM**.
3. Enter:
   - **Base URL**: typically `https://openrouter.ai/api/v1` (or your router)
   - **API Key**
   - **Model** (example: `gemini-3-pro-preview`)


### How requests are made

The app calls:

```
POST {baseUrl}/chat/completions
Authorization: Bearer {apiKey}
Content-Type: application/json
```

With payload similar to:

```json
{
  "model": "google/<modelName>",
  "messages": [
    {"role": "system", "content": "<system prompt>"},
    {"role": "user", "content": "<your drawing prompt>"}
  ]
}
```

Implementation is in `genSVG()` in `script.js`. fileciteturn0file1L80-L145

---

## 🧭 Using the App

1. Pick a demo card (optional) — it fills the prompt and SVG editor.  
2. Or type your own prompt in **SVG Drawing Prompt**.
3. Click **Generate SVG**.
4. Review/edit the SVG in **Generated SVG (editable)**.
5. Click **Animate** to render a hand‑drawn animation.
6. Use **Reset** to restart the animation.

### Keyboard shortcut

- ⌨️ **Ctrl+Enter** (or **Cmd+Enter**) in the prompt box triggers **Generate SVG**. fileciteturn0file1L262-L280

---

## 🛠️ Advanced Settings (What they do)

- **Roughness**: how “wobbly” the hand‑drawn stroke is (higher = more sketchy) 
- **Stroke Width**: width of the rendered strokes
- **Duration (ms)**: time taken for the animation
- **Animation Type**:
  - **Delayed**: overlapping but delayed starts
  - **Sync**: everything animates together
  - **One by One**: groups animate sequentially fileciteturn0file1L205-L258  
- **Stroke Color**: output stroke color

---

## 📜 License

Internal / demo use (update as needed).
