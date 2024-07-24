+++
title = 'Oral_guard'
date = 2024-07-24T12:32:52+05:30
draft = false
+++

## Its my Summer Internship Project at IIT Bhilai

During my internship, I worked on an innovative deep learning project focusing on cancer prediction. I developed a web app with Gradio that assists in diagnosing and evaluating oral diseases. Here’s a detailed breakdown of the project:

### Part 1: Image Classification

**Model:** YOLOv8n  
**Task:** Predicts the type of oral disease (cancer, dental caries, scurvy, periodontal, healthy) using image classification on custom data.

**Advanced Detection:** If cancer is detected, the model then uses object detection to pinpoint the growth location and determines the grade and stage:

**Grades:**

- **Grade 1:** Similar to normal cells
- **Grade 2:** Slightly abnormal
- **Grade 3:** Very abnormal

**Stages:**

- **Stage 1:** Less than 2 cm
- **Stage 2:** 2 cm to 4 cm
- **Stage 3:** Greater than 4 cm to widespread growth

**Data Collection:** All images were gathered and processed by me using Google extensions.

**Workflow:** The images are fed into the trained YOLOv8n model, which first classifies the disease type. If the disease is classified as cancer, the model performs object detection to identify the specific location of the cancerous growth. The detected area is then analyzed to determine the grade and stage of the cancer based on predefined criteria.

### Part 2: Symptom-Based Prediction

**Input:** Symptoms entered by the patient

**Model:** Retrieval-Augmented Generation (RAG) model on custom PDFs  
**Functionality:** Predicts the grade and stage of oral cancer based on patient symptoms, followed by treatment recommendations.

**Grade and Stage Prediction:** The RAG model takes the patient’s symptoms and matches them with information from custom PDFs to determine the grade and stage of cancer.

**Treatment Recommendations:** Two additional RAG models provide treatment options based on the determined grade and stage, sourcing information from specific PDFs that detail treatments for each grade and stage.

**LLM used:** Mistral 7B

### Challenges and Limitations

**LLM Constraints:** Due to size limitations (maximum 10GB on Hugging Face), a lighter LLM was utilized, necessitating the creation of three distinct RAG models (two for treatment recommendations and one for grade and stage evaluation).  
**Multiple API Calls:** Multiple calls to the LLM were required for coherent responses, which could be optimized with a more robust model such as GPT-3 or Gemini. A single, more powerful LLM would enhance processing efficiency and accuracy.  
**Performance:** The current RAG model setup results in longer processing times, impacting the speed of output generation.

[Linked in post](https://www.linkedin.com/posts/manodeep-ray-346b3b294_deeplearning-cancerprediction-ai-activity-7219962641518067712--nht?utm_source=share&utm_medium=member_desktop)
[Github repo ](https://github.com/Manodeepray/oral_health_ai)
