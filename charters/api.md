# Project Charter - API

**Last Updated**: [Date]
**Version**: 1.0.0
**Status**: In Progress

---

## 1. Project Identification

| Field                  | Value                           |
| ---------------------- | ------------------------------- |
| **Project Name**       | API                             |
| **Project Repo**       | quran-api                       |
| **Project Manager**    | [nyzd](https://github.com/nyzd) |
| **Development Team**   | Backend                         |
| **Start Date**         | 2025-02-24                      |
| **Estimated End Date** |                                 |

---

## 2. Vision and Goals

### Vision

TBD

### High-Level Goals

TBD

---

## 3. Project Scope

### In-Scope

- Islamic data including:
  - quran
- Account management
- Token-based authentication
- Role-based access control (e.g., free tier vs. authenticated)
- Stateless architecture to support horizontal scaling.
- Monitoring and health-check endpoints.

### Out-of-Scope

TBD

---

## 4. Architecture & Technologies

### Backend

- **Language**: Python
- **Framework**: Django (RESTful API)
- **Coding Standards**: backend-standards
- **Database**: PostgreSQL
- **Broker**:

#### API Routers

- **Account:**
  - Auth/Login
  - Auth/LogOut
  - Auth/LogOutAll
  - Auth/Register
  - Profile/{id}
  - Profile/me
  - Users
  - Users/{id}/names
  - Groups
- **Quran:**
  - Mushafs
  - Mushafs/id/transmissions
  - Mushafs/import
  - Surahs
  - Surahs/{id}/names
  - Ayahs
  - Ayahs/random
  - Words
  - Translations
  - Translations/{id}/ayahs
  - Translations/import
  - Recitations
  - Recitations/{id}/track
  - Takhtits
  - Takhtits/{id}/ayahs_breakers
  - Takhtits/{id}/word_brakers
  - Takhtits/{id}/import
- **Other:**
  - Provenances
  - Notifications
  - Notifications/me
  - Notifications/opened
  - Notifications/viewed
  - Health

#### DB Tables

- **Account:**
  - **account_customuser** (Stores user accounts and profile information)
  - **account_customuser_groups** (Intermediate table for user-group relationships)
  - **account_customuser_user_permissions** (Intermediate table for user-permission relationships)
  - **account_username** (Stores different names associated with users)
  - **auth_permission** (Stores user and group permissions)
  - **auth_group** (Stores user groups)
  - **auth_group_permissions** (Intermediate table for group-permission relationships)

- **Django system tables**
  - **django_admin_log** (Stores actions performed through Django Admin)
  - **django_content_type** (Stores metadata about installed Django models)
  - **django_migrations** (Tracks applied database migrations)
  - **django_sessions** (Stores user session data and expiration information)
  - **knox_authtoken** (Pending model and relationship inspection)

- **Core:**
  - **core_request** (Stores information about requests and responses)
  - **core_publicdocument** (Stores publicly accessible documents)
  - **core_file** (Stores uploaded file metadata and storage information. Related to account_customuser)
  - **core_notification** (Stores notifications and their status for users)

- **Quran:**
  - **quran_rasmolmushaf** (Stores Rasm al-Mushaf information)
  - **quran_romsurahayahs** (Associates a Rasm al-Mushaf with a Surah and Ayah)
  - **quran_provenance** (Stores provenance records with optional one-to-one parent-child relationships)
  - **quran_transmission** (Stores Quran transmission information, Related to quran_provenance)
  - **quran_surah** (Stores Quran surah information, Related to account_customuser)
  - **quran_ayah** (Stores Quran ayah information)
  - **quran_word** (Stores Quran word information)
  - **quran_wordtext** (Stores text associated with Quran words, Related to quran_transmission)
  - **quran_translation** (Stores Quran translation information, Related to quran_transmission)
  - **quran_ayahtranslation** (Stores translation text for individual ayahs, Related to account_customuser)
  - **quran_takhtit** (Stores Takhtit information, Related to quran_rasmolmushaf)
  - **quran_ayahbreaker** (Stores ayah boundary/breaking information, Related to account_customuser, quran_ayah,account_customuser, quran_takhtit)
  - **quran_wordbreaker** (Stores word boundary/breaking information, Related to account_customuser, quran_word, account_customuser, quran_takhtit)
  - **quran_recitation** (Stores Quran recitation information, Related to account_customuser, quran_transmission, account_customuser)
  - **quran_recitationsurah** (Associates a recitation with a surah and its audio file, Related to quran_recitation, quran_surah, core_file)
  - **quran_recitationsurahtimestamp** (Stores timestamps for recited surahs, Related to quran_recitationsurah, quran_word)
  - **quran_surahname** (Stores different names of a surah, Related to quran_surah)

### Infrastructure

- **CI/CD**: GitHub Actions
- **Hosting**:
  - Single standalone server (Linux) running Docker
- **Docker available containers**:
  - Django API
  - PostgreSQL

---

## 5. Pending Decisions

TBD

---

## 6. Timeline

TBD

---

## 7. Risks & Challenges

TBD

---

## 8. Success Metrics

TBD

---

## 9. Budget & Resources

- **Human Resources**: 1 developer
- **Hardware/Software Resources**: 1 server

---

## 10. Approval Signatures

| Role            | Github Account                                    |
| --------------- | ------------------------------------------------- |
| Curator         | [Al-Abd](https://github.com/al-abd)               |
| DevOps          | [codebysilence](https://github.com/codebysilence) |
| Project Manager |                                                   |
