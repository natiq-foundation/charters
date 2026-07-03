# Project Charter - Forced Alignment

**Last Updated**:
**Version**: 1.0.0
**Status**: In Progress

---

## 1. Project Identification

| Field                  | Value              |
| ---------------------- | ------------------ |
| **Project Name**       | Forced Alignment   |
| **Project Repo**       | [forced-alignment] |
| **Project Manager**    |                    |
| **Development Team**   |                    |
| **Start Date**         | 2025-07-13         |
| **Estimated End Date** |                    |

---

## 2. Vision and Goals

### Vision

Automatically align a given text with a spoken audio file, producing word-level timestamps.

### High-Level Goals

- Enable users to obtain word‑level timestamps for any given audio and text.
- Provide on‑demand audio segmentation (by word, sentence, or custom marker).
- Offer a simple web interface that requires no technical knowledge.

---

## 3. Project Scope

### In-Scope

- Build an endpoint that accepts audio + transcript, returns alignment JSON.
- Implement asynchronous background processing with status polling.
- Segment the audio file server‑side and serve the clips via S3‑compatible storage.
- Develop a React frontend for upload, preview, and download.

### Out-of-Scope

- Exposing a standalone speech-to-text (ASR) endpoint.
- Collection of data (No data backup).

---

## 4. Architecture & Technologies

### Frontend

- **Coding Standards**: frontend-standards

### Backend

- **Language**: Python
- **Framework**: Django (RESTful API)
- **Coding Standards**: backend-standards
- **Database**: None
- **Broker**: Redis (Celery)
- **Workflow**:
  1. Accept audio + text
  2. Return 202 with task_uuid
  3. Process in background (async)
  4. Poll GET /task/{uuid} for status/result
  5. Optionally support webhooks.

### AI

- **Language**: Python
- **Module**: Free/Opensource model like Whisper-timestamped

### Infrastructure

- **CI/CD**: GitHub Actions
- **Hosting**: Single standalone server (Linux) running Docker
- **Container Orchestration**: Docker Compose (for managing multi-container setup on one host)
- **Core Containers:**:
  - AI Processor
  - Django API
  - Celery
  - Redis
  - minio (Optional - Or use as external service)

---

## 5. Pending Decisions

- Secret access token to api
- Brute force handling
- login

---

## 6. Timeline

none

---

## 7. Risks & Challenges

none

---

## 8. Success Metrics

- Word boundary accuracy >95% on Quranic recitation test set

---

## 9. Budget & Resources

- **Human Resources**: 1

---

## 10. Approval Signatures

| Role            | Github Account    | Signature |
| --------------- | ----------------- | --------- |
| Curator         | [Al-Abd](/al-abd) |           |
| Deputy Curator  | [Al-Abd](/al-abd) |           |
| Project Manager |                   |           |
