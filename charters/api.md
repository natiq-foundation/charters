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
  - Profile/{uuid}
  - Profile/me
  - Users/Users
  - Groups
- **Quran:**
  - Mushafs
  - Mushafs/import
  - Surahs
  - Ayahs
  - Words
  - Translations
  - Translations/{uuid}/ayahs
  - Translations/import
  - Recitations
  - Recitations/{uuid}/upload/{surah_uuid}
  - Takhtits
  - Takhtits/{uuid}/ayahs_breakers
  - Takhtits/{uuid}/word_brakers
  - Takhtits/{uuid}/import
- **Other:**
  - Phrases
  - Phrases/modify
  - Notifications
  - Notifications/me
  - Notifications/opened
  - Notifications/viewed
  - Health

#### DB Tables

- **Account:**
  - **account_customuser** (Stores user accounts and profile information)
    - Related to `auth_group` (Many-to-Many via field `groups`)
    - Related to `auth_permission` (Many-to-Many via field `user_permissions`, intermediary table `account_customuser_user_permissions`)

  - **account_customuser_groups** (Intermediate table for user-group relationships)  
      - Related to `account_customuser`
      - Related to `auth_group`

  - **account_customuser_user_permissions** (Intermediate table for user-permission relationships)  
    - Related to `account_customuser`
    - Related to `auth_permission`

  - **account_username** (Stores different names associated with users)  
      - Related to `account_customuser` (Many-to-One via `user`)

- **Core:**
  - **core_request** (Stores information about requests and responses)
    - No direct relationship to other tables

  - **core_publicdocument** (Stores publicly accessible documents)
    - No direct relationship to other tables

  - **core_file** (Stores uploaded file metadata and storage information)
    - Related to `account_customuser` (Many-to-One via `deleted_by`)
    - Related to `account_customuser` (Many-to-One via `uploader`)

  - **core_notification**
    - Related to `account_customuser` (Many-To-One via `user`)

- **Quran:**
  - **quran_rasmolmushaf** (Stores Rasm al-Mushaf information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `account_customuser` (Many-To-One via compiler)

  - **quran_romsurahayahs** (Associates a Rasm al-Mushaf with a Surah and Ayah)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `account_customuser` (Many-To-One via rasm_ol_mushaf)
    - Related to `account_customuser` (Many-To-One via surah)
    - Related to `account_customuser` (Many-To-One via ayah)

  - **quran_provenance** (Stores provenance information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `account_customuser` (Many-To-One via account)
    - Related to `self` (One-To-One via child_provenance)

  - **quran_transmission** (Stores Quran transmission information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_RasmOlMushaf` (Many-To-One via rasm_ol_mushaf)
    - Related to `quran_provenance` (Many-To-One via provenances)

  - **quran_surah** (Stores Quran surah information)
    - Related to `account_customuser` (Many-To-One via creator)

  - **quran_ayah** (Stores Quran ayah information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_surah` (Many-To-One via surah)

  - **quran_word** (Stores Quran word information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_ayah` (Many-To-One via ayah)

  - **quran_wordtext** (Stores text associated with Quran words)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_customuser` (Many-To-One via word)
    - Related to `quran_transmission` (Many-To-One via transmission)

  - **quran_translation** (Stores Quran translation information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_transmission` (Many-To-One via transmission)
    - Related to `account_customuser` (Many-To-One via translator)

  - **quran_ayahtranslation** (Stores translation text for individual ayahs)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_translation` (Many-To-One via translation)
    - Related to `quran_ayah` (Many-To-One via ayah)

  - **quran_takhtit** (Stores Takhtit information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_rasmolmushaf` (Many-To-One via rasm_ol_mushaf)
    - Related to `account_customuser` (Many-To-One via account)

  - **quran_ayahbreaker** (Stores ayah boundary/breaking information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_ayah` (Many-To-One via ayah)
    - Related to `account_customuser` (Many-To-One via owner)
    - Related to `quran_takhtit` (Many-To-One via takhtit)

  - **quran_wordbreaker** (Stores word boundary/breaking information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_word` (Many-To-One via word)
    - Related to `account_customuser` (Many-To-One via owner)
    - Related to `quran_takhtit` (Many-To-One via takhtit)

  - **quran_recitation** (Stores Quran recitation information)
    - Related to `account_customuser` (Many-To-One via creator)
    - Related to `quran_transmission` (Many-To-One via transmission)
    - Related to `account_customuser` (Many-To-One via reciter_account)

  - **quran_recitationsurah** (Associates a recitation with a surah and its audio file)
    - Related to `quran_recitation` (many-To-One via recitation)
    - Related to `quran_surah` (Many-To-One via surah)
    - Related to `core_file` (Many-To-One via file)

  - **quran_recitationsurahtimestamp** (Stores timestamps for recited surahs)
    - Related to `quran_recitationsurah` (Many-To-One via recitation_surah)
    - Related to `quran_word` (Many-To-One via word)

  - **quran_surahname** (Stores different names of a surah)
    - Related to `quran_surah` (Many-To-One via surah)

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
