# 🛡️ HeLa Stealth

**Privacy-preserving stablecoin payment gateway on HeLa blockchain.**

HeLa Stealth allows merchants to accept stablecoin payments with complete privacy. By generating one-time stealth payment addresses for every invoice, a merchant's main wallet transaction history remains shielded on public block explorers.

![HeLa Landing Page](C:\Users\risha\.gemini\antigravity\brain\3dda39d3-ba76-43d0-8223-e95083e6a228\hela_landing_page_final_1773542514094.png)

---

## Live Deployment (HeLa Testnet)

The project is fully operational on the **HeLa Testnet**.

### Smart Contracts
| Contract | Address |
|----------|---------|
| **HUSD** | `0xEf3cA15C04e82b90B01AF9EccE1A0C620E74E0b3` |
| **StealthRegistry** | `0x71741409c2F568735748D40F232Be35d43a48661` |
| **FeeManager** | `0xEA5399958B5848eBd835F888f4310e6b7D84B0Fb` |
| **PrivacyPool** | `0x098abE69A28b897d18E998a5F73Fc777e48fe365` |
| **PaymentRouter** | `0x15334Ef0e00F29F5ecCb03D765982F1282B05df8` |

---

## Key Features

1. **HeLa Brand Alignment**: Sleek, professional UI with the HeLa teal palette and glassmorphism.
2. **Stealth Payments**: One-time invoice IDs and stealth vaults protect user privacy.
3. **One-Chain Privacy**: Leverages HeLa's native privacy features on a single, intelligent blockchain.
4. **Seamless UX**: Unified "Connect Wallet" flow and high-impact hero design.

![Merchant Dashboard](C:\Users\risha\.gemini\antigravity\brain\3dda39d3-ba76-43d0-8223-e95083e6a228\merchant_dashboard_final_verify_1773542852945.png)

---

## Quick Start (Local Development)

### Prerequisites
- Node.js ≥ 18
- MetaMask browser extension
- HeLa testnet HLUSD

### 1. Install Dependencies
```bash
npm install && cd backend && npm install && cd ../frontend && npm install
```

### 2. Configure & Run
```bash
# Backend
cd backend && cp .env.example .env && npm start

# Frontend
cd frontend && cp .env.example .env && npm run dev
```

---

## Security & Architecture

- **One-time addresses**: Invoices are single-use, preventing linkability.
- **Atomic Operations**: Router handles deposit and release in a single transaction.
- **HeLa Privacy**: Built to leverage the unique privacy-preserving capabilities of the HeLa blockchain.

---

## 🚀 V2 Roadmap: Advanced Privacy Packets

To combat **Amount Correlation Analysis** (preventing hackers from linking large unique payments across wallets), HeLa Stealth V2 will introduce **High-Frequency Dynamic Splitting**:

### 📦 Privacy Tiers (High-Range Packets)
Users can select a "Privacy Package" with massive randomization ranges:

| Tier | Packet Split Range | Security Effect | Gas Profile |
|------|--------------------|-----------------|-------------|
| **Standard** | 1 (Fixed) | Basic Privacy | ⚡ High Speed |
| **Iron Shield** | 50 – 100 Packets | Stealth Mixing | 🛡️ Secure |
| **Gold Ghost** | 200 – 500 Packets | Trace-Breaking | 👻 Maximum |
| **Infinite Shadow** | 1000+ Packets | Total Obfuscation | 🌌 Extreme |

### 🛠️ The Technical Vision
1.  **Fragmented Deposits**: A 5,000 HUSD payment is atomized into *hundreds* of random small amounts (e.g., 1.04, 15.6, 0.99...) impossible to link back to a single 5k transaction.
2.  **Cross-Block Staggering**: Packets are deployed across different blocks over time, defeating temporal correlation.
3.  **Fragmented Withdrawal**: Merchants can choose to withdraw specific packets or the whole set, providing ultimate control over their wallet's transaction fingerprint.

---

## 🚀 V2 Roadmap: Advanced Privacy Packets

To combat **Amount Correlation Analysis** (where hackers link large unique amounts across wallets), HeLa Stealth V2 will introduce **Dynamic Packet Splitting**:

### 📦 Privacy Tiers
Users can select a "Privacy Package" with dynamic splitting ranges:

| Tier | Packet Range | Privacy Level | Gas Efficiency |
|------|--------------|---------------|----------------|
| **Standard** | 1 (Fixed) | Basic | ⚡ High |
| **Stealth Plus** | 5 – 15 Packets | Enhanced | 🛡️ Medium |
| **Ghost Mode** | 20 – 50 Packets | Maximum | 👻 Low |

### 🛠️ How it Works
1.  **Dynamic Splitting**: A 10,000 HUSD payment is automatically broken into *randomized* amounts (e.g., 402, 1290, 88...) based on the selected range.
2.  **Time-Staggered Deposits**: Packets can be sent over multiple blocks to break time-based correlation.
3.  **Fragmented Withdrawal**: Merchants can withdraw individual packets separately, making the incoming funds appear as hundreds of unrelated small transactions.

---

Built for the **HeLa Hackathon** 🚀
rotocol fee (default 0.00402 HUSD) |

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/merchant/register` | Register merchant on-chain |
| `POST` | `/invoice/create` | Create payment invoice |
| `GET` | `/invoice/status/:id` | Check invoice status |
| `GET` | `/merchant/invoices/:address` | List merchant invoices |

## Security

- **One-time addresses**: Invoices are single-use, burned after payment
- **Replay protection**: Nonce-based invoice IDs prevent replay attacks
- **ReentrancyGuard**: Payment functions protected against reentrancy
- **Access control**: Mint is owner-only, invoices are merchant-only

## HeLa Chain Config

| Property | Value |
|----------|-------|
| Chain ID | `666888` |
| RPC | `https://testnet-rpc.helachain.com` |
| Explorer | `https://testnet-blockexplorer.helachain.com` |
| Currency | `HLUSD` |

---

Built for hackathon deployment on **HeLa blockchain** 🚀
