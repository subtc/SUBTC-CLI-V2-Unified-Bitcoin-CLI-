🚀 SUBTC-CLI V2 — Unified Bitcoin CLI

One CLI to rule both mainnet and testnet Bitcoin transactions.

https://img.shields.io/badge/version-2.0.0-blue.svg
https://img.shields.io/badge/go-1.21+-00ADD8.svg
https://img.shields.io/badge/license-Apache%202.0-green.svg
https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.subtc.net%2Fstats%2Fcli&query=%24.downloads&label=downloads&color=orange

Download the binary directly from: https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli

---

✨ What's New in V2

Feature V1 (Testnet only) V2 (Unified)
Mainnet Support ❌ ✅
Testnet Support ✅ ✅
Network Switching ❌ ✅ (config, flag, env)
Idempotent Sends ✅ ✅ (enhanced)
Webhook Callbacks ❌ ✅
Configurable Timeouts ⚠️ Limited ✅ Full
Docker Ready ❌ ✅ (Coming V3)
Tor Support ❌ ✅ (Coming V4)

---

⚡ Quick Start

```bash
# 1. Build from source
go build -o subtc subtc-cli.go

# 2. Create your API key
./subtc key create

# 3. Set network (testnet for testing)
./subtc config set-net test

# 4. Create a wallet
./subtc wallet create

# 5. Generate receive address
./subtc wallet receive <wallet_id>

# 6. Check balance
./subtc wallet balance <wallet_id>

# 7. Send Bitcoin
./subtc send <wallet_id> <address> 50000
```

---

📋 Table of Contents

· Installation
· Network Configuration
· Key Management
· Wallet Operations
· Sending Bitcoin
· Waiting & Polling
· Configuration
· Environment Variables
· Examples
· API Reference
· Roadmap
· License

---

🔧 Installation

Option 1: Build from Source (Recommended)

```bash
# Clone or download subtc-cli.go
https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli

# Build
go build -o subtc subtc-cli.go

# Move to PATH (optional)
sudo mv subtc /usr/local/bin/
```

Option 2: Download Binary

Grab the latest binary for your platform from our download page.

Option 3: Docker (Coming in V3)

```bash
# Stay tuned for V3!
docker pull subtc/cli:v3
```

---

🌐 Network Configuration

V2 introduces unified network support — switch between testnet and mainnet seamlessly.

Set Default Network

```bash
# Set testnet as default
./subtc config set-net test

# Set mainnet as default
./subtc config set-net main
```

Per-Command Network Override

```bash
# Override with flag
./subtc --net=main wallet create

# Override with environment variable
SUBTC_NET=main ./subtc wallet create
```

Network Precedence

1. --net flag (highest)
2. SUBTC_NET environment variable
3. Config file (~/.subtc.json)
4. Default: test (safe default)

---

🔑 Key Management

```bash
# Create new API key
./subtc key create

# Verify current key
./subtc key status
```

Example output:

```
./subtc key create
Key Created
✓ Key saved → ~/.subtc.json

./subtc key status
{
  "ok": true,
  "request_id": "fcf859dae07b00d7",
  "result": {
    "key": "SUBTC-KEY-79821c194cd50ff0ce948920532fd8953a8c417de3d61c90",
    "wallet_count": 0
  }
}
```

---

💼 Wallet Operations

```bash
# Create new wallet (uses default network)
./subtc wallet create

# List all wallets
./subtc wallet list

# Generate receive address
./subtc wallet receive <wallet_id>

# Check balance
./subtc wallet balance <wallet_id>
```

Example workflow:

```bash
./subtc config set-net test
./subtc wallet create
# Wallet Created · testnet
# wallet_id: w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2f2e

./subtc wallet receive w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
# Receive Address · testnet
# address: tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s

./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
# balance: 191849 sat
```

---

💸 Sending Bitcoin

```bash
# Simple send (auto-generates idempotency key)
./subtc send <wallet_id> <address> <sat>

# Send with custom idempotency key (safe to retry)
./subtc send <wallet_id> <address> <sat> <idem-key>
```

Example:

```bash
./subtc send w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000

# ✓ Transaction broadcast
# txid: 26c264561605408253edec687c2f159f8c6dd0091f03b12b68969892e0086b1d
# sent_sat: 48500 sat
# fee_sat: 1500 sat
```

Fee Structure

· Service fee: 3%
· Minimum send: 20,000 SAT
· Network: Automatically detected from wallet

---

⏳ Waiting & Polling

Wait (Long-Poll)

Block until payment received or timeout:

```bash
# Basic wait (default timeout: 300s)
./subtc wait <wallet_id> <address> <sat>

# Custom timeout (seconds)
./subtc wait <wallet_id> <address> <sat> 300

# With webhook callback
./subtc wait <wallet_id> <address> <sat> 300 https://yourserver.com/webhook
```

Example:

```bash
./subtc wait w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s 30000
# received: 191849 sat
```

Poll (Check & Loop)

```bash
# Single poll check
./subtc poll <wallet_id> <address> <sat>

# Poll in loop until confirmed
./subtc poll <wallet_id> <address> <sat> --loop

# Custom interval (default: 3s)
./subtc poll <wallet_id> <address> <sat> --loop --interval=5
```

---

⚙️ Configuration

```bash
# Show current configuration
./subtc config show

# Set API key
./subtc config set-key <key>

# Set default network
./subtc config set-net <test|main>

# Check node health
./subtc health
```

Example output:

```bash
./subtc config show
key: SUBTC-KEY-79••••••••
network: test
file: ~/.subtc.json
env-override: SUBTC_KEY · SUBTC_NET

./subtc health
{
  "ok": true,
  "configured": true,
  "fee_bps": 300,
  "min_send_sat": 20000
}
```

Config File (~/.subtc.json)

```json
{
  "key": "SUBTC-KEY-79821c194cd50ff0ce948920532fd8953a8c417de3d61c90",
  "network": "test"
}
```

---

🌍 Environment Variables

Override config file settings:

Variable Purpose Example
SUBTC_KEY API key override SUBTC_KEY=xxx ./subtc wallet list
SUBTC_NET Network override SUBTC_NET=main ./subtc wallet create

Precedence: Flag > Env > Config

---

📝 Examples from Tests

Complete Workflow

```bash
# 1. Create key
./subtc key create
# Key Created
# ✓ Key saved → ~/.subtc.json

# 2. Verify key
./subtc key status
# {
#   "ok": true,
#   "request_id": "fcf859dae07b00d7",
#   "result": {
#     "key": "SUBTC-KEY-79821c194cd50ff0ce948920532fd8953a8c417de3d61c90",
#     "wallet_count": 0
#   }
# }

# 3. Set network to testnet
./subtc config set-net test
# ✓ Default network → testnet

# 4. Create wallet
./subtc wallet create
# Wallet Created · testnet
# wallet_id: w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2f2e

# 5. Generate address
./subtc wallet receive w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
# Receive Address · testnet
# address: tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s

# 6. Check balance
./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
# balance: 191849 sat

# 7. Wait for incoming payment
./subtc wait w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s 30000
# received: 191849 sat

# 8. Send Bitcoin
./subtc send w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000
# ✓ Transaction broadcast
# txid: 26c264561605408253edec687c2f159f8c6dd0091f03b12b68969892e0086b1d
# sent_sat: 48500 sat
# fee_sat: 1500 sat

# 9. Check updated balance
./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
# balance: 91849 sat

# 10. Health check
./subtc health
# {
#   "ok": true,
#   "configured": true,
#   "fee_bps": 300,
#   "min_send_sat": 20000
# }

# 11. Show config
./subtc config show
# key: SUBTC-KEY-79••••••••
# network: test
# file: ~/.subtc.json
# env-override: SUBTC_KEY · SUBTC_NET
```

---

📚 API Reference

Full API documentation available at:

· REST API: https://subtc.net/api
· LLM-friendly version: https://subtc.net/llms-full.txt
· Tor endpoint: Coming in V4

---

🗺️ Roadmap

Version Features Status
V1 Testnet-only CLI ✅ Released
V2 Mainnet + Testnet + Go 🚀 Today!
V3 Docker containers 🔜 Coming Soon
V4 Tor support + Onion endpoints 🔜 Coming Soon
V5 AI Agent integration 🤖 Planned

---

🤝 Contributing

Contributions are welcome! This is open source for a reason:

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

Or just download the binary and start building!

---

📄 License

Apache 2.0 License — free for commercial and personal use.

---

🌐 Connect

· Website: https://subtc.net
· API Docs: https://subtc.net/api
· Download V2: https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli
· GitHub Issues: Create an issue

---

⚡ Built for Freedom

SUBTC-CLI is designed to work everywhere — regardless of geographic restrictions. Combined with our distributed proxy infrastructure and upcoming Tor support, we're building tools that respect your right to access financial technology.

No borders. No blocks. Just Bitcoin. 🧅🔓

---

One CLI to rule them all.
V2 is out. Go build something. 🚀
