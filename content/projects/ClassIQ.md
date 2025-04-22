+++
title = 'ClassIQ'
date = 2025-04-23T03:06:53+05:30
draft = false
+++


# Building a Classroom Monitoring System with Face Recognition and AI-Powered Lecture Notes 🧠📸

> 📚 *This was my 3rd-year college minor project,* built to explore how AI can enhance classroom engagement, automate attendance, and help with structured note generation.

---

## 💡 The Vision

The **Classroom Monitoring System** is a server-based AI pipeline using **computer vision**, **speech recognition**, and **LLMs** to:
- Detect faces and recognize student identities
- Track attentiveness throughout a session
- Transcribe and summarize lectures into structured markdown notes
- Store and visualize data on a cloud dashboard

While the system is designed to work with **edge devices** (like a classroom Raspberry Pi or local camera unit), I built a **simple Streamlit app** to demo the functionality on a **single video** on your laptop.

---

## 🧩 How It Works

The core system is designed as a **server-based pipeline**. Once deployed:

1. An **edge device** records a classroom session (video + audio).
2. The **URL of the processing server (ngrok)** is entered into the edge device.
3. Every time a new video is sent, the server:
   - Detects and recognizes faces
   - Tracks attentiveness
   - Transcribes the audio
   - Uses an LLM to generate structured notes
   - Saves all output to cloud storage

The **Streamlit UI** (`apps/demo_app.py`) showcases this pipeline for a **single demo video**, giving a preview of the end-to-end process.

---

## ✅ Core Features

✅ **Face Detection and Recognition for Attendance**  
✅ **Frame-Based Attentiveness Tracking**  
✅ **Audio Transcription via Vosk**  
✅ **LLM-Powered Summarization (Groq's `llama3-8b-8192`)**  
✅ **Streamlit-Based UI for Demos & Data Exploration**  

---

## 🧠 Tech Stack

| Layer             | Tools & Libraries                            |
|------------------|----------------------------------------------|
| Vision            | YOLOv11, YuNet (OpenCV)                      |
| Transcription     | [Vosk Small EN](https://alphacephei.com/vosk/models) |
| Summarization     | Groq LLM (`llama3-8b-8192`)                  |
| Backend           | Flask, tmux, ngrok                           |
| UI/Dashboard      | Streamlit                                    |
| Deployment        | Lightning AI                                 |

---

## ⚙️ Getting Started


Clone the repo
```bash
git clone https://github.com/manodeepray/minor_project
cd minor_project
```

Create a virtual environment
```bash
python3 -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
```

Install dependencies
```bash
pip install -r requirements.txt
```
Install system packages (Linux)
```bash
sudo apt install ffmpeg -y
```
(Optional) Install tmux for background processes
```bash
sudo apt install tmux
```
# Add your Groq API key to a .env file
```bash
echo 'GROQ_API_KEY="your_key_here"' > .env

```
---

## Usage Instructions

### Training The Face Recognition Model With Your Own Data

1. Add your dataset: `dataset/{student_name}/{face_images}`
2. Update the dataset path in `src/training/train_face_rec.py`
3. Generate YOLO-ready data:
   ```bash
   python src/training/get_training_data.py
   ```
4. Train the model:
   ```bash
   bash scripts/train.sh
   ```

### 🖥️ Running the Server Pipeline

```bash
# Optionally use tmux to manage long processes
bash scripts/run_servers.sh
```
```bash
# Or run components manually
python processor.py
python server.py
ngrok http 5000
```

✅ Once deployed, enter the **ngrok link** in your edge device. Each uploaded classroom session video will be processed and results generated automatically.

### Try the Demo UI

```bash
# Demo for single video
streamlit run apps/demo_app.py

# View saved notes and data
streamlit run apps/files_ui.py
```

---

## Customizing Summarization

You can switch the LLM or update the prompt for note generation in:
```python
# src/pipelines/core/llm_integration.py
GROQ_LLM_MODEL_ID = "llama3-8b-8192"
```

And edit the prompt in `generate_notes()` to match your desired note structure.

---

## Results & Observations

- **Face Recognition Accuracy**: 91.67% (Top-1)
- **Attentiveness Metric**:
  ```
  Attentiveness = (frames student is visible) / (total frames)
  ```
- **Lecture Notes Quality**: Depends on LLM + prompt, human-evaluated

---

## 🔮 Future Plans

- Shift to custom facial-points-based recognition model
- Add real-time inattentiveness alerts
- Refine LLM prompts for more structured results
- Switch from CSV to PostgreSQL for scalable dashboard
---

## About Me

**Manodeep Ray** – Passionate about deep learning, LLM , CV, and building real-world systems. This project was built as part of my **college 3rd-year minor project**, blending CV + NLP in an educational setting.




Thanks for checking it out! If you liked this, drop a ⭐ on [GitHub](https://github.com/Manodeepray/minor_project/) or connect with me to chat about AI + education 
