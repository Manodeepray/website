+++
title = 'ClassIQ'
date = 2025-04-23T03:06:53+05:30
draft = false
+++

# Building a Classroom Monitor with Face Recognition and AI-Powered Lecture Notes

> This was my 3rd-year college minor project. I built it to explore how AI could be used for classroom engagement, automating attendance, and helping out with note generation.

-----

## What I Was Trying to Do

The basic idea was to build an AI system on a server that uses computer vision, speech recognition, and an LLM to:

  * Detect faces and recognize student identities.
  * Track attentiveness during a class.
  * Transcribe and summarize the lecture into structured markdown notes.
  * Store and show all this data on a cloud dashboard.

The system is designed to work with a device in the classroom (like a Raspberry Pi or a local camera), but I built a **simple Streamlit app** to demo the functionality on a **single video** right on your laptop.

-----

## How It Works

The core system is designed as a **server-based pipeline**. Once it's deployed:

1.  An **edge device** (like a Pi) records a classroom session (video + audio).
2.  The **URL of the processing server (ngrok)** is entered into that device.
3.  Every time a new video is sent, the server:
      * Detects and recognizes faces
      * Tracks attentiveness
      * Transcribes the audio
      * Uses an LLM to generate structured notes
      * Saves all the output to cloud storage

The **Streamlit UI** (`apps/demo_app.py`) just runs this whole process for a **single demo video**, giving a preview of how it all fits together.

-----

## Core Features

  * Face Detection and Recognition for Attendance
  * Frame-Based Attentiveness Tracking
  * Audio Transcription via Vosk
  * LLM-Powered Summarization (Groq's `llama3-8b-8192`)
  * Streamlit-Based UI for Demos & Data Exploration

-----

## Tech Stack

| Layer | Tools & Libraries |
|:---|:---|
| Vision | YOLOv11, YuNet (OpenCV) |
| Transcription | [Vosk Small EN](https://alphacephei.com/vosk/models) |
| Summarization | Groq LLM (`llama3-8b-8192`) |
| Backend | Flask, tmux, ngrok |
| UI/Dashboard | Streamlit |
| Deployment | Lightning AI |

-----

## Some Results

  * **Face Recognition Accuracy**: 91.67% (Top-1)
  * **Attentiveness Metric**: I used a simple metric for this:
    ```
    Attentiveness = (frames student is visible) / (total frames)
    ```
  * **Lecture Notes Quality**: This was pretty subjective and depends heavily on the LLM and the prompt.

-----

## What I'd Do Next

  * Shift to a custom facial-points-based recognition model.
  * Add real-time inattentiveness alerts.
  * Refine the LLM prompts for more structured results.
  * Switch from CSV to PostgreSQL for a more scalable dashboard.

-----

## About Me

**Manodeep Ray** – I'm really into deep learning, LLMs, CV, and building real-world systems. This project was built as part of my **college 3rd-year minor project** and was a fun way to blend CV and NLP in an educational setting.

Thanks for checking it out\! If you liked this, drop a ⭐ on [GitHub](https://github.com/Manodeepray/minor_project/) or connect with me to chat about AI + education.