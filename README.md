# For IBFT2.0
## (Note: The steps given below are for the private gasless transaction)

## Step-0
#### Install Besu
https://besu.hyperledger.org/private-networks/get-started/install

## Step-1
#### Open atleast 4 terminal instance of Ubuntu or WSL
#### Each terminal will act as one independent node
<img width="1914" height="1017" alt="image" src="https://github.com/user-attachments/assets/1b805652-7010-4fe4-bf7b-43e7e1d49907" />

#### Change the directory where this repository is cloned

## Step-2
#### Run these command to each terminal stated properly
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

## Step-3
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

#### **--bootnode** value is the **enode url** present in the logs of Node-1
### See the highlighted text in picture for the reference

<img width="1919" height="1014" alt="image" src="https://github.com/user-attachments/assets/fa3aa9b7-6775-41c7-8635-db50c0bdc41f" />

### Paste the bootnode to from Node-1 to Node-2's **--bootnodes** flag
<img width="1919" height="1019" alt="image" src="https://github.com/user-attachments/assets/abd56077-a41b-4879-8bad-2d7bac7f2440" />

## Step-4
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
#### again the Node-1 enode url will be pasted at **--bootnodes** flag 
<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/e17df2da-c37a-4859-be1f-d84e6bf9e33b" />

## Step-5
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
##### same enode url here also
<img width="1919" height="1017" alt="image" src="https://github.com/user-attachments/assets/022f0bd2-27e5-451e-b449-7cc4e4dda4f9" />


## Private Blockchain with IBFT2.0 initialized
<img width="1914" height="1011" alt="image" src="https://github.com/user-attachments/assets/c7de9921-4937-471b-8c7f-d6d45d3408cf" />


### Now you can use **Hardhat**, **Foundry** or Remix to deploy the Smart Contracts
### You have 4 RPC URL for the 4 nodes. Use any one of the RPC URL to Deploy Smart Contract, send transactions and read the events on chain
