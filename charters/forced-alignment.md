# Project Charter - forced-alignment

**Last Updated**:
**Version**: 1.0.0
**Status**: In Progress

---

## Project Identification

| Field                  | Value            |
| ---------------------- | ---------------- |
| **Project Name**       | Forced Alignment |
| **Project Code**       |                  |
| **Project Manager**    |                  |
| **Development Team**   |                  |
| **Start Date**         | 2025-07-13       |
| **Estimated End Date** |                  |

---

## Vision and Goals

### Vision

Automatically align a given text with a spoken audio file, producing word-level timestamps.

### High-Level Goals

- Implement an AI-based forced alignment algorithm with word-level accuracy.
- Splite the audio at specific timestamps (by word, sentence, or custom markers).
- Standalone server
- RESTful Open API
- User-friendly web interface to upload audio/text, view results, and download segmented audio.

---

## Project Scope

### In-Scope

- Accept an audio file and its transcript, return a JSON response with alignment timestamps.
- Segment the audio file.
- Store input and output files in S3-compatible storage.

### Out-of-Scope

- Speech-to-text (ASR) transcription.
- Collection of data for backup purposes.

---

## Architecture & Technologies

### Frontend

- **Framework**: React
- **Template**: [natiq-frontend](https://github.com/natiq-foundation/natiq-frontend)
- **Coding Standards**: frontend-standards

### Backend

- **Language**: Python
- **Framework**: Django
- **Database**: Redis

### AI

- **Language**: Python
- **Module**: Free/Opensource model like OpenAI Whisper

### Infrastructure

- **CI/CD**: GitHub Actions
- **Hosting**: Docker Containers
- **Docker available containers**:
  - AI Processor
  - Django API
  - Redis
  - AWS S3

---

## Success Metrics

- Word boundary accuracy >95% on Quranic recitation test set
- Brute force handling

---

## Approval Signatures

| Role            | Name              | Signature | Date |
| --------------- | ----------------- | --------- | ---- |
| Curator         | [Al-Abd](/al-abd) |           |      |
| Project Manager |                   |           |      |
