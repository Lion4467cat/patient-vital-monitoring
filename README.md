# Intelligent Patient Vital Monitoring and Alert System

## Overview

This project implements an AI‑assisted **patient vital monitoring and alert system** using **LangFlow** and the **IBM Granite 3‑8B Instruct** model on **IBM watsonx.ai**.  
The system analyzes heart rate, blood pressure, oxygen saturation (SpO₂), and temperature, detects anomalies using medical guidelines, computes a risk score (GREEN → RED), and generates non‑diagnostic care guidance.

---

## Problem Statement

Continuous monitoring of vitals for many patients is difficult for hospital staff.  
Early signs of deterioration (sepsis, respiratory failure, cardiac events) can be missed when vitals are only checked periodically.

**Goal:**  
Build an intelligent assistant that:

- Continuously analyzes patient vitals using guideline thresholds.  
- Detects anomalies and trends compared to baseline.  
- Computes a weighted risk score and risk category.  
- Provides assistive, non‑diagnostic alerts and preventive care suggestions.

---

## Architecture (High Level)

Pipeline built in **LangFlow (DataStax Astra)**:

1. **Chat Input** – user enters patient details and current vitals.  
2. **File (Read File)** – loads `file.txt` containing vital‑sign normal ranges and simple protocols (RAG context).  
3. **Prompt Template** – merges:
   - Medical guidelines (`{context}`)
   - Patient vitals (`{patient_data}`)
4. **IBM Granite API Component** – calls `ibm/granite-3-8b-instruct` on IBM watsonx.ai for:
   - Vital analysis (NORMAL / WARNING / CRITICAL)
   - Explanation of anomalies
   - Assistive care guidance
5. **Risk Stratification Calculator (Custom Component)** – Python component that:
   - Parses Granite output to extract severity for each vital.  
   - Maps severity to points: NORMAL=0, WARNING=1, CRITICAL=2.  
   - Computes weighted risk score:  
     - HR × 0.25, BP × 0.30, SpO₂ × 0.30, Temp × 0.15.  
   - Converts score to **GREEN / YELLOW / ORANGE / RED** category.  
   - Appends a short baseline/trend summary to the report.
6. **Chat Output** – displays the final combined report.

---

## Technologies Used

- **LangFlow (DataStax Astra)** – LLM workflow orchestration.  
- **IBM Granite 3‑8B Instruct** – watsonx.ai LLM used for vital interpretation and text generation.  
- **IBM Cloud / watsonx.ai** – Granite hosting and API.  
- **RAG over `file.txt`** – medical vital‑sign guidelines as context.  
- **Python (custom components)** – risk scoring and trend summary logic.

---

## Project Files in This Repository

- `app.py`  
  - Simple Python entry script that demonstrates how vitals would be passed into the LangFlow + Granite pipeline.  
  - When run locally, prints a demo explanation and points to the LangFlow deployment.

- `Problem statement Bengaluru hackathon.docx`  
  - Original hackathon problem statement for “Intelligent Patient Vital Monitoring and Alert System”.

- `Hackathon Project Presentation Final Copy.pptx`  
  - Slide deck explaining need, architecture, components used, screenshots, results, and future scope.

> **Note:**  
> The actual running flow (Read File → Prompt Template → IBM Granite → Risk Stratification → Chat Output) is built and executed in **LangFlow on DataStax Astra**, not directly inside this repository.

---

## How to Run `app.py` (Demo)

```bash
python app.py
