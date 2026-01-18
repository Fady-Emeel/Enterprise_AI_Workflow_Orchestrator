# 🏦 Enterprise AI Support Orchestrator (Applied AI Project)

This project demonstrates how **Applied AI** can be used to build **reliable, enterprise-grade AI systems** for banking and payments support — focusing on **structure, safety, and business integration**, not just model outputs.

It was built as a hands-on application of:
- **LangChain for LLM Application Development**
- **Building Systems with the ChatGPT API** (system design concepts applied locally)

---

## 🎯 Problem Statement

In real organizations, customer support messages are:
- Unstructured
- Inconsistent
- Risky to automate blindly (especially in banking & payments)

This project solves that by turning raw customer messages into **controlled, auditable, and actionable workflows**.

---

## 🧠 What This System Does

The system acts as an **AI-powered workflow orchestrator** for banking support:

### 1️⃣ Intake (Understanding the Message)
- Accepts raw customer messages (email, chat, ticket)
- Extracts:
  - Intent (e.g. `payment_failure`, `refund_request`)
  - Urgency level
  - Missing required information
  - Confidence score
- Enforces **strict JSON schema** using Pydantic

### 2️⃣ Guardrails & Routing (Enterprise Logic)
Based on confidence, intent, and completeness:
- Ask the user for missing info
- Retrieve answers from internal policy documents (RAG)
- Create a support ticket
- Escalate to a human agent

No unsafe free-form automation.

### 3️⃣ RAG (Retrieval-Augmented Generation)
- Uses **LangChain + FAISS**
- Retrieves answers strictly from internal documents
- Prevents hallucinations
- Includes source traceability

### 4️⃣ Memory & Auditability
- Stores conversation history
- Logs every decision with timestamps
- Designed for compliance and review

---

## 🏗️ Architecture Overview

```text
User Message
     ↓
Intake Chain (LLM + Schema)
     ↓
Intent Normalization
     ↓
Decision Router
 ┌─────────┬──────────┬──────────┐
 │ Ask User│   RAG    │  Tools   │
 │ Missing │ (Policies)│ (Tickets)│
 │ Info    │          │          │
 └─────────┴──────────┴──────────┘
     ↓
Memory + Logs
