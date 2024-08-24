# XPLA Snapshot

## Install lz4 package

```
sudo apt install lz4
```

## Download the snapshot

```
wget -O xpla_10449078.tar.lz4 https://snapshots.polkachu.com/snapshots/xpla/xpla_10449078.tar.lz4 --inet4-only
```

## Stop Xpla

```
sudo service xpla stop
```

## Back up priv_validator_state.json

```
cp ~/.xpla/data/priv_validator_state.json  ~/.xpla/priv_validator_state.json
```

## Reset node DB

```
xplad tendermint unsafe-reset-all --home $HOME/.xpla --keep-addr-book
```

## Decompress the snapshot to your database location

> [!WARNING] 
> `КОМАНДА ВЫПОЛНЯЕТСЯ ДОЛГО ДОЖДИТЕСЬ ПОЛНОЙ РАСПАКОВКИ`!

```
lz4 -c -d xpla_10449078.lz4  | tar -x -C $HOME/.xpla
```

## Replace with the backed-up priv_validator_state.json

```
cp ~/.xpla/priv_validator_state.json  ~/.xpla/data/priv_validator_state.json
```

## Restart XPLA & Logs

```
sudo service xplad restart && sudo journalctl -u xplad -f --output cat
```

## Sync state

```
curl http://localhost:26657/status | jq -r ".result.sync_info"
```
