# Moja ulica

Moja ulica is a Slovenian web app that helps residents turn an idea for improving a street or public space into a visual proposal. Upload a photo, describe the change you would like to see, and compare the original with an AI-generated proposal.

## Live demo

Try the app at [moja-ulica.web.bilt.me](https://b468f1ec-f05c-45dd-b220-fe3b9227978f.web.bilt.me).

## What it does

- Upload, drag-and-drop, paste, or select a street photo
- Choose a sample image when you do not have a photo ready
- Describe a proposed improvement in Slovenian
- Create an AI-generated visual proposal
- Compare the original and result with an interactive before/after slider
- Download the generated proposal as a PNG

## How it works

```text
Street photo + improvement request
              ↓
Browser prepares the image and sends a ComfyUI workflow
              ↓
Ollama turns the request into a scene-aware image prompt
              ↓
ComfyUI creates the visual proposal
              ↓
The app shows and downloads the before/after result
```

The prompt workflow is designed to preserve the existing street scene—such as the viewpoint, weather, buildings, and layout—while visualising only the requested changes.

## Run locally

The frontend is a static HTML page, but generation requires a ComfyUI server.

1. Set the ComfyUI base URL in the HTML file:

   ```js
   const SERVER_URL = "https://your-comfyui-host.example";
   ```

2. Start ComfyUI with CORS enabled:

   ```bash
   python main.py --enable-cors-header "*"
   ```

3. Serve the project locally:

   ```bash
   python -m http.server 8000
   ```

4. Open the page in your browser.

## Requirements

- A ComfyUI installation exposing `/prompt`, `/history`, `/view`, and `/system_stats`
- Ollama with the `gemma3:4b` model
- The custom ComfyUI nodes and models referenced by the embedded workflow

## Privacy and deployment

Photos are sent directly from the browser to the configured ComfyUI server. Before public deployment, secure the generation endpoint and provide a privacy notice explaining how submitted images are handled.

