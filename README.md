# MeetScribe

Convert meeting audio into structured minutes and action items using open-source AI models. Built as a Google Colab notebook for easy GPU access.

## Overview

MeetScribe takes a meeting recording (MP3) and produces professional meeting minutes in Markdown, including:

- Summary with attendees, location, and date
- Key discussion points
- Takeaways
- Action items with owners

The pipeline has two stages:

1. **Transcribe** — Convert audio to text
2. **Analyze & report** — Generate structured minutes from the transcript

## Pipeline

```
Meeting Audio (MP3)
        │
        ▼
┌───────────────────┐
│  Step 1: Transcribe │
│  Whisper (HF)       │
└───────────────────┘
        │
        ▼
┌───────────────────┐
│ Step 2: Analyze   │
│ Llama 3.2 3B      │  4-bit quantized via Hugging Face
└───────────────────┘
        │
        ▼
Structured Markdown Minutes
```

## Models & tools

| Component | Model / library |
|-----------|-----------------|
| Transcription | `openai/whisper-medium.en` via Hugging Face Transformers |
| Minutes generation | `meta-llama/Llama-3.2-3B-Instruct` (4-bit quantization) |
| Runtime | Google Colab (GPU recommended) |

## Requirements

- [Google Colab](https://colab.research.google.com/) with a **T4 GPU** runtime
- [Hugging Face](https://huggingface.co/) account and access token (for Whisper and Llama)
- Meeting audio file (MP3)

## Getting started

1. Open [`MeetScribe.ipynb`](MeetScribe.ipynb) in Google Colab.
2. Set the Colab secret `HF_TOKEN` — your Hugging Face access token.
3. Mount Google Drive and place your audio file (default path: `MyDrive/llms/denver_extract.mp3`).
4. Run all cells from top to bottom.

### Sample audio

You can use the included Denver City Council meeting extract:

- [Sample MP3 (Google Drive)](https://drive.google.com/file/d/1UedmC2PrxtxWs0_qCk3ffl9T2cBa1x1a/view?usp=sharing)

Or use your own recording, or the full [MeetingBank dataset on Hugging Face](https://huggingface.co/datasets/huuuyeah/meetingbank).

## Colab tips

If you see a CUDA / bitsandbytes error mid-run, Colab likely switched your runtime:

1. **Kernel → Disconnect and delete runtime**
2. **Edit → Clear all outputs**, then reconnect with a **T4 GPU**
3. Re-run cells from the top, starting with `pip install`

## Project structure

```
MeetScribe-Converts-meeting-audio-into-structured-minutes-and-action-items/
├── MeetScribe.ipynb    # Main Colab notebook
├── README.md
└── LICENSE
```

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE).

## Acknowledgments

Based on course material from the LLM Engineering curriculum. Student contribution reference: Emad S. (Gradio streaming UI variant).
