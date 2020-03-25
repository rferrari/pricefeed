# HIVE/STEEM Price Feed
A price feed application written in NodeJS for witnesses on the Hive or Steem network.

## Features
- Application resilience with NodeJS restart on crash/exit.
- Automatic RPC switching.
- Averaged price from up to 7 cryptocurrency exchanges.
- Supported exchanges: Binance, Bittrex, Huobi, Ionomy, Poloniex, Probit, Upbit

# Pre-install (e.g. Ubuntu 16.04)
Requires NodeJS >7.6 (for the async functions).
```
sudo apt update
sudo apt install -y curl software-properties-common gnupg build-essential libssl-dev
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm i npm@latest -g
```

# Docker Install (recommended)
```
sudo apt install -y jq
git clone https://github.com/Jolly-Pirate/pricefeed.git
cd pricefeed
chmod +x run.sh
./run.sh install_docker
./run.sh build
```
Edit the file `app/config.json` accordingly (see the Configuration section below), then start the container with
```
./run.sh start
```

Check that it's running fine with `./runs.sh logs`

Type `./run.sh` without arguments for a list of options.

---

# Npm Install
Alternatively to the docker installation procedure.

```
git clone https://github.com/Jolly-Pirate/pricefeed.git
cd pricefeed
cp app/config.json.example app/config.json
chmod 600 app/config.json
```

Edit the file `app/config.json` accordingly (see the Configuration section below), then start the app with
```
npm install
npm start
```

### Screen session example
Start and enter a screen session: `screen -S pricefeed`

Start the script: `npm start`

Detach from the screen session with `CTRL-a-d`. This will leave it running in the background.

Reattach to the session with `screen -x pricefeed` to monitor its status. 

If you want to terminate the script press `CTRL-c`, then type `exit` to close the session.

---

# Configuration
The configuration is located in the file `app/config.json`.

- witness: witness account
- privateActiveKey : private active key of the witness account
- interval : delay between each feed publishing.
- peg : set to true only if you want to adjust your price feed bias.
- peg_multi : if the peg is enabled, then this will change the "quote" to `1 / peg_multi`, e.g. a peg_multi of 2 it will show a 100% bias on the feed.
- testmode : when set to true, the script won't broadcast the price feed to the blockchain, good for testing or checking the price on the different exchanges
- hivechain/steemchain : select which blockchain to broadcast to, by setting only one of those options to `true`
- rpc: array of the Hive OR Steem RPC nodes (be careful not to mix RPC's from both blockchains)

The different exchanges can be enabled/disabled with `true` or `false`. Always keep an eye on the exchange prices and edit their setting accordingly.

# Acknowledgment
Some parts were based on someguy123's steemfeed-js and steem-in-a-box.
