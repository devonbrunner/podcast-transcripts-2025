# 🧠 Project Handoff: AWS Podcast Whisper Automation

### Purpose
Automate the download and transcription of AWS Official Podcast episodes using **GitHub Actions** and **Whisper.cpp**, storing the outputs (`.txt` + `.csv`) directly in the repository.

---

## ✅ Current Project Summary

**Objective:**  
Transcribe AWS podcast episodes automatically, append results, and maintain a cumulative dataset.

**Environment:**  
- GitHub repository with Actions enabled  
- Public repo structure:
.github/workflows/transcribe_local.yml
data/
transcripts/
audio/
README.md

**Toolchain:**  
- **Whisper.cpp** (compiled during workflow run)
- **Feedparser + Python** for pulling RSS metadata
- **GitHub Actions runner** (`ubuntu-latest`)
- **ffmpeg** for audio decoding
- **Python subprocess wrapper** for stable transcription execution

---

## 🎧 Podcast Feed Details

**Feed name:** AWS Official Podcast  
**RSS URL:** `https://d3gih7jbfe3jlq.cloudfront.net/aws-podcast-feed.xml`  
**Format:** Standard podcast RSS with MP3 enclosures.

---

## ⚙️ Workflow Overview

**Filename:** `.github/workflows/transcribe_local.yml`

**Trigger:**  
Manual — via **“Run Workflow”** button on the GitHub Actions tab.

**Parameters:**  
- `model` → Whisper model size (`base.en`, `small.en`, `medium.en`)  
- `source_name` → Default metadata tag (`AWS Official Podcast`)  
- `feed_url` → Defaults to AWS RSS feed  
- `max_items` → How many episodes to fetch per run (default: 5)

**Process Flow:**
1. Checkout repo and install dependencies.  
2. Clone and build `whisper.cpp`.  
3. Download Whisper model (`ggml-small.en.bin`, etc.).  
4. Fetch and download the latest podcast episodes via RSS.  
5. Transcribe audio to `.txt` using Whisper.cpp (Python-managed).  
6. Append results to `data/transcripts/transcripts.csv`.  
7. Commit new transcripts back to the repository.  
8. Skip already-transcribed episodes on future runs.  

---

