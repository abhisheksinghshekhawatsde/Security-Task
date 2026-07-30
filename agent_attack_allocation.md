# Skynet Dual-Agent Security Test & Attack Allocation Matrix

**Target System:** Skynet AI Application  
**Date:** July 30, 2026  

---

## 1. Executive Summary

A comprehensive security test case simulation was conducted on **Skynet**.

The primary objective of this test was to evaluate Skynet's resilience against **Prompt Injection (Direct & Indirect)**, **System Prompt & Memory Leakage**, **Tool Abuse / Function Injection**, **LangGraph State Hijacking**, **Vector Database Poisoning**, **Algorithmic Bias & Regulatory Bypasses**, **Financial Logic Hallucinations**, **PII Data Exfiltration**, **Obfuscation Evasion**, and **Denial of Service (DoS)** attacks.

A total of **550 adversarial test cases** across **11 Attack Modules** were developed, mapped, and executed against the Skynet.

---

## 2. Problem Statement & Testing Dilemma

During initial attack planning, an challenge was identified: **Skynet is not a single chatbot**. It consists of **two distinct, specialized sub-agents** with fundamentally different input interfaces and operational capabilities:

1. **Doc Insights Agent (Agent 1):** An interactive conversational RAG agent that answers user and retrieves policy details from the internal vector database via a **Chat UI**.
2. **Xdlc Suite (Agent 2):** A specialized document ingestion and generation engine that accepts user file uploads (PDF, DOCX, scans) and produces technical specification documents (LLD, HLD, PRD, BRD) via a **File Upload UI**.

### The Testing Efficiency Challenge

Executing all 550 test cases twice (once on Doc Agent and once on xDSC Suite) would result in **1,100 total executions**, creating massive redundancy, resource exhaustion, and testing delay. Conversely, testing only one agent or running file upload attacks on a chat box would leave critical security blind spots.

---

## 3. Attack Allocation & Attack Surface Mapping (The Solution)

To achieve 100% comprehensive security coverage without operational redundancy, we implemented **Capability-Aligned Threat Allocation**. Each of the 11 Attack Modules was mapped exclusively to the agent possessing the specific interface, toolset, and attack surface to handle that threat vector.

```text
┌─────────────────────────────────────────┐
│           SKYNET AI SYSTEM              │
└────────────────────┬────────────────────┘
                     │
┌────────────────────┴────────────────────┐
▼                                         ▼

┌───────────────────────────┐   ┌───────────────────────────┐
│ AGENT 1: DOC AGENT        │   │ AGENT 2: XDLC SUITE       │
├───────────────────────────┤   ├───────────────────────────┤
│ Interface: Chat UI        │   │ Interface: File Upload UI │
│ Capability: Q&A / RAG     │   │ Capability: Doc Generator │
│ Focus: System Prompts,    │   │ Focus: Ingestion, Parsers,│
│ Tools, Logic & Reasoning  │   │ PII, File DoS & Vectors   │
└─────────────┬─────────────┘   └─────────────┬─────────────┘
              │                               │
              ▼                               ▼

      6 Chat-Based Attack Files      5 File-Based Attack Files
      (01, 03, 05, 07, 08, 10)       (02, 04, 06, 09, 11)
```

### Threat Allocation Matrix

| Module ID | Attack Module File | Allocated Agent | Attack Surface & Rationale |
|:----------|:-------------------|:---------------:|:---------------------------|
| **Module 01** | `01. direct prompt injection.md` | **Doc Agent** | Direct user chat inputs attempting to override persona and system rules. |
| **Module 02** | `02. indirect prompt injection.md` | **xDSC Suite** | Adversarial text hidden inside uploaded PDF/DOCX files targeting LLD/HLD generation. |
| **Module 03** | `03. system prompt & memory leakage.md` | **Doc Agent** | Probing chat context, LangGraph state buffers, and memory history for system prompt text. |
| **Module 04** | `04. tool abuse & function injection.md` | **xDSC Suite** | Exploiting file conversion tools, path traversal (`../etc/passwd`), and OS command execution via file uploads. |
| **Module 05** | `05. langgraph state & routing hijack.md` | **Doc Agent** | Manipulating conditional router edges, `StateGraph` variables, and supervisor node transitions in chat loops. |
| **Module 06** | `06. vector db & rag poisoning.md` | **xDSC Suite** | Ingesting malicious vector chunks via uploaded files to poison the master spec generation index. |
| **Module 07** | `07. bias fairness & regulatory manipulation.md` | **Doc Agent** | Probing demographic bias (gender/pincode), fair lending compliance, and RBI policy overrides in chat. |
| **Module 08** | `08. hallucination logic & edge cases.md` | **Doc Agent** | Testing financial math paradoxes (EMI/IRR), non-existent product hallucinations, and negative input boundaries. |
| **Module 09** | `09. pii & financial data exfiltration.md` | **xDSC Suite** | Testing whether uploaded customer documents leak unmasked PAN/Aadhaar/PII into generated output docs. |
| **Module 10** | `10. encoding obfuscation & polyglot.md` | **Doc Agent** | Testing Base64, LeetSpeak, homoglyphs, and zero-width spaces in chat to evade pre-execution guardrail regex. |
| **Module 11** | `11. denial of service & resource exhaustion.md` | **xDSC Suite** | Testing decompression bombs (zip bombs), 1,000-page PDFs, high-DPI OCR locks, and file parser worker crashes. |

---

## 4. Organization of Part B Test Results

To maintain clean segregation of audit artifacts, the test execution logs and master vulnerability reports are structured into dedicated agent subdirectories within `Part B/`:

```text
security_task/Part B/
├── agent_attack_allocation.md     <-- (This Document) Strategy & Threat Mapping
│
├── agent_1_doc_agent/             <-- Interactive Chat Agent Audit Artifacts
│   ├── skynet_test_results.csv    <-- 300 Executed Chat Test Case Results
│   └── doc_agent_audit_report.md  <-- Detailed Vulnerability & Risk Assessment Report
│
└── agent_2_xdsc_suite/            <-- Document Processing Suite Audit Artifacts
    ├── xdsc_test_results.csv      <-- 250 Executed Document Upload Test Case Results
    └── xdsc_suite_audit_report.md <-- Detailed Vulnerability & Risk Assessment Report
```

---

## 5. Summary of Overall Audit Findings

Across both agents, a total of **550 test cases** were executed:

- **Doc Agent (Agent 1): 300 Test Cases Executed**
  - **00 Passed (00.0%)**
  - **00 Failed (00.0%)**

- **Xdlc Suite (Agent 2): 250 Test Cases Executed**
  - **00 Passed (00.0%)**
  - **00 Failed (00.0%)**

- **Total System Pass Rate: 00.0%**
