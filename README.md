# XPLA Snapshot

## Install lz4 package

```
sudo apt install lz4
```

## Download the snapshot

```
wget -O xpla_10449078.tar.lz4 https://www.dropbox.com/scl/fi/3ynu2gzynd2flf2zh1vc0/xpla_10450690.lz4
```

## Stop Xpla

```
sudo service xpla stop
```

## Back up priv_validator_state.json

> [!WARNING] 
> `СОХРАНИТЕ БЭКАП priv_validator_state.json ПЕРЕД ИСПОЛЬЗОВАНИЕМ СНАПШОТА!`

```
cp ~/.xpla/data/priv_validator_state.json  ~/.xpla/priv_validator_state.json
```

## Reset node DB

```
xpla tendermint unsafe-reset-all --home $HOME/.xpla --keep-addr-book
```

## Decompress the snapshot to your database location

> [!WARNING] 
> `КОМАНДА ВЫПОЛНЯЕТСЯ ДОЛГО ДОЖДИТЕСЬ ПОЛНОЙ РАСПАКОВКИ`!

```
lz4 -c -d xpla_10450690.lz4  | tar -x -C $HOME/.xpla
```

## Replace with the backed-up priv_validator_state.json

> [!WARNING] 
> `ВОССТАНОВИТЕ СВОЙ priv_validator_state.json ИЗ БЭКАП ПОСЛЕ ИСПОЛЬЗОВАНИЯ СНАПШОТА!`

```
cp ~/.xpla/priv_validator_state.json  ~/.xpla/data/priv_validator_state.json
```

## Restart XPLA & Logs

```
sudo service xpla restart && sudo journalctl -u xpla -f --output cat
```

## Sync state

```
curl http://localhost:26657/status | jq -r ".result.sync_info"
```
