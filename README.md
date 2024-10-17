# Light Client Setup Guide

This guide explains how to set up a light client using Docker, Go, and IPFS on Ubuntu, and how to create a burner wallet.

## 1. Create a Burner Wallet

1. Visit [VisualKey](https://visualkey.link/).
2. Generate a burner wallet.
3. Save the **address** and **private key** securely.

## 2. Install Docker

1. Install Docker using a single command:
   ```bash
   curl -fsSL https://get.docker.com | sudo bash
   

2. Verify Docker installation:
   
   docker --version
   

## 3. Install Go

1. Download and install Go:
   
   wget https://go.dev/dl/go1.22.3.linux-amd64.tar.gz
   sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
   

2. Set up environment variables for Go:
   
   echo "" >> ~/.bashrc
   echo 'export GOPATH=$HOME/go' >> ~/.bashrc
   echo 'export GOROOT=/usr/local/go' >> ~/.bashrc
   echo 'export GOBIN=$GOPATH/bin' >> ~/.bashrc
   echo 'export PATH=$PATH:/usr/local/go/bin:$GOBIN' >> ~/.bashrc
   source ~/.bashrc
   

3. Verify Go installation:
   
   go version
   

## 4. Install IPFS

1. Download and install IPFS (Kubo):
   
   wget https://dist.ipfs.tech/kubo/v0.30.0/kubo_v0.30.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.30.0_linux-amd64.tar.gz
   

2. Verify IPFS installation:
   
   ipfs --version
   

## 5. Clone the Repository

1. Navigate to your home directory:
   
   cd ~
   

2. Clone the ewm-das repository:
   
   git clone https://github.com/covalenthq/ewm-das
   cd ewm-das
   

## 6. Build the Docker Image

1. Build the Docker image:
   
   docker build -t covalent/light-client -f Dockerfile.lc .
   

## 7. Run the Docker Container

1. Run the Docker container using the private key from your burner wallet:


   
   docker run -d --restart always --name light-client -e PRIVATE_KEY="YOUR_HEX_PRIVATE_KEY" covalent/light-client
   

   Replace YOUR_HEX_PRIVATE_KEY with the private key you generated at [VisualKey](https://visualkey.link/). Delete the fist 0x on the private key.

## 8. Check the Container Status

1. View the container logs:
   
   docker logs -f light-client
   

   Example output:
   
   Version: v0.10.0, commit: 8d6709bee9e79d3c4e6ece35fed65da02f3850f4
   2024-09-18T15:45:01.238-0700    INFO    light-client    light-client/main.go:91    Starting client...
   2024-09-18T15:45:01.238-0700    INFO    light-client    light-client/main.go:97    Client identity: 0x51b6D674514849aF97FB77BCac51bcdD7799842C
   ...
   

## Additional Resources

- [Go Installation Guide](https://golang.org/doc/install)
- [Docker Documentation](https://docs.docker.com/get-started/)
- [IPFS Documentation](https://docs.ipfs.io/)
```
