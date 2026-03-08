# For IBFT2.0
## (Note: The steps given below are for the private gasless transaction)

## Step-1
#### Install Besu(Ubuntu)

Check the Java version
```
java --version
```

The Java version must be 21 or higher. If not, update it.

#### Besu Installation latest version - https://github.com/hyperledger/besu/releases 

```
wget https://github.com/hyperledger/besu/releases/download/26.2.0/besu-26.2.0-bin.tar.gz
```

#### Extract
```
tar xvf besu-*-bin.tar.gz
```

#### Add to PATH
```
echo 'export PATH="$HOME/besu/bin:$PATH"' >> ~/.bashrc
```

```
source ~/.bashrc
```

#### Run
```
besu --help
besu --version
```

## Step-2
#### Clone this repository
```
git clone git@github.com:Herb-Supply-Chain/IBFT-Network.git
```

```
cd IBFT-Network
```

## Step-2
#### Generate node keys and a genesis file

```
besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key
```

## Step-3 
Move the four key folders, each containing key and key.pub files, to the **Node-1/data**, **Node-2/data**, **Node-3/data**, and **Node-4/data** directories respectively

```
networkFiles/
├── genesis.json
└── keys
    ├── 0x438821c42b812fecdcea7fe8235806a412712fc0
    │   ├── key
    │   └── key.pub
    ├── 0xca9c2dfa62f4589827c0dd7dcf48259aa29f22f5
    │   ├── key
    │   └── key.pub
    ├── 0xcd5629bd37155608a0c9b28c4fd19310d53b3184
    │   ├── key
    │   └── key.pub
    └── 0xe96825c5ab8d145b9eeca1aba7ea3695e034911a
        ├── key
        └── key.pub
```


```
IBFT-Network/
├── genesis.json
├── Node-1
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-2
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-3
│   ├── data
│   │    ├── key
│   │    ├── key.pub
├── Node-4
│   ├── data
│   │    ├── key
│   │    ├── key.pub
```

## Step-4
Copy the **genesis.json** to the **IBFT-Network** directory as shown above in the folder tree


## Step-5
#### Open at least 4 terminal instances of Ubuntu or WSL
#### Each terminal will act as one independent node
<img width="1914" height="1017" alt="image" src="https://github.com/user-attachments/assets/1b805652-7010-4fe4-bf7b-43e7e1d49907" />

#### Change to the directory where this repository is cloned

## Step-6
#### Run these commands in each terminal as stated below
### Terminal 1
```
besu --data-path=data \
 --genesis-file=../genesis.json \
 --rpc-http-enabled\
 --rpc-http-api=ETH,NET,IBFT \
 --host-allowlist="*" \
 --rpc-http-cors-origins="all" \
 --min-gas-price=0 \
 --api-gas-price-max=0 \
 --profile=ENTERPRISE
```
<img width="1907" height="1021" alt="image" src="https://github.com/user-attachments/assets/3d65ae33-db82-44e7-a65d-534a1ac8d36b" />

## Step-7
### Terminal 2
```
besu --data-path=data \
--genesis-file=../genesis.json \
--p2p-port=30304 \
--rpc-http-enabled \
--rpc-http-api=ETH,NET,IBFT \
--host-allowlist="*" \
--rpc-http-cors-origins="all" \
--rpc-http-port=8546 \
--min-gas-price=0 \
--api-gas-price-max=0 \
--profile=ENTERPRISE \
--bootnodes=
```

**--bootnodes** value is the **enode URL** present in the logs of Node-1
See the highlighted text in the picture for reference

<img width="1919" height="1014" alt="image" src="https://github.com/user-attachments/assets/fa3aa9b7-6775-41c7-8635-db50c0bdc41f" />

Paste the bootnode from Node-1 to Node-2's **--bootnodes** flag
<img width="1919" height="1019" alt="image" src="https://github.com/user-attachments/assets/abd56077-a41b-4879-8bad-2d7bac7f2440" />

## Step-8
### Terminal 3
```
besu --data-path=data \
--genesis-file=../genesis.json \
--p2p-port=30305 \
--rpc-http-enabled \
--rpc-http-api=ETH,NET,IBFT \
--host-allowlist="*" \
--rpc-http-cors-origins="all" \
--rpc-http-port=8547 \
--min-gas-price=0 \
--api-gas-price-max=0 \
--profile=ENTERPRISE \
--bootnodes=
```
again the Node-1 enode URL will be pasted in the **--bootnodes** flag 
<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/e17df2da-c37a-4859-be1f-d84e6bf9e33b" />

## Step-9
### Terminal 4
```  
besu --data-path=data \
--genesis-file=../genesis.json \
--p2p-port=30306 \
--rpc-http-enabled \
--rpc-http-api=ETH,NET,IBFT \
--host-allowlist="*" \
--rpc-http-cors-origins="all" \
--rpc-http-port=8548 \
--min-gas-price=0 \
--api-gas-price-max=0 \
--profile=ENTERPRISE \
--bootnodes=
```
The same enode URL here as well
<img width="1919" height="1017" alt="image" src="https://github.com/user-attachments/assets/022f0bd2-27e5-451e-b449-7cc4e4dda4f9" />


## Private Blockchain with IBFT2.0 initialized
<img width="1914" height="1011" alt="image" src="https://github.com/user-attachments/assets/c7de9921-4937-471b-8c7f-d6d45d3408cf" />


Now you can use **Hardhat**, **Foundry**, or **Remix** to deploy smart contracts
You have 4 RPC URLs for the 4 nodes. Use any one of the RPC URLs to deploy smart contracts, send transactions, and read events on the chain

More nodes can be added; you just have to change the **--p2p-port** and **--rpc-http-port** to the next sequential numbers

#### For more information, refer to https://besu.hyperledger.org/private-networks/tutorials/ibft