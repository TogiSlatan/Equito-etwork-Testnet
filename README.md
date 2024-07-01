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

#

# Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```console

sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Add Docker's official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Use the following command to set up the stable repository.
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine:
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Verify that Docker Engine is installed correctly:
sudo docker --version
Step 2: Setup Folder Structure and Configuration
Create Folder Structure:

bash
Kodu kopyala
mkdir equito-testnet
cd equito-testnet
Download Configuration and Startup Script:

Download equito.yaml configuration file and start-full-node.sh startup script into equito-testnet folder.
Edit Configuration File (equito.yaml):

Open equito.yaml and edit it to include your private key and RPC endpoints for all networks.
Example (equito.yaml):

yaml
Kodu kopyala
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
# more networks ...
Replace <your-private-key> with your actual private key and configure RPC endpoints accordingly.

Step 3: Start Equito Full Node
Run Docker Containers:

Execute the following command in the equito-testnet folder:

bash
Kodu kopyala
bash start-full-node.sh <node-name>
Replace <node-name> with your desired node name (e.g., MyEquitoNode).

Verify Node Startup:

After starting the nodes, verify that the folder structure looks similar to this:

c
Kodu kopyala
├── equito-testnet
│   ├── start-full-node.sh
│   ├── equito.yaml
│   ├── equito-node
│   │   ├── p2p_secret
│   │   ├── ...
│   ├── logs
│   │   ├── equito-node.log
│   │   ├── equito-worker.log
Ensure p2p_secret is present for peer-to-peer communication between Substrate nodes.

Step 4: Manage Docker Containers
Stop Services:

To stop the services, run:

bash
Kodu kopyala
docker container stop equito-node
docker container stop equito-worker
Restart Services:

To restart the services, run:

bash
Kodu kopyala
docker container restart equito-node
docker container restart equito-worker# Equito-etwork-Testnet
Equito Full Node setup and configuration
