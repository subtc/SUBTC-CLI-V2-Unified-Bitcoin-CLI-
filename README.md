🚀 SUBTC-CLI V2 — Unified Bitcoin CLI

One CLI to Rule Both Mainnet & Testnet


Download: https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli

---

✨ What's New in V2

Feature V1 V2
Mainnet ❌ ✅
Testnet ✅ ✅
Network Switching ❌ ✅ (config, flag, env)
Idempotent Sends ✅ ✅ (enhanced)
Webhooks ❌ ✅
Polling Intervals ❌ ✅ (--interval)

---

⚡ Quick Start

```bash
# Build
go build -o subtc subtc-cli.go

# Create API key
./subtc key create

# Set network (test/main)
./subtc config set-net test

# Create wallet
./subtc wallet create

# Get address
./subtc wallet receive <wallet_id>

# Check balance
./subtc wallet balance <wallet_id>

# Send BTC
./subtc send <wallet_id> <address> 50000

# Wait for payment
./subtc wait <wallet_id> <address> 30000

# Poll until confirmed
./subtc poll <wallet_id> <address> 30000 --loop
```

---

🌐 Network Control (V2 Superpower)

Set Default

```bash
./subtc config set-net test   # testnet
./subtc config set-net main   # mainnet
```

Per-Command Override

```bash
# Flag
./subtc --net=main wallet create

# Environment
SUBTC_NET=main ./subtc wallet create

# Precedence: flag > env > config
```

---

🔑 Key Management

```bash
./subtc key create      # Generate & save
./subtc key status      # Verify current
```

---

💼 Wallet Ops

```bash
./subtc wallet create                 # New wallet
./subtc wallet list                   # All wallets
./subtc wallet receive <wid>          # Generate address
./subtc wallet balance <wid>          # Check balance
```

---

💸 Send BTC

```bash
# Auto idempotency key
./subtc send <wid> <addr> 50000

# Custom idempotency key (safe to retry)
./subtc send <wid> <addr> 50000 my-unique-id
```

Example:

```bash
./subtc send w_abc123 tb1q... 50000
# ✓ Transaction broadcast
# txid: 26c2645616...
# sent_sat: 48500
# fee_sat: 1500
```

---

⏳ Wait & Poll

Wait (Long-Poll)

```bash
./subtc wait <wid> <addr> 30000          # 300s timeout
./subtc wait <wid> <addr> 30000 600      # Custom timeout
./subtc wait <wid> <addr> 30000 300 https://x.com/cb  # Webhook
```

Poll (Check & Loop)

```bash
./subtc poll <wid> <addr> 30000                     # Single check
./subtc poll <wid> <addr> 30000 --loop              # Loop (3s interval)
./subtc poll <wid> <addr> 30000 --loop --interval=5 # Custom interval
```

---

⚙️ Config

```bash
./subtc config show                         # View current
./subtc config set-key <key>                 # Set API key
./subtc config set-net <test|main>           # Set network
./subtc health                               # Node status
```

Config file: ~/.subtc.json

```json
{
  "key": "SUBTC-KEY-xxx",
  "network": "test"
}
```

Environment override:

```bash
SUBTC_KEY=xxx ./subtc wallet list
SUBTC_NET=main ./subtc wallet create
```

---

📝 Real Test Output (V2)

```bash
$ ./subtc key create
Key Created
✓ Key saved → ~/.subtc.json

$ ./subtc config set-net test
✓ Default network → testnet

$ ./subtc wallet create
Wallet Created · testnet
wallet_id: w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2f2e

$ ./subtc wallet receive w_acfd7aa7e54f...
Receive Address · testnet
address: tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s

$ ./subtc wallet balance w_acfd7aa7e54f...
balance: 191849 sat

$ ./subtc send w_acfd7aa7e54f... tb1q... 50000
✓ Transaction broadcast
txid: 26c264561605408253edec687c2f159f8c6dd0091f03b12b68969892e0086b1d
sent_sat: 48500 sat
fee_sat: 1500 sat

$ ./subtc health
{
  "ok": true,
  "configured": true,
  "fee_bps": 300,
  "min_send_sat": 20000
}
```

---

🧠 Why V2 Matters

· Unified: Same tool for testing (testnet) and production (mainnet)
· Idempotent: Never double-spend — safe to retry
· Flexible: Network switching via config, flag, or env
· Programmable: Webhooks, custom timeouts, polling loops
· Lightweight: Single Go binary, zero dependencies

---

🔮 Coming Soon

Version Features
V3 Docker containers
V4 Tor support + Onion endpoints
V5 AI Agent integration

---

📚 Docs & Links

· Full API: https://subtc.net/api
· LLMs: https://subtc.net/llms-full.txt
· Download V2: https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli
· License: Apache 2.0

---

One CLI. Both networks. Zero borders. 🧅🔓
