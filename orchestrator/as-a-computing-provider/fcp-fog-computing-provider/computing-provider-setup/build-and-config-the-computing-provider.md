# Build and config the Computing Provider

Step1: Firstly, clone the code to your local:

```bash
git clone https://github.com/swanchain/go-computing-provider.git
cd go-computing-provider
git checkout releases
```

Step2: Then build the Computing provider follow the below steps:

```bash
make clean && make
make install
```

Step3: Update Configuration The computing provider's configuration sample locate in `./go-computing-provider/config.toml.sample`

```
cp config.toml.sample config.toml
```

Step4: Update your configuration file (config.toml) as follows, paying special attention to the newly added `HUB`, `RPC`, and `CONTRACT`sections:

```toml
[API]
Port = 8085                                    # The port number that the web server listens on
MultiAddress = "/ip4/<public_ip>/tcp/<port>"   # The multiAddress for libp2p
Domain = ""                                    # The domain name
NodeName = ""                                  # The computing-provider node name

RedisUrl = "redis://127.0.0.1:6379"            # The redis server address
RedisPassword = ""                             # The redis server access password
WalletWhiteList = ""                           # CP only accepts user addresses from this whitelist for space deployment

[UBI]
UbiTask = true                                                # Accept the UBI task (Default: true)
UbiEnginePk = "0xB5aeb540B4895cd024c1625E146684940A849ED9"    # UBI Engine's public key, CP only accept the task from this UBI engine 
UbiUrl ="https://ubi-task.swanchain.io/v1"                    # UBI Engine's API address

[LOG]
CrtFile = "/YOUR_DOMAIN_NAME_CRT_PATH/server.crt"             # Your domain name SSL .crt file path
KeyFile = "/YOUR_DOMAIN_NAME_KEY_PATH/server.key"             # Your domain name SSL .key file path

[HUB]
ServerUrl = "https://orchestrator-api.swanchain.io"           # The Orchestrator's API address
AccessToken = ""                                              # The Orchestrator's access token, Acquired from "https://orchestrator.swanchain.io" 
WalletAddress = ""                                            # The cp‘s wallet address
BalanceThreshold= 1                                            # The cp’s collateral balance threshold
OrchestratorPk = "0x29eD49c8E973696D07E7927f748F6E5Eacd5516D"  # Orchestrator's public key, CP only accept the task from this Orchestrator
VerifySign = true                                              # Verify that the task signature is from Orchestrator


[MCS]
ApiKey = ""                                   # Acquired from "https://www.multichain.storage" -> setting -> Create API Key
BucketName = ""                               # Acquired from "https://www.multichain.storage" -> bucket -> Add Bucket
Network = "polygon.mainnet"                   # polygon.mainnet for mainnet, polygon.mumbai for testnet
FileCachePath = "/tmp"                        # Cache directory of job data

[Registry]
ServerAddress = ""                            # The docker container image registry address, if only a single node, you can ignore
UserName = ""                                 # The login username, if only a single node, you can ignore
Password = ""                                 # The login password, if only a single node, you can ignore

[RPC]
SWAN_TESTNET ="https://rpc-proxima.swanchain.io"  # Swan testnet RPC
SWAN_MAINNET= ""								   # Swan mainnet RPC

[CONTRACT]
SWAN_CONTRACT="0x91B25A65b295F0405552A4bbB77879ab5e38166c"              # Swan token's contract address
SWAN_COLLATERAL_CONTRACT="0xfD9190027cd42Fc4f653Dfd9c4c45aeBAf0ae063"   # Swan's collateral address
```

**Note:** _Note:_ Example WalletWhiteList hosted on GitHub can be found [here](https://raw.githubusercontent.com/swanchain/market-providers/main/clients/whitelist.txt).
