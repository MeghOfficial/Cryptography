# 🔐 Hybrid Post-Quantum File Transfer Tool

> Combining **Elliptic Curve Diffie-Hellman (ECDH)** with **lattice-based LWE/Kyber** encryption to build a quantum-resistant secure file transfer system — deployed live on the web.

🌐 **Live Demo:** [hybrid-post-quantum-cryptography.vercel.app](https://hybrid-post-quantum-cryptography.vercel.app/)

---

## 📌 What Is This?

Modern encryption (like ECDH used in TLS, WhatsApp, Signal) is vulnerable to quantum computers running **Shor's Algorithm**. This project implements a **hybrid cryptographic system** that remains secure even if one of the underlying algorithms is broken — classical or quantum.

The hybrid key is derived as:
```
hybridKey = SHA-256(ECDH_shared_secret || LWE_shared_secret)
```
An attacker must break **both** ECDH and LWE simultaneously — which is computationally infeasible under current cryptanalytic knowledge.

---

## 🧠 Core Concepts

### 1. ECDH — Classical Security
- Elliptic Curve Diffie-Hellman over the **P-256 curve**
- Provides **128-bit classical security**
- Same primitive used in TLS 1.3, Signal Protocol, and WhatsApp

### 2. LWE / Kyber — Post-Quantum Security
- **Learning With Errors (LWE)**: a lattice-based hard problem believed to be resistant to quantum attacks
- Based on NIST Post-Quantum Cryptography standardization (2024)
- Even quantum computers running Shor's algorithm cannot efficiently solve LWE

### 3. Hybrid Key Combination
- Both shared secrets combined via **SHA-256**
- Resulting 256-bit hybrid key used for symmetric encryption
- Defense-in-depth: secure even if either primitive is eventually broken

### 4. AES-256-GCM File Encryption
- Files encrypted with **AES-256-GCM** using the hybrid key
- Same standard used by banks, governments, and cloud providers
- Authenticated encryption — tamper-proof output
- All processing done in-browser via **Web Crypto API** — no data leaves the device

---

## ✨ Features

- 🔒 **Hybrid key exchange** — ECDH + LWE running simultaneously
- 📁 **Real file encryption** — encrypt any file, download as `.hpqc`
- 🔓 **Decryption** — restore original file from `.hpqc` on the receiver side
- 🧮 **Math walkthrough** — interactive LWE demo with real matrix operations (n=4, q=97)
- 📖 **Full documentation** — How It Works, Math Details, Security Analysis pages
- 🌐 **Zero-install** — runs entirely in the browser using Web Crypto API
- 🚀 **Deployed on Vercel** — live and accessible

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (ES6+) |
| Cryptography | Web Crypto API (native browser) |
| Math Engine | Vanilla JS matrix operations for LWE simulation |
| Deployment | Vercel |

---

## 📁 Project Structure

```
Cryptography/
├── index.html          # Landing page — overview and features
├── how-it-works.html   # ECDH + LWE explained step by step
├── math-details.html   # Mathematical deep-dive into LWE
├── security.html       # Security analysis and threat modeling
├── demo.html           # Interactive encryption/decryption demo
├── about.html          # Project background and references
├── css/                # Stylesheets
├── js/                 # Cryptographic logic and UI
└── CryptoGraphy.pdf    # Project report / documentation
```

---

## 🔬 The LWE Hard Problem (Simplified)

Given a public matrix **A** and vector **b = A·s + e** (where **e** is a small random error):
- Finding secret **s** from **(A, b)** is computationally hard
- The added noise makes exact solving impossible
- Even quantum computers using Shor's algorithm cannot efficiently solve this

This "noisy linear equation" is the mathematical foundation of post-quantum security.

---

## 🛡️ Security Model

| Attack Scenario | ECDH Status | LWE Status | Hybrid Key |
|---|---|---|---|
| Classical computer attack | ✅ Secure | ✅ Secure | ✅ Secure |
| Quantum computer (Shor's) | ❌ Broken | ✅ Secure | ✅ Secure |
| Future lattice attack on LWE | ✅ Secure | ❌ Broken | ✅ Secure |
| Both broken simultaneously | ❌ | ❌ | ❌ (negligible probability) |

---

## 🚀 Run Locally

No installation needed. Just clone and open:

```bash
git clone https://github.com/MeghOfficial/Cryptography.git
cd Cryptography
# Open index.html in any modern browser
```

Or visit the live demo directly: [hybrid-post-quantum-cryptography.vercel.app](https://hybrid-post-quantum-cryptography.vercel.app/)

---

## 📚 References

- [NIST Post-Quantum Cryptography Standardization (2024)](https://csrc.nist.gov/projects/post-quantum-cryptography)
- [CRYSTALS-Kyber Specification](https://pq-crystals.org/kyber/)
- [Web Crypto API — MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
- [Learning With Errors — Regev, 2005](https://cims.nyu.edu/~regev/papers/qcrypto.pdf)

---

## 👤 About

Built by **Megh Bavarva**
- 📧 [bavarvamegh3139@gmail.com](mailto:bavarvamegh3139@gmail.com)
- 💼 [LinkedIn](https://www.linkedin.com/in/megh-bavarva-588b78284)
- 🐙 [GitHub](https://github.com/MeghOfficial)

---

> ⚠️ **Educational Demonstration** — This project is built to explore and demonstrate post-quantum cryptographic concepts. For production security systems, use audited libraries like [liboqs](https://github.com/open-quantum-safe/liboqs).
