# canto-snapshots  

## Run your own backup server with snapshots  
Install requirements  
```bash
sudo apt update && \
sudo apt install curl git docker.io -y
```

Clone github repo  
```bash
git clone https://github.com/SiddarthVijay/cosmos-snapshots.git
cd cosmos-snapshots
git checkout patch/canto
```

Create folder for snapshots  
`mkdir -p $HOME/snapshots/canto`

Start Nginx via docker  
```bash
sudo docker run --name canto-snapshots \
--restart always \
-v $(pwd)/default.conf:/etc/nginx/conf.d/default.conf \
-v $HOME/snapshots/canto:/root/ \
-p 80:80 \
-d nginx
```

Edit config if required by editing variables in the file `canto_snapshot.sh`  
```
CHAIN_ID="canto_7700-1"
SNAP_PATH="$HOME/snapshots/canto"
LOG_PATH="$HOME/snapshots/canto_log.txt"
DATA_PATH="$HOME/.cantod/data/"
SERVICE_NAME="cantod.service"
```
Create new snapshot  
`./canto_snapshot.sh`  

Check snapshot  
```bash
MY_IP=$(curl -s 2ip.ru); \
curl -s http://${MY_IP}
```

## Automation  
You can add script to the cron  
```cron
# start every day at 00:00
0 0 * * * /bin/bash -c '/root/canto_snapshot.sh'
```
