# 🛡️ StealthCheckout

**Privacy-preserving stablecoin payment gateway on HeLa blockchain.**

Merchants generate one-time stealth payment addresses for every invoice, so their wallet's transaction history stays private on public block explorers.

---

## Architecture

```
┌──────────────┐     ┌──────────────┐     ┌──────────────────┐
│  Customer    │────▶│  Payment     │────▶│  PaymentRouter   │
│  (Browser)   │     │  Page (React)│     │  (Smart Contract)│
└──────────────┘     └──────────────┘     └────────┬─────────┘
                                                   │
┌──────────────┐     ┌──────────────┐     ┌────────▼─────────┐
│  Merchant    │────▶│  Dashboard   │────▶│  StealthRegistry │
│  (Browser)   │     │  (React)     │     │  (Smart Contract)│
└──────────────┘     └──────────────┘     └──────────────────┘
                                          ┌──────────────────┐
                     ┌──────────────┐     │  HUSD Token      │
                     │  Backend     │────▶│  (ERC-20)        │
                     │  (Express)   │     └──────────────────┘
                     └──────────────┘     ┌──────────────────┐
                                          │  FeeManager      │
                                          └──────────────────┘
```

## Payment Flow

1. **Merchant registers** wallet + meta-public-key on `StealthRegistry`
2. **Merchant creates invoice** → `PaymentRouter.createInvoice()` → unique invoice ID generated, protocol fee charged
3. **Customer receives link** with QR code → `/pay/<invoiceId>`
4. **Customer pays** → `PaymentRouter.payInvoice()` → HUSD routed to merchant, invoice marked as paid (burned)
5. **Invoice is one-time** — replay and double-spend prevented

---

## Quick Start

### Prerequisites

- Node.js ≥ 18
- MetaMask browser extension
- HeLa testnet HLUSD (faucet: https://faucet-testnet.helachain.com)

### 1. Install Dependencies

```bash
# Root (smart contracts)
npm install

# Backend
cd backend && npm install

# Frontend
cd ../frontend && npm install
```

### 2. Compile & Deploy Contracts

```bash
# Compile
npx hardhat compile

# Deploy to HeLa testnet
# First set your private key:
# $env:PRIVATE_KEY = "your_private_key_here"
npx hardhat run scripts/deploy.js --network hela_testnet

# Or deploy locally:
npx hardhat node                         # Terminal 1
npx hardhat run scripts/deploy.js --network localhost  # Terminal 2
```

Copy the deployed addresses from the output.

### 3. Configure Backend

```bash
cd backend
cp .env.example .env
# Edit .env with your deployed contract addresses
```

### 4. Start Backend

```bash
cd backend
npm start
```

### 5. Start Frontend

```bash
cd frontend

# Create .env with contract addresses:
# VITE_HUSD_ADDRESS=0x...
# VITE_REGISTRY_ADDRESS=0x...
# VITE_ROUTER_ADDRESS=0x...
# VITE_FEE_MANAGER_ADDRESS=0x...

npm run dev
```

Open http://localhost:5173

---

## Project Structure

```
StealthCheckout/
├── contracts/
│   ├── HUSD.sol              # USD-pegged ERC-20 stablecoin
│   ├── StealthRegistry.sol   # Merchant registration + meta keys
│   ├── PaymentRouter.sol     # Invoice creation, payment routing
│   └── FeeManager.sol        # Protocol fee collection
├── scripts/
│   └── deploy.js             # Hardhat deployment script
├── backend/
│   ├── server.js             # Express server + event listener
│   ├── routes.js             # API routes
│   └── .env.example          # Environment template
├── frontend/
│   └── src/
│       ├── App.jsx           # Main app with routing
│       ├── config.js         # Contract addresses + ABIs
│       ├── useWallet.js      # MetaMask hook
│       └── pages/
│           ├── MerchantDashboard.jsx
│           └── CustomerPayment.jsx
├── sdk/
│   └── merchantCheckout.js   # JS SDK for contract interactions
├── hardhat.config.js
└── README.md
```

## Smart Contracts

| Contract | Purpose |
|----------|---------|
| `HUSD` | ERC-20 stablecoin with owner-only mint and public burn |
| `StealthRegistry` | Merchant registration with meta-public-key storage |
| `PaymentRouter` | One-time invoice creation, payment routing, replay protection |
| `FeeManager` | Configurable protocol fee (default 0.00402 HUSD) |

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
