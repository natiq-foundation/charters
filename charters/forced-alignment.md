# Project Charter - forced-alignment

**Last Updated**:
**Version**: 1.0.0
**Status**: In Progress

---

## Project Identification

| Field                  | Value            |
| ---------------------- | ---------------- |
| **Project Name**       | Forced Alignment |
| **Project Code**       | Python           |
| **Project Manager**    |                  |
| **Development Team**   |                  |
| **Start Date**         | 2025-07-13       |
| **Estimated End Date** |                  |

---

## Vision and Goals

### Vision

Alignment Text to voice, by word by word timestamp.

### High-Level Goals

- Forced Alignment AI Algorithm
- Cut voice file by word or cut flag
- RESTfull Open API
- Independent server
- FrontEnd

---

## Project Scope

### In-Scope

- Get voice file & text, Response json
- Cut voice file
- Hold files in S3
- Serve response in S3

### Out-of-Scope

- Convert voice to text
- Collect any Backupable data

---

## Architecture & Technologies

### Frontend

- **Framework**: React
- **Template**: [natiq-frontend](/natiq-foundation/natiq-frontend)
- **Coding Standards**: frontend-standards

### Backend

- **Language**: Python
- **Framework**: Django
- **Database**: Redis

### AI

- **Language**: Python
- **Module**: GPT free ver

### Infrastructure

- **CI/CD**: GitHub Actions
- **Hosting**: Server
- **Docker availbe containers**:
  - AI Proccessor
  - Django API
  - Redis
  - S3

---

## Success Metrics

- Alignment Quran text to recitation

---

## Approval Signatures

| Role            | Name              | Signature | Date |
| --------------- | ----------------- | --------- | ---- |
| Curator         | [Al-Abd](/al-abd) |           |      |
| Project Manager |                   |           |      |
