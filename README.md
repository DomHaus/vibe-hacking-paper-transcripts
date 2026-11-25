# Vibe Hacking - Supplementary AI Transcripts

This repository contains the full prompts and generative-AI responses behind the paper:

> **Vibe Hacking: Using Accessible Generative AI for Hands-On IoT Hacking within the SEPP Platform**
> D. Hauser, S. Fischer — ICISSP 2027.
> (DOI / link: _add after publication_)

The paper reports the results in condensed form (see Table 1). This repository
provides the complete transcripts for transparency and reproducibility.

## Scope

Three hands-on IoT exercises from the SEPP course were attempted with three public and cost-free
available assistants (ChatGPT, Microsoft Copilot, Google Gemini), plus an automated
attack against the intentionally vulnerable VM *Metasploitable 2* via an MCP server.

| Folder | Content |
|---|---|
| `exercise-1-ble-dos/` | BLE information leak & DoS (Nuki smart lock) |
| `exercise-2-replay/`  | Network scan & replay attack (smart bulb) |
| `exercise-3-bruteforce/` | Brute-force attack (Siemens LOGO! web interface) |
| `automated-mcp/` | Automated exploitation of Metasploitable 2 via Gemini + MCP |

## Test setup

- Conducted in **September 2025** with the then-current free-tier versions:
  ChatGPT (GPT-5), Microsoft Copilot (model not disclosed by Microsoft),
  Google Gemini (2.5 Flash). The automated experiment used the free-tier
  Gemini 2.5 Pro API.
- All tests were run in a **controlled, isolated environment** on hardware owned
  by the authors' institution. No external or third-party systems were targeted.

## Responsible disclosure / redactions

Consistent with the paper, **working exploit code targeting real consumer devices
is redacted** (marked `[code omitted for security reasons]`). The transcripts show
the assistants' *behaviour* — when they refused, what unlocked assistance, and what
they were willing to produce — which is the object of study. Code targeting the
intentionally vulnerable *Metasploitable 2* training VM is included, as it is based
on publicly available material (Lieb & Schwarz, 2025) and poses no real-world risk.

Please use this material for educational and defensive research only.
