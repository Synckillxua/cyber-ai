# AI CyberShield — AI-Powered Cybersecurity Intelligence Platform

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-2.3.3-black?style=for-the-badge&logo=flask)
![Google Gemini](https://img.shields.io/badge/Gemini-2.5%20Flash-orange?style=for-the-badge&logo=google)
![SQLite](https://img.shields.io/badge/SQLite-3-lightblue?style=for-the-badge&logo=sqlite)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**A production-ready, AI-driven cybersecurity analysis platform built on Flask and Google Gemini AI — designed to detect threats, assess vulnerabilities, and educate users in real time.**

[Features](#-core-features) • [Architecture](#-system-architecture) • [Installation](#-installation--setup) • [API Reference](#-api-reference) • [Security](#-security-considerations) • [Contact](#-contact)

</div>

---

## Table of Contents

- [Overview](#-overview)
- [Core Features](#-core-features)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Installation & Setup](#-installation--setup)
- [Environment Configuration](#-environment-configuration)
- [API Reference](#-api-reference)
- [Database Schema](#-database-schema)
- [Security Considerations](#-security-considerations)
- [Troubleshooting](#-troubleshooting)
- [Roadmap](#-roadmap)
- [License](#-license)
- [Contact](#-contact)

---

## Overview

**AI CyberShield** is a full-stack cybersecurity web application that leverages the power of **Google's Gemini 2.5 Flash** large language model to provide real-time threat intelligence and security analysis. The platform is designed for security analysts, developers, students, and everyday users who need fast, reliable cybersecurity assessments without deep technical expertise.

The system integrates a secure user authentication layer, a RESTful API backend, and an intuitive responsive frontend — making advanced AI-powered threat detection accessible through a browser.

---

## Core Features

### 🔍 Phishing Email Detector
- Submits email content to Gemini AI for natural language threat classification
- Returns a risk assessment: **Yes / No / Maybe** phishing
- Detects urgency manipulation, suspicious link patterns, and social engineering tactics
- Processes raw email text in real time with error-tolerant handling

### 🔐 Password Strength Analyzer
- Rates password security on a **1–10 scale** using AI evaluation
- Analyzes entropy, character diversity, length, and common patterns
- Provides actionable feedback to strengthen weak credentials
- Useful for security audits and user education workflows

### 🌐 Malicious URL Checker
- Classifies URLs as **Fraud / Genuine / Maybe** using AI domain analysis
- Detects spoofed brand domains, suspicious TLDs, and deceptive subdomains
- Cross-references URL structure against known phishing patterns
- Designed to flag lookalike domains targeting major platforms

### 💬 AI Cybersecurity Assistant
- Interactive chatbot powered by Gemini 2.5 Flash
- Answers security questions in concise, non-technical language
- Covers topics: password hygiene, 2FA, encryption, malware, social engineering
- Optimized prompt engineering for accurate, brief responses

### 🔒 Secure User Authentication
- User registration and login with hashed passwords (`werkzeug` PBKDF2-SHA256)
- Session management with configurable expiry (default: 30 minutes)
- Route-level access control via `login_required` decorator
- Flash messaging for real-time user feedback

---

## System Architecture

```
┌─────────────────────────────────────────────────────┐
│                     CLIENT LAYER                    │
│         Tailwind CSS + Vanilla JS Frontend          │
│   (landing.html / login.html / register.html /      │
│                    index.html)                      │
└──────────────────────┬──────────────────────────────┘
                       │ HTTP Requests
┌──────────────────────▼──────────────────────────────┐
│                   FLASK BACKEND                     │
│                                                     │
│  ┌──────────────┐   ┌──────────────────────────┐   │
│  │  Auth Routes  │   │     Analysis Routes      │   │
│  │  /login       │   │  /analyze/email          │   │
│  │  /register    │   │  /analyze/password       │   │
│  │  /logout      │   │  /analyze/url            │   │
│  └──────┬───────┘   │  /ask                    │   │
│         │            └────────────┬─────────────┘   │
│  ┌──────▼───────┐                 │                 │
│  │  SQLAlchemy  │   ┌─────────────▼──────────────┐  │
│  │  ORM Layer   │   │   Google Gemini AI Client  │  │
│  └──────┬───────┘   │   gemini-2.5-flash model   │  │
│         │            └────────────────────────────┘  │
└─────────┼───────────────────────────────────────────┘
          │
┌─────────▼───────┐
│   SQLite DB     │
│   users.db      │
└─────────────────┘
```

---

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Web Framework | Flask | 2.3.3 |
| ORM | Flask-SQLAlchemy | 3.1.1 |
| Password Hashing | Werkzeug | 2.3.7 |
| AI Model | Google Generative AI (Gemini) | 0.3.2 |
| Database | SQLite | Built-in |
| Environment Management | python-dotenv | 1.0.0 |
| HTTP Client | Requests | 2.31.0 |
| CSS Framework | Tailwind CSS | 2.2.19 |
| Icons | Font Awesome | 6.0.0 |
| Language | Python | 3.8+ |

---

## Installation & Setup

### Prerequisites

- Python **3.8 or higher**
- `pip` package manager
- A valid **Google Gemini API key** ([Get one free at Google AI Studio](https://aistudio.google.com/))
- Git

### Step-by-Step Installation

**1. Clone the repository**
```bash
git clone https://github.com/Synckillxua/cyber-ai.git
cd cyber-ai
```

**2. Create and activate a virtual environment**
```bash
# Windows
python -m venv venv
.\venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

**3. Install all dependencies**
```bash
pip install -r requirements.txt
```

**4. Configure environment variables**
```bash
# Create a .env file in the project root
cp .env.example .env   # or create manually
```
Edit `.env` and add your Gemini API key (see [Environment Configuration](#-environment-configuration)).

**5. Initialize the database**

The database is auto-created on first run via SQLAlchemy's `db.create_all()`.

**6. Run the development server**
```bash
python app.py
```

**7. Access the application**

Open your browser and navigate to: `http://localhost:5000`

---

## Environment Configuration

Create a `.env` file in the project root directory:

```env
GEMINI_API_KEY=your_google_gemini_api_key_here
```

> **Important:** Never commit your `.env` file. It is already excluded via `.gitignore`.

| Variable | Description | Required |
|----------|-------------|----------|
| `GEMINI_API_KEY` | Google Gemini API key for AI analysis | Yes |

---

## API Reference

All analysis endpoints accept `POST` requests with a JSON body and return JSON responses.

### `POST /analyze/email`
Analyze an email for phishing indicators.

**Request:**
```json
{
  "email": "URGENT: Your account has been compromised! Click here..."
}
```
**Response:**
```json
{
  "result": "Phishing analysis: Yes, this is likely a phishing attempt..."
}
```

---

### `POST /analyze/password`
Rate the strength of a password.

**Request:**
```json
{
  "password": "MyP@ssw0rd!2024"
}
```
**Response:**
```json
{
  "result": "Password strength: 8/10"
}
```

---

### `POST /analyze/url`
Check a URL for malicious indicators.

**Request:**
```json
{
  "url": "http://paypal-login-secure.com/verify"
}
```
**Response:**
```json
{
  "result": "URL safety check: Fraud — suspicious domain mimicking PayPal..."
}
```

---

### `POST /ask`
Ask the AI cybersecurity assistant a question.

**Request:**
```json
{
  "question": "What is two-factor authentication?"
}
```
**Response:**
```json
{
  "result": "Two-factor authentication (2FA) adds a second verification step..."
}
```

---

## Database Schema

```sql
CREATE TABLE user (
    id       INTEGER PRIMARY KEY AUTOINCREMENT,
    username VARCHAR(80)  UNIQUE NOT NULL,
    email    VARCHAR(120) UNIQUE NOT NULL,
    password VARCHAR(200) NOT NULL
);
```

Passwords are stored as **PBKDF2-SHA256 hashes** via `werkzeug.security.generate_password_hash` — plain-text passwords are never stored.

---

## Security Considerations

| Risk | Mitigation Applied |
|------|--------------------|
| API key exposure | Stored in `.env`, excluded from version control |
| Plain-text passwords | PBKDF2-SHA256 hashing via Werkzeug |
| Unauthorized access | `login_required` decorator on protected routes |
| Session hijacking | Server-side sessions with 30-minute expiry |
| SQL injection | Parameterized queries via SQLAlchemy ORM |

> **Note:** For production deployment, replace `app.secret_key = os.urandom(24)` with a fixed secret key stored in your `.env` file to maintain sessions across restarts.

---

## Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| `Error: API key not valid` | Missing or incorrect Gemini API key | Check `.env` file has correct `GEMINI_API_KEY` |
| `Empty response from AI` | Input too long or rate limited | Shorten the input or wait before retrying |
| `Username already exists` | Duplicate registration attempt | Use a different username or log in |
| `500 Internal Server Error` | Missing dependency or DB error | Run `pip install -r requirements.txt` |
| Sessions expiring too fast | Default 30-min timeout | Adjust `permanent_session_lifetime` in `app.py` |

---

## Roadmap

- [ ] Add `.env.example` template file for new contributors
- [ ] Implement rate limiting on analysis endpoints
- [ ] Add export report feature (PDF / JSON)
- [ ] Integrate VirusTotal API for URL cross-validation
- [ ] Deploy to cloud (Render / Railway / AWS)
- [ ] Add admin dashboard for user management
- [ ] Write unit and integration tests

---

## License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## Contact

**Ayush Roy**
- Email: [ayushroy6889@gmail.com](mailto:ayushroy6889@gmail.com)
- GitHub: [@Synckillxua](https://github.com/Synckillxua)
- Repository: [github.com/Synckillxua/cyber-ai](https://github.com/Synckillxua/cyber-ai)

---

<div align="center">
  Built with Python, Flask, and Google Gemini AI — for a more secure digital world.
</div>
