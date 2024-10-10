# Zenchain Node Setup on Ubuntu 22.04 VPS with Docker

This guide provides step-by-step instructions for setting up a **Zenchain Node** on your **Ubuntu 22.04 VPS** using **Docker**.

## 🚀 Prerequisites

Before you begin, ensure that Docker is installed on your server.

### 1. Install Docker

Run the following commands to install Docker:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. (Optional) Allow Docker to run as a non-root user
This allows you to run Docker commands without sudo.
```bash
sudo usermod -aG docker $USER
newgrp docker
```

3. Verify Docker Installation
Ensure that Docker is correctly installed:
```bash
docker --version
```

📥 Steps to Run the Zenchain Node
1. Pull the Zenchain Docker Image
First, pull the latest Zenchain image from GitHub's Container Registry:
```
docker pull ghcr.io/zenchain-protocol/zenchain-testnet:latest
```

2. Create a Directory for Chain Data
Create a directory on your VPS to store the node's data:
```bash
mkdir -p ~/zenchain-data
```

3. Run the Zenchain Node in Production Mode
Now, run the Zenchain node in detached mode (background). This will start the node and persist its data in the ~/zenchain-data directory:
```
docker run -d \
  --name zenchain \
  -p 9944:9944 \
  -v ~/zenchain-data:/chain-data \
  ghcr.io/zenchain-protocol/zenchain-testnet:latest \
  ./usr/bin/zenchain-node \
  --base-path=/chain-data \
  --rpc-cors=all \
  --validator \
  --name="MyZenchainNode" \
  --bootnodes="/dns4/node-7242611732906999808-0.p2p.onfinality.io/tcp/26266/p2p/12D3KooWLAH3GejHmmchsvJpwDYkvacrBeAQbJrip5oZSymx5yrE" \
  --chain=zenchain_testnet
```
Explanation of the Command:
-d: Run in detached mode (background).
--name zenchain: Name the container zenchain.
-p 9944:9944: Expose port 9944 for RPC calls.
-v ~/zenchain-data:/chain-data: Mount local directory ~/zenchain-data for data persistence.
--base-path=/chain-data: Set the node data directory.
--rpc-cors=all: Enable CORS for RPC to allow external access.
--validator: Run as a validator node.
--name="MyZenchainNode": Assign a name to the node.
--bootnodes: Specify the bootnode for network discovery.
--chain=zenchain_testnet: Use the Zenchain testnet configuration.
```

4. Monitor Node Logs
To view the logs of the running Zenchain node, use:
```
docker logs -f zenchain
```
This will stream the logs in real time so you can monitor the syncing process and node status.


## References

- **[Zenquest](https://zenquest.zenchain.io?referral=tGaa_g1b0yk_O-J_e3hCaEUOpEe2rPN2tBlOWkXOvgA)**  
  You can participate in various Zenchain quests, earn rewards, and gain valuable incentives. This is an excellent starting point to become familiar with Zenchain’s ecosystem.

- **[Zenchain Faucet](https://faucet.zenchain.io/)**  
  The Zenchain Faucet provides testnet tokens to help you get started. 

## Useful Tools and Resources

- **[Zenchain Official Documentation](https://zenchain.io/docs)**  
  The official Zenchain documentation provides all the necessary details to understand, set up, and manage your Zenchain node.
- **[Zenchain GitHub Repository](https://github.com/zenchain-protocol)**  





