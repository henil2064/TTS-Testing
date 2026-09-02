# TTS-Testing

A collection of notebooks and results for evaluating and comparing Indic-language Text-to-Speech (TTS) engines on accuracy, robustness, and speed.

## Overview

This repo is a testing sandbox for benchmarking multiple TTS systems by:

- Synthesizing speech for a set of reference texts (across languages and emotions)
- Transcribing the generated audio back to text using two different ASR models
- Scoring intelligibility with **Word Error Rate (WER)** and **Character Error Rate (CER)**
- Measuring synthesis speed with **Real-Time Factor (RTF)**

## Contents

| File | Description |
|---|---|
| `dhvaani.ipynb` | Testing/evaluation notebook for the **Dhvaani** TTS engine |
| `svara-tts-v1.ipynb` | Testing/evaluation notebook for the **Svara TTS** engine |
| `praxy-voice-r6 (1).ipynb` | Testing/evaluation notebook for the **Praxy Voice** TTS engine |
| `indic-mioq8q4.ipynb` | Testing/evaluation notebook for an Indic TTS engine/model |
| `emotion-tagging (1).ipynb` | Notebook for tagging/labeling emotion categories on the evaluation dataset |
| `tts-metrics.ipynb` | Computes WER, CER, and RTF metrics from synthesized audio and ASR transcripts |
| `Final_tts_eval.csv` | Consolidated evaluation results across all tested engines |

## Evaluation Data

`Final_tts_eval.csv` holds the combined results, with one row per synthesized audio sample:

| Column | Meaning |
|---|---|
| `engine` | TTS engine used to generate the audio |
| `file` | Audio file identifier |
| `language` | Language of the sample |
| `emotion` | Emotion label for the sample |
| `wer_sravaani` / `cer_sravaani` | WER / CER when transcribed with the Sravaani ASR model |
| `wer_whisper` / `cer_whisper` | WER / CER when transcribed with OpenAI Whisper |
| `rtf` | Real-Time Factor (synthesis time ÷ audio duration — lower is faster) |
| `audio_seconds` | Duration of the generated audio |
| `reference_text` | Ground-truth text that was synthesized |
| `asr_sravaani` / `asr_whisper` | Transcript produced by each ASR model |

## Methodology

1. Each TTS engine synthesizes audio from the same set of reference texts (spanning multiple languages/emotions).
2. The generated audio is transcribed independently by two ASR systems — **Sravaani** and **Whisper** — to cross-check intelligibility.
3. WER and CER are computed by comparing each ASR transcript against the reference text.
4. RTF is logged to capture how synthesis speed compares across engines.
5. Results from all engines are aggregated into `Final_tts_eval.csv` for side-by-side comparison.

## Usage

The notebooks are designed to run on a GPU-backed environment (e.g., Kaggle/Colab):

1. Open the notebook for the engine you want to test (e.g., `svara-tts-v1.ipynb`).
2. Run the synthesis cells to generate audio from the reference texts.
3. Run `tts-metrics.ipynb` to score the output against the ASR models and compute WER/CER/RTF.
4. Results append to / regenerate `Final_tts_eval.csv`.

## Notes

- This is a testing/benchmarking repo, not a production TTS library — no installable package is provided.
- Add engine-specific setup instructions (model weights, API keys, dependencies) here as needed.

---

