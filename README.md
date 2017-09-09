# CoppercoinMasterNode
Compiled Coppercoin Masternode for Linux Ubuntu 14.04

UBUNTU 14.04 IS NEEDED

Port to be opened on your server
TCP 22 YOUR_IP_ADDRESS/22 
TCP 22951 0.0.0.0/0 
TCP 22952 0.0.0.0/0

Set up a swapfile if your system has less than 1.5GB of memory:

sudo fallocate -l 2G /swapfile sudo chown root:root /swapfile sudo chmod 0600 /swapfile sudo mkswap /swapfile sudo swapon /swapfile

If fallocate doesn’t work, you can use dd if=/dev/zero of=/swapfile bs=1024 count=1024288 instead.

Initialize swapfile automatically on boot

sudo nano /etc/fstab Add this at the bottom: /swapfile none swap sw 0 0

#now install all required dependencies:

sudo apt-get update 
sudo apt-get upgrade 
sudo apt-get install build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev git libssl1.0.0-dbg 
sudo apt-get install libdb-dev libdb++-dev libboost-all-dev libminiupnpc-dev libminiupnpc-dev libevent-dev libcrypto++-dev libgmp3-dev

#now pull the source code from github, or upload it yourself:

git clone https://github.com/coppercoinet/CoppercoinMasterNode.git

#now change directory 

cd CopperCoinMasterNode

#now extract the binary

tar -xzvf coppercoin-daemon-linux.tar.gz
chmod +x coppercoind sudo mv coppercoind /usr/bin/

#now come back one directory

cd ..

#now edit the configuration file

mkdir .coppercoin

nano $HOME/.coppercoin/coppercoin.conf

rpcuser=rpc_coppercoin 
rpcpassword=08f7cc761957eb4e3bcbc40d8 
rpcallowip=127.0.0.1 
listen=1 
server=1 
txindex=1 
daemon=1

#now launch the screen to run Coppercoin Masternode

screen -dmS CopperCoin-MasterNode 
screen -x CopperCoin-MasterNode

#now run the daemon

coppercoind
