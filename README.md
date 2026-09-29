# Scrypt

### Cryptographic Attribution and Immutable Decryption Provenance for Multi-Recipient Encrypted Document Distribution

> **Smart India Hackathon 2026 — Project X**

[![SIH 2026](https://img.shields.io/badge/SIH%202026-Project%20X-2E7D5B)](https://www.sih.gov.in/)
[![Post--Quantum Cryptography](https://img.shields.io/badge/Cryptography-Post--Quantum-17233C)](https://csrc.nist.gov/pubs/fips/203/final)
[![Blockchain](https://img.shields.io/badge/Ledger-CometBFT-D97832)](https://github.com/cometbft/cometbft)

---

## Problem Statement

**Problem Statement ID:** 2024273  
**Theme:** Blockchain & Cybersecurity  
**Category:** Software  
**Organization:** Ministry of Defence  
**Department:** Indian Navy (WESEE)  
**Team ID:** 141798  
**Team Name:** Project X

### The Problem

In a multi-recipient encrypted document distribution system, the same encrypted document can be distributed to multiple authorized recipients.

Once decrypted, however, each recipient receives a visually identical plaintext document.

If one of those copies is later leaked, conventional encryption and server-side logs may not provide a reliable cryptographic connection between the leaked visual artifact and the exact decryption event that produced it.

Scrypt addresses this attribution gap.

---

#  What is Scrypt?

**Scrypt** is an offline, post-quantum document provenance system that connects:

**Encryption → Decryption → Session Fingerprint → Watermark → Digital Signature → Immutable Ledger → Forensic Recovery**

At every authorized decryption, Scrypt generates a fresh forensic fingerprint and embeds it invisibly into the rendered document.

The resulting provenance record is cryptographically signed by the recipient and committed to a private, air-gapped distributed ledger.

If a copy of the document is later recovered — including a visual artifact such as an image or screenshot — the embedded fingerprint can be extracted and used to locate and verify the corresponding provenance record.

---

# Core Idea

```text
                    ORIGINAL DOCUMENT
                           │
                           ▼
                  AES-256-GCM ENCRYPTION
                           │
                           ▼
                  MULTI-RECIPIENT PACKAGE
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
     RECIPIENT A      RECIPIENT B      RECIPIENT C
          │                │                │
          ▼                ▼                ▼
      DECRYPTION       DECRYPTION       DECRYPTION
          │                │                │
          ▼                ▼                ▼
    UNIQUE SESSION    UNIQUE SESSION    UNIQUE SESSION
     FINGERPRINT       FINGERPRINT       FINGERPRINT
          │                │                │
          ▼                ▼                ▼
     WATERMARK        WATERMARK        WATERMARK
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                 SIGNED PROVENANCE EVENT
                           │
                           ▼
                    COMETBFT LEDGER
                           │
                           ▼
                    WATERMARKED COPY
                           │
                           ▼
                    LEAKED ARTIFACT
                           │
                           ▼
                 FORENSIC EXTRACTION
                           │
                           ▼
                  CRYPTOGRAPHICALLY
                  VERIFIED PROVENANCE
