# Whisper Small DV: Fine-Tuning for Dhivehi Speech Recognition

This project fine-tunes OpenAI's Whisper Small model for **Dhivehi (Maldivian language)** speech recognition using the **Common Voice 13 dataset**. The trained model can transcribe Dhivehi speech with high accuracy and is deployed using **Gradio** for an interactive demo. While Whisper does not officially support Dhivehi, this fine-tuning approach leverages Sinhalese as a proxy language to enhance transcription performance.

---

## Features

- **Fine-tunes Whisper Small** on the Dhivehi dataset from Common Voice 13.
- **Uses Sinhalese as a proxy language**, as Dhivehi is not officially supported by Whisper.
- **Applies data preprocessing**: normalizes audio, adjusts sampling rate, and tokenizes text labels for consistency.
- **Evaluates performance** using **Word Error Rate (WER)**.
- **Deploys an interactive demo** using **Gradio**.

---

## Dataset & Model

The fine-tuning process utilizes the **Mozilla Common Voice 13** dataset, which provides transcribed Dhivehi audio samples for training and evaluation. Since Dhivehi data is limited, **Sinhalese was incorporated as a proxy language** to enhance model performance.

### **Dataset Details**

- **Source**: [Mozilla Common Voice 13](https://commonvoice.mozilla.org)
- **Data Splits**: Training, validation, and test sets
- **Preprocessing Techniques**:
  - Converting audio to a 16kHz sampling rate
  - Tokenizing and normalizing text labels
  - Filtering out noisy or misaligned samples for better training stability

### **Model Training**

Fine-tuning was performed using the **Whisper Small** architecture with carefully optimized training parameters:

- **Base Model**: `whisper-small` by OpenAI
- **Training Configuration**:
  - **Max Input Length**: 30 seconds
  - **Batch Size**: 8 (training), 16 (evaluation)
  - **Learning Rate**: 1e-5 with `constant_with_warmup` scheduler
  - **Warmup Steps**: 50
  - **Evaluation Metric**: Word Error Rate (WER)
- **Training Framework**: `Seq2SeqTrainer`

**Fine-tuned Model on Hugging Face**: [AhmedNabil1/whisper-small-dv](https://huggingface.co/AhmedNabil1/whisper-small-dv)

---

## Results

The fine-tuned model demonstrated **strong transcription performance**, significantly improving over the baseline model:

| Training Loss | Epoch  | Step | Validation Loss | Wer Ortho | Wer     |
| ------------- | ------ | ---- | --------------- | --------- | ------- |
| 0.1657        | 0.8157 | 500  | 0.1912          | 65.7218   | 14.1670 |

### **Key Findings:**

- The **baseline Whisper model** struggled with Dhivehi, achieving an **orthographic WER of 168%** and a **normalized WER of 126%**, making it impractical for accurate transcription.
- Our fine-tuned model **significantly reduced WER**, improving transcription accuracy and usability for Dhivehi speech.
- The use of **Sinhalese as a proxy language** played a crucial role in refining the model, enabling it to generalize better to Dhivehi.

---

## Interactive Demo

A **Gradio** demo allows users to transcribe Dhivehi (Maldivian language) speech from a microphone or uploaded audio file.

### **Run the demo**

```python
import gradio as gr
demo.launch()
```

### **Interface**

- **Transcribe Microphone**: Speak and get real-time transcription.
- **Transcribe Audio File**: Upload an audio file for transcription.

---

### 🚀 Try the model and contribute!
