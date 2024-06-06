# ECP Setup

## Prerequisites

* Need to map the ECP service port of the intranet to the public network, the default port is`9085`:

```
 <Intranet_IP>:<9085> --> <Public_IP>:<PORT>
```

* Running the `setup.sh`

```bash
curl -fsSL https://raw.githubusercontent.com/swanchain/go-computing-provider/releases/ubi/setup.sh | bash
```

* Download the v28 parameters for `ZK-FIL` task:

```bash
# At least 200G storage is needed
export PARENT_PATH="<V28_PARAMS_PATH>"

# 512MiB parameters
curl -fsSL https://raw.githubusercontent.com/swanchain/go-computing-provider/releases/ubi/fetch-param-512.sh | bash

# 32GiB parameters
curl -fsSL https://raw.githubusercontent.com/swanchain/go-computing-provider/releases/ubi/fetch-param-32.sh | bash

```

### Install ECP and Init CP Account

* Download `computing-provider`

```bash
wget https://github.com/swanchain/go-computing-provider/releases/download/v0.4.8/computing-provider
```

* Initialize ECP repo

```bash
 ./computing-provider init --multi-address=/ip4/<YOUR_PUBLIC_IP>/tcp/<YOUR_PORT> --node-name=<YOUR_NODE_NAME>
```

* Generate a new wallet address and deposit the `SWAN-ETH`, refer [here](https://docs.swanchain.io/swan-testnet/atom-accelerator-race/before-you-get-started/claim-sepoliaeth):

```bash
./computing-provider wallet new
```

Output:

```
 0x9024a875f44172591373b92...31d67AcCEa
```

* **\[OPTIONAL]** You can also import your own wallet by private key

```
./computing-provider wallet import private.key
```

> **Note:**
>
> 1. By default, the CP's repo is `~/.swan/computing`, you can configure it by `export CP_PATH="<YOUR_CP_PATH>"`
> 2. `private.key` is a file that contains the private key

* Initialize ECP Account

```bash
./computing-provider account create --ownerAddress <YOUR_WALLET_ADDRESS> --ubi-flag=true
```

### Start ECP service

```bash
#!/bin/bash
export FIL_PROOFS_PARAMETER_CACHE=$PARENT_PATH
export RUST_GPU_TOOLS_CUSTOM_GPU="GeForce RTX 4090:16384"   
        
nohup ./computing-provider ubi daemon >> cp.log 2>&1 &
```

**Note:**

* `<FIL_PROOFS_PARAMETER_CACHE>` is your parameters directory,
* `RUST_GPU_TOOLS_CUSTOM_GPU` is your GPU model and cores, you should update it to your own GPU model. More examples can be found [here](https://github.com/filecoin-project/bellperson?tab=readme-ov-file#supported--tested-cards)
* `<YOUR_PUBLIC_IP>`, `<YOUR_PORT>` are your public IP and port ,
* `<YOUR_NODE_NAME>` is your CP name which will show in the dashboard, If not specified, the default is `hostname`.
