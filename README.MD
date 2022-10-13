## A simple and quite interesting way to keep track of your cosmo-nodes.
Set it all up together

![1 (1)](https://user-images.githubusercontent.com/44331529/189982005-b4e0fe45-36a5-4a24-b824-eef923be2f11.png)

## download additional utilities
```console
sudo apt update && sudo apt upgrade -y &&
sudo apt install curl build-essential git wget jq make gcc tmux htop nvme-cli pkg-config libssl-dev lib
```

## docker 
```console
apt update && \
apt install apt-transport-https ca-certificates curl software-properties-common -y && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && \
apt update && \
apt-cache policy docker-ce && \
sudo apt install docker-ce -y && \
docker --version
```

## tenderduty
```console
tmux new-session -S tnd
mkdir tenderduty && cd tenderduty
docker run --rm ghcr.io/blockpane/tenderduty:latest -example-config >config.yml
```

## configuration
```console
nano $HOME/tenderduty/config.yml
```
### For simple monitoring without notifications, just change in the config:

+ network name:
+ chain-id:
+ valoper_address:
+ RPC url:

## Start
```console
docker run -d --name tenderduty -p "8888:8888" -p "28686:28686" --restart unless-stopped -v $(pwd)/config.yml:/var/lib/tenderduty/config.yml ghcr.io/blockpane/tenderduty:latest
```
## check logs
```console
docker logs -f --tail 50 tenderduty
```

## Let's check our monitoring in the browser
```console
echo -e "\033[0;32mhttp://$(wget -qO- eth0.me):8888/\033[0m"
# Exmp - http://1.0.0.111:8888/
```

## commands

## stop the container
```console
docker stop tenderduty
```
## restart the container
```console
docker restart tenderduty
```
## check logs
```console
docker logs -f --tail 50 tenderduty
```

