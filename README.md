# canto-snapshots  

## Clone github repo 
```bash
git clone https://github.com/SiddarthVijay/cosmos-snapshots.git
cd cosmos-snapshots
git checkout patch/v1-canto
```

## Create folder for snapshots  
```bash
mkdir -p $HOME/snapshots/canto
```

## Create new snapshot  
```bash
./canto_snapshot.sh
```

## Automation  
You can add script to the cron  
```cron
# start every day at 00:00
0 0 * * * /bin/bash -c '/root/canto_snapshot.sh'
```
