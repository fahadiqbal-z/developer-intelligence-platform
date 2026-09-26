# Developer Intelligence Platform

**Creator:** Fahad Iqbal  
**Professional Identity:** Full-Stack Developer • Cybersecurity • AI Engineering • Creative Technology  
**Repository:** `developer-intelligence-platform`  
**License:** MIT

---

## 1. Executive Overview

The **Developer Intelligence Platform** is a dedicated developer workstation designed to inspect, analyze, document, debug, and understand complex software codebases.

Unlike superficial AI chatbot wrappers or mock dashboards with fabricated metrics, this application implements a functional developer workstation integrating:
- **Static AST & regex-based code analysis** for transparent security, reliability, maintainability, and performance findings.
- **Provider-abstracted AI service** that isolates untrusted code to prevent prompt injection and separates observed evidence from hypotheses.
- **Grounded context management** selecting relevant source files for contextual developer queries.
- **Inferred multi-tier architecture mapping** detecting Frontend, API, Business Logic, Persistence, and Test layers.
- **Interactive workstation UI** featuring a split-pane multi-file code editor, fast project-wide code search, findings management, editable documentation workspace, and report exports.

---

## 2. Core Capabilities

### A. Defensive Static Code Intelligence
- **Hardcoded Secret Detection:** Flags patterns matching API keys, secrets, private keys, and passwords.
- **Cryptographic Weakness:** Detects predictable pseudo-random number generators (`Math.random()`) used in authentication/token contexts.
- **DOM-based XSS Risk:** Scans for dangerous HTML injection (`dangerouslySetInnerHTML`, `.innerHTML =`).
- **SQL Injection Patterns:** Identifies unparameterized string concatenations in database queries.
- **Reliability Checks:** Catches empty catch blocks and swallowed exceptions.
- **Maintainability Rules:** Identifies lingering debug console logging in production files.

### B. Context-Aware Developer Assistant & Debugger
- **Structured Explanations:** Explains selected code functions with explicit inputs, outputs, operational flow, and potential failure modes.
- **Evidence-Grounded Debugger:** Takes error messages, stack traces, and expected behavior, returning problem hypotheses clearly distinguished from verified runtime evidence.
- **AI Code Review:** Evaluates maintainability, reliability, performance, and security without claiming code is 100% bug-free.

### C. Repository Architecture & Dependency Synthesis
- **Layer Detection:** Groups files into architectural tiers (Presentation, API routing, Business Services, Persistence, Testing).
- **Dependency Manifest Parsing:** Extracts dependencies and version constraints from `package.json`, `requirements.txt`, etc.
- **Transparent Health Indicators:** Reports factual indicators (tests detected, documentation detected, container configurations) rather than arbitrary scores.

### D. Documentation Workspace & Export
- **Automated Generation:** Generates grounded `README.md`, `API Reference`, `Architecture Specs`, and `Setup Guides`.
- **In-Browser Markdown Editor & Live Preview:** Edit, copy, and download documentation.
- **Multi-Format Export:** Generates consolidated Markdown and JSON audit reports.

---

## 3. Technology Stack

- **Frontend & Workstation UI:** Next.js (App Router), React 19, Tailwind CSS, Lucide Icons.
- **Code Highlighting & Viewing:** Highlight.js with GitHub Dark Dimmed styling.
- **Backend & API Architecture:** Next.js Server Route Handlers, NextRequest/NextResponse.
- **Data Persistence:** Prisma ORM with SQLite (local zero-config) / PostgreSQL (production-ready).
- **Security & Cryptography:** bcryptjs, jsonwebtoken, path traversal sanitizers, prompt delimiter isolation.
- **Archive Processing:** JSZip for in-memory, safe ZIP parsing with size enforcement.
- **Testing Suite:** Vitest for automated unit and integration tests.

---

## 4. Architecture

```text
┌────────────────────────────────────────────────────────┐
│                   Next.js App Router                   │
│   (Dashboard, Project Workstation, Code Editor, Search)│
└────────────┬─────────────────────────────┬─────────────┘
             │                             │
    HTTP API Layer                 Client Components
             │                             │
   ┌─────────┴─────────────┐               │
   │ API Route Controllers ├───────────────┘
   └─────────┬─────────────┘
             │
   ┌─────────┼─────────────────────────┐
   │         │                         │
┌──┴──┐  ┌───┴──────────┐       ┌──────┴──────────────┐
│ Auth│  │Static Engine │       │ Context AI Gateway  │
│ &   │  │(Regex & AST) │       │ (Mock / Cloud LLMs) │
│ JWT │  └──────────────┘       └─────────────────────┘
└──┬──┘              │                         │
   │                 └───────────┬─────────────┘
   ▼                             ▼
┌─────────────────────────────────────────────────────┐
│          Prisma ORM (SQLite / PostgreSQL)           │
└─────────────────────────────────────────────────────┘
```

---

## 5. Security & Prompt Injection Defense

1. **Untrusted Code Containment:** All uploaded or pasted user code is treated as untrusted data. When passed to language models, it is wrapped in isolated boundary delimiters (`### BEGIN UNTRUSTED CONTEXT`), neutralizing attempts to override system prompts.
2. **Path Traversal Protection (CWE-22):** All file paths are strictly sanitized against directory traversal attacks (`../`, `..\\`, null bytes).
3. **No Arbitrary Execution:** Uploaded or analyzed code is never executed or evaluated in shell processes.
4. **Credential Safety:** Server-side AI provider API keys are never exposed to browser bundles.

---

## 6. Installation & Local Development

### Prerequisites
- Node.js >= 18.0.0
- npm >= 9.0.0

### Step 1: Clone and Install
```bash
git clone https://github.com/fahadiqbal-z/developer-intelligence-platform.git
cd developer-intelligence-platform
npm install
```

### Step 2: Configure Environment
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```

### Step 3: Initialize Database & Seed Demo Project
```bash
npx prisma db push
npx tsx prisma/seed.ts
```

### Step 4: Run Test Suite
```bash
npx vitest run
```

### Step 5: Launch Development Server
```bash
npm run dev
```
Open `http://localhost:3000` in your browser.

---

## 7. Portfolio Case Study

### Problem
Software engineers frequently spend hours onboarding onto unfamiliar, legacy, or distributed codebases, struggling to understand execution flows, verify architectural boundaries, and locate defensive vulnerabilities.

### Solution
A high-precision developer workstation combining fast local static analysis with grounded contextual AI assistance, allowing developers to inspect file trees, identify security issues with transparent line markers, and generate truthful documentation without hallucinations.

### Engineering Challenges
- **Prompt Injection Defense:** Preventing malicious repositories from overriding LLM instructions through README or comment injection.
- **Air-Gapped & Offline Usability:** Ensuring the platform remains completely functional without external internet connectivity or expensive API keys using a deterministic provider abstraction.
- **Factual Integrity:** Eliminating fake "health scores" or unsubstantiated vulnerability claims in favor of verifiable evidence.

---

**Author:** Fahad Iqbal  
*Full-Stack Developer • Cybersecurity • AI Engineering • Creative Technology*
