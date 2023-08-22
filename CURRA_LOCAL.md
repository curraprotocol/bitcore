# Guide how to run bitcore node for local development (by Curra team)

### Before start

Before the start you have to run bitcoin node. See our installation [guide](./CURRA_BITCOIN_INSTALL_OSX.md)

Then, run bitcoin node locally in regtest mode:

1. Create `bitcoin.conf` file in the directory `~/Library/Application Support/Bitcoin` (create this folder if it not exists) with following content:

   ```
   whitelist=127.0.0.1

   [regtest]
   port=20008
   rpcport=20009
   rpcallowip=127.0.0.1

   rpcuser=curra
   rpcpassword=curra
   ```

2. Run the node and create your first wallet to interact with blockchain:

   ```zsh
   bitcoind -regtest

   # open new terminal and run
   bitcoin-cli -regtest createwallet dev
   bitcoin-cli -regtest generatetoaddress 101 $(bitcoin-cli -regtest getnewaddress)
   bitcoin-cli -regtest getbalance

   # to find another command check the docs https://developer.bitcoin.org/reference/rpc/index.html
   # after each node restart run the next command to load your wallet

   bitcoin-cli -regtest loadwallet dev
   ```

### Run bitcore node

Create `bitcore.config.json` file with following content

```json
{
  "bitcoreNode": {
    "chains": {
      "BTC": {
        "regtest": {
          "chainSource": "p2p",
          "trustedPeers": [
            {
              "host": "127.0.0.1",
              "port": 20008
            }
          ],
          "rpc": {
            "host": "127.0.0.1",
            "port": 20009,
            "username": "curra",
            "password": "curra"
          }
        }
      }
    }
  },
  "blockchainExplorerOpts": {
    "btc": {
      "livenet": {
        "url": "https://api.bitcore.io"
      },
      "testnet": {
        "url": "http://localhost:3000",
        "regtestEnabled": true
      }
    }
  }
}
```

Then run following commands

```
npm i
npm run node
```

### Run bitcore wallet service
