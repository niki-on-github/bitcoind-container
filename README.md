# Bitcoind Container

Bitcoind Container image that runs the Bitcoin node in a container for easy deployment.

## Setup (Quickstart)

Create Directory `bitcoin` for the persisten data (`mkdir bitcoin`).

Create `bitcoin/bitcoin.conf` (Example):

```
# [core]
prune=20000

# [debug]
logips=1
printtoconsole=1

# [rpc]
# Format <USERNAME>:<SALT>$<HASH>. You can generate this value at https://jlopp.github.io/bitcoin-core-rpc-auth-generator/. 
rpcauth=${SECRET_BITCOIN_RPC_AUTH}
server=1
rpcbind=0.0.0.0
rpcallowip=10.0.0.0/8
rpcallowip=172.16.0.0/12
rpcallowip=192.168.0.0/16
```

Use tools like [bitcoin-core-config-generator](https://jlopp.github.io/bitcoin-core-config-generator/#config=e30=) or read the [manpage](https://manpages.org/bitcoinconf/5).

Use any open source rpc-auth-generator e.g. https://jlopp.github.io/bitcoin-core-rpc-auth-generator/ to generate the repc credentials for the config


Start Container:

```sh
docker run --rm -it -v $PWD/bitcoin:/home/bitcoin/.bitcoin -p 8332:8332 -p 8333:8333 -p 18332:18332 -p 18443:18443 ghcr.io/niki-on-github/bitcoind-container
```

Use [Sparrow Bitcoin Wallet](https://github.com/sparrowwallet/sparrow) to connect to this container. Available in nixpkgs: `nix-shell -p sparrow`.
