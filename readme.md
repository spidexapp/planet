# planet
**planet** is a blockchain built using Cosmos SDK and Tendermint and created with [Ignite CLI](https://ignite.com/cli).

### Create two chain and send ibc token between chains

## ENV
```
Mac os
Go -> https://go.dev/
nodejs -> https://nodejs.org/en/
ignite -> https://www.cnblogs.com/farwish/p/14783218.html
protobuf -> https://grpc.io/docs/protoc-installation/
```

## Get started

```
ignite scaffold chain  planet --no-module

ignite scaffold module transfer --ibc

add earth.yml
add mars.yml

ignite chain serve -c earth.yml
ignite chain serve -c mars.yml

ignite relayer configure -a \
  --source-rpc "http://0.0.0.0:26657" \
  --source-faucet "http://0.0.0.0:4500" \
  --source-port "transfer" \
  --source-gasprice "0.0000025earth" \
  --source-prefix "cosmos" \
  --source-gaslimit 300000 \
  --target-rpc "http://0.0.0.0:26659" \
  --target-faucet "http://0.0.0.0:4501" \
  --target-port "transfer" \
  --target-gasprice "0.0000025mars" \
  --target-prefix "cosmos" \
  --target-gaslimit 300000

// start connect
ignite relayer connect

// query account
planetd keys list --home ~/.earth

// query balances
planetd q bank balances [address]

// transfer
planetd tx bank send [from_key_or_address] [to_address] [amount] [flags]

// ibc transfer
planetd tx ibc-transfer transfer [src-port] [src-channel] [receiver] [amount] [flags] --from [account]  --node tcp://127.0.0.1:26657 --home ~/.earth
```
