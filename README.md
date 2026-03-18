## SUBTC-CLI V2 — Unified Bitcoin CLI
Download: https://subtc.net/post/subtc-cli-v2-unified-bitcoin-cli

install tools
go build -o subtc subtc-cli.go

./subtc key create
./subtc key status
./subtc config set-net test
./subtc wallet create
./subtc wallet receive <wid>
./subtc wallet balance <wid>
./subtc send <wid> <addr> 50000
./subtc wait <wid> <addr> 30000
./subtc poll <wid> <addr> 30000 --loop
./subtc health
./subtc config show

./subtc key create
./subtc key status

./subtc config set-net test
./subtc config set-net main
./subtc --net=main <cmd>
SUBTC_NET=main ./subtc <cmd>

./subtc wallet create
./subtc wallet list
./subtc wallet receive <wid>
./subtc wallet balance <wid>

./subtc send <wid> <addr> <sat>
./subtc send <wid> <addr> <sat> <idem-key>

./subtc wait <wid> <addr> <sat>
./subtc wait <wid> <addr> <sat> <timeout_sec>
./subtc wait <wid> <addr> <sat> 300 https://x.com/cb
./subtc poll <wid> <addr> <sat>
./subtc poll <wid> <addr> <sat> --loop
./subtc poll <wid> <addr> <sat> --loop --interval=5

./subtc config show
./subtc config set-key <key>
./subtc config set-net <test|main>

./subtc health

SUBTC_KEY=xxx ./subtc wallet list
SUBTC_NET=main ./subtc wallet create

~/.subtc.json
{
  "key": "SUBTC-KEY-...",
  "network": "test"
}

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

./subtc config set-net test
✓ Default network → testnet

./subtc wallet create
Wallet Created · testnet
wallet_id: w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2f2e

./subtc wallet receive w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
Receive Address · testnet
address: tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s

./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
balance: 191849 sat

./subtc wait w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qhcy9w09yk22ppf3fdg6twnjh2zvgarf4zlsw4s 30000
received: 191849 sat

./subtc send w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000
✓ Transaction broadcast
txid: 26c264561605408253edec687c2f159f8c6dd0091f03b12b68969892e0086b1d
sent_sat: 48500 sat
fee_sat: 1500 sat

./subtc health
{
  "ok": true,
  "configured": true,
  "fee_bps": 300,
  "min_send_sat": 20000
}

./subtc wallet balance w_acfd7aa7e54f31d533c4f6eed2cf18c9c192957c2e
balance: 91849 sat

./subtc config show
key: SUBTC-KEY-79••••••••
network: test
file: ~/.subtc.json
env-override: SUBTC_KEY · SUBTC_NET
