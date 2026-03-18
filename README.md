# SUBTC-CLI-V2-Unified-Bitcoin-CLI-
SUBTC-CLI V2 — Unified Bitcoin CLI 

 `# SUBTC-CLI V2 — Unified Bitcoin CLI  Gateway V4.2 · Stateless · Idempotent · curl-first · Go CLI  ---  ## ⚡ Quick Start  install tools 🔥  ```bash go build -o subtc subtc-cli.go ` 
Run commands with `./subtc`:
 `./subtc key create ./subtc key status ./subtc config set-net test ./subtc wallet create ./subtc wallet receive <wid> ./subtc wallet balance <wid> ./subtc send <wid> <addr> 50000 ./subtc wait <wid> <addr> 30000 ./subtc poll <wid> <addr> 30000 --loop ./subtc health ./subtc config show `  
## 🔑 Key Management
 `./subtc key create                    # Create & save API key ./subtc key status                    # Check key status `  
## 🌐 Network
 `./subtc config set-net test           # testnet (default) ./subtc config set-net main           # mainnet (persistent) ./subtc --net=main <cmd>              # override temporarily SUBTC_NET=main ./subtc <cmd>          # override via environment `  
## 👛 Wallet
 `./subtc wallet create                 # Create wallet on current network ./subtc wallet list                   # List all wallets ./subtc wallet receive <wid>          # Generate receive address ./subtc wallet balance <wid>          # Show balance (SAT + BTC) `  
## 💸 Send
 `./subtc send <wid> <addr> <sat>               # Send (auto idempotency) ./subtc send <wid> <addr> <sat> <idem-key>    # Custom idempotency # mainnet: requires YES confirmation # Minimum: 50,000 sat · Fee: 3% `  
## ⏳ Wait / Poll
 `./subtc wait <wid> <addr> <sat>                        # long-poll (blocking) ./subtc wait <wid> <addr> <sat> <timeout_sec>          # custom timeout ./subtc wait <wid> <addr> <sat> 300 https://x.com/cb  # webhook mode  ./subtc poll <wid> <addr> <sat>                        # single poll ./subtc poll <wid> <addr> <sat> --loop                 # loop every 3 sec ./subtc poll <wid> <addr> <sat> --loop --interval=5    # loop every 5 sec `  
## ⚙️ Config
 `./subtc config show                   # Show current key & network ./subtc config set-key <key>          # Save API key ./subtc config set-net <test|main>    # Change default network `  
## 🏥 Health Check
 `./subtc health                        # Node status `  
## 🔧 Env Variables
 `SUBTC_KEY=xxx  ./subtc wallet list    # Override key SUBTC_NET=main ./subtc wallet create  # Override network `  
## 📌 Config File
 
`~/.subtc.json`
 `{   "key": "SUBTC-KEY-...",   "network": "test" } `  
## 💻 Examples from Tests (V2)
 `# Create Key ./subtc key create Key Created ✓ Key saved → ~/.subtc.json  # Check Key Status ./subtc key status {   "ok": true,   "request_id": "fcf859dae07b00d7",   "result": {     "key": "SUBTC-KEY-79821c194cd50ff0ce948920532fd8953a8c417de3d61c90",     "wallet_count": 0   } }  # Set Network ./subtc config set-net test ✓ Default network → testnet  # Create Wallet ./subtc wallet create Wallet Created · testnet wallet_id: w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2f2e  # Receive Address ./subtc wallet receive w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e Receive Address · testnet address: tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s  # Wallet Balance ./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e balance: 191849 sat  (0.00191849 BTC)  # Wait for Funds ./subtc wait w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s 30000 Waiting for Funds · testnet received: 191849 sat  (0.00191849 BTC)  # Send BTC ./subtc send w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000 ✓ Transaction broadcast txid: 26c264561605408253edec687c2f159f8c6dd0091f03b12b68969892e0086b1d sent_sat: 48500 sat fee_sat: 1500 sat  # Health Check ./subtc health {   "ok": true,   "configured": true,   "fee_bps": 300,   "min_send_sat": 20000 }  # Wallet Balance After Send ./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e balance: 91849 sat  (0.00091849 BTC)  # Show Config ./subtc config show key: SUBTC-KEY-79•••••••• network: test  testnet file: ~/.subtc.json env-override: SUBTC_KEY · SUBTC_NET `  
