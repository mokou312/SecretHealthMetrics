# 🧬 SecretHealthMetrics — Fully Encrypted Health Match (FHEVM dApp)

A decentralized **privacy-preserving health-compatibility matcher** built on **Zama’s FHEVM** (Sepolia testnet).
All user data — **age group, BMI category, blood pressure index** — is encrypted end-to-end, processed homomorphically on-chain, and never revealed to anyone, not even the validators.

✔ No plaintext data
✔ No metadata leakage
✔ 100% on-chain encrypted comparison
✔ Built with official **Zama FHEVM Solidity libraries** + **Relayer SDK v0.3.0**

---

## ✨ Features

* 🔐 **Encrypted Citizen Profiles**
  Age group, BMI category, and BP index submitted as encrypted FHE values.

* 🏙 **Encrypted Regional Thresholds**
  Regions define minimum/maximum encrypted criteria.

* 🧠 **Homomorphic On-Chain Matching**
  FHE comparisons (`FHE.ge`, `FHE.le`, `FHE.and`) compute compatibility entirely under encryption.

* 🎯 **Zero-Knowledge of Inputs**
  Neither nodes nor the contract sees any plaintext.

* 🔓 **Controlled Decryption**
  Users can privately decrypt match results or make them publicly decryptable.

* 🧊 **Modern Glassmorphic UI**
  Clean dual-column interface using pure HTML + CSS.

* 🔗 **Relayer SDK Powered**
  Fully integrated encrypted/frontend flows using Zama’s official tools.

---

## 🏗 Technology Stack

| Layer                   | Tools                                     |
| ----------------------- | ----------------------------------------- |
| Smart Contracts         | Solidity + Zama FHEVM (`@fhevm/solidity`) |
| Encryption / Decryption | Zama Relayer SDK v0.3.0                   |
| Frontend                | Vanilla JS, HTML, CSS                     |
| Wallet                  | MetaMask / any EIP-1193 provider          |
| Node Framework          | Hardhat                                   |
| Network                 | Sepolia FHEVM Testnet                     |

---

## 📦 Project Structure

```
tinderdao-private-match/
├── contracts/
│   └── SecretHealthMetrics.sol      # Main FHE health matching contract
├── deploy/                          # Deployment scripts
├── frontend/
│   └── index.html                   # UI + Relayer SDK integration
├── hardhat.config.js
├── package.json
└── README.md
```

---

## ⚙️ Smart Contract Overview

The `SecretHealthMetrics` contract uses **encrypted types**:

* `euint8` for age group & BMI category
* `euint16` for blood pressure index
* `ebool` for encrypted logical results

### Matching Logic (homomorphic)

```
ageOk = citizen.ageGroup ≥ region.minAgeGroup
bmiOk = citizen.bmiCategory ≤ region.maxBmiCategory
bpOk  = citizen.bpIndex ≤ region.maxBpIndex

match = ageOk AND bmiOk AND bpOk
```

All comparisons are done using **FHE operators**, and the final result is stored as an `euint8` (0 or 1).

Users (citizen or region owner) may privately decrypt or publish the result.

---

## 🚀 Quick Start

### **Prerequisites**

* Node.js ≥ 20
* npm / yarn / pnpm
* MetaMask or any injected Ethereum wallet
* Infura/Alchemy RPC key (Sepolia)

---

## 🔧 Installation

```bash
git clone https://github.com/mokou312/SecretHealthMetrics
cd SecretHealthMetrics
npm install
```

---

## 🔐 Environment Setup

```bash
npx hardhat vars set MNEMONIC
npx hardhat vars set INFURA_API_KEY
npx hardhat vars set ETHERSCAN_API_KEY   # optional
```

---

## 🧪 Compile & Test

```bash
npm run compile
npm run test
```

---

## 🛠 Local Deployment

Start a local FHEVM dev node:

```bash
npx hardhat node
```

Deploy:

```bash
npx hardhat deploy --network localhost
```

---

## 🌐 Deployment to Sepolia FHEVM

```bash
npx hardhat deploy --network sepolia
npx hardhat verify --network sepolia
```

**Latest Deployment Address:**
`0x3A32DDCDA724d8329E139ad60b98432D9C4A0cf2`

---

## 🖥 Frontend Integration (Relayer SDK)

Frontend uses:

* `@zama-fhe/relayer-sdk` v0.3.0
* `ethers.js` v6.13

### Workflow

1. Connect wallet
2. Encrypt health data using Relayer SDK
3. Submit encrypted profile / region thresholds
4. Compute FHE match via `computeHealthMatch()`
5. Make the result public (optional)
6. Public or private decrypt

Supports both **userDecrypt()** (private) and **publicDecrypt()**.

---

## 🔒 FHEVM Highlights

* Encrypted integer & boolean types
* Homomorphic logic: `FHE.le`, `FHE.ge`, `FHE.and`
* Secure access control:

  * `FHE.allow`
  * `FHE.allowThis`
  * `FHE.allowTransient`
* Public decryption: `FHE.makePubliclyDecryptable`
* Zero-Knowledge attestation of encrypted inputs

---

## 📚 Documentation

* **Zama FHEVM Overview**
  [https://docs.zama.ai/protocol](https://docs.zama.ai/protocol)

* **Relayer SDK Guide**
  [https://docs.zama.ai/protocol/relayer-sdk-guides/](https://docs.zama.ai/protocol/relayer-sdk-guides/)

* **Solidity FHE Library**
  [https://github.com/zama-ai/fhevm-solidity](https://github.com/zama-ai/fhevm-solidity)

* **Ethers.js v6**
  [https://docs.ethers.org/v6/](https://docs.ethers.org/v6/)

---

## 🆘 Support

* 🐛 GitHub Issues — bug reports & feature requests
* 💬 Zama Discord: **[https://discord.gg/zama-ai](https://discord.gg/zama-ai)**

---

## 📄 License

**BSD-3-Clause-Clear**
See the `/LICENSE` file for full details.

