# Prerequisites
Hardware Requirements:

CPU Cores: Minimum 4 cores
RAM: Minimum 8 GB
Disk Space: Minimum 8 GB
Network Bandwidth: Stable and fast internet connection
Storage Type: SSD recommended for better performance
Software Requirements:

64-bit Linux operating system (Ubuntu 22.04)
Docker installed and configured
Step 1: Install Docker on Ubuntu 22.04
If Docker is not already installed, follow these steps to install it:

```console

# Step 1: Installing Docker on Ubuntu 22.04
If Docker is not installed, follow these steps to install it:


# Update the apt package index and install packages to allow apt to use a repository over HTTPS:
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up the stable repository for Docker Engine:
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine:
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Verify that Docker Engine is installed correctly:
sudo docker --version


# Step 2: Setting Up Folder Structure and Configuration
Create the folder structure:

mkdir equito-testnet
cd equito-testnet

# Download the equito.yaml configuration file and start-full-node.sh startup script into the equito-testnet directory.

# Step 3: Editing the Configuration File (equito.yaml)
Open equito.yaml and edit it to include your private key and RPC endpoints for all networks. Here is an example configuration:

private-key: 0x<your-private-key>
evm:
  - chain: Ethereum
    id: 1
    endpoint:
      https: ethereum.infura.io/v3/<API-KEY>
      wss: ethereum.infura.io/ws/v3/<API-KEY>
  - chain: BSC
    id: 56
    endpoint: bsc-rpc.my-rpc-provider.com

Add more networks as needed
Replace <your-private-key> with your actual private key and configure RPC endpoints accordingly.

# Step 4: Starting the Equito Full Node
Run the following command in the equito-testnet directory:

bash start-full-node.sh <node-name>

# Replace <node-name> with your desired node name (e.g., MyEquitoNode).

# Verifying Node Startup
After starting the nodes, ensure your folder structure resembles:

├── equito-testnet
│   ├── start-full-node.sh
│   ├── equito.yaml
│   ├── equito-node
│   │   ├── p2p_secret
│   │   ├── ...
│   ├── logs
│   │   ├── equito-node.log
│   │   ├── equito-worker.log

# Ensure the p2p_secret file is present for peer-to-peer communication between Substrate nodes.

# Step 5: Managing Docker Containers
To stop services:

docker container stop equito-node
docker container stop equito-worker

# To restart services:

docker container restart equito-node
docker container restart equito-worker

# This guide provides a comprehensive overview of setting up an Equito Full Node on Ubuntu 22.04 using Docker. Adjust configurations and commands as needed based on your specific setup and requirements.

