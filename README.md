# opbnb-snapshot

## Endpoint

Snapshots are created and preserved every week,
and each snapshot is kept for 30 days.
NodeReal, a community developer, is responsible for regularly creating and updating the snapshots.

At present, we offer snapshots for both the mainnet and testnet networks in path-based state scheme and archived formats.
It is advisable to utilize the path-based state scheme snapshot for quicker synchronization, improved performance, and reduced storage needs.

For more details about different node type and database scheme, please refer to the [official documentation](https://docs.bnbchain.org/opbnb-docs/docs/tutorials/run-nodes-best-practices/).

### *Mainnet*
- Path-Base-State-Scheme(recommand):
    - url: https://opbnb-snapshot-mainnet.bnbchain.org/geth-pbss-20240614.tar.gz 
    - sha256 checksum: 5fbbaf7a9ca5542230ce742bf76acb8b9be071d1df20b5b39c0974986adaab43
- Archived:  
    - The full archived node status is too large(over 5.6 TB at the end of May, 2024). There is no available archive snapshot at the moment.
    If you do need a full archived node, you have to sync the node from scratch.
- Pruned Archived: (Note that the pruned snapshot has erased state data before block height: 19598373)
    - url:  https://opbnb-snapshot-mainnet.bnbchain.org/geth-prune-20240614.tar.gz
    - sha256 checksum: 19a9c9c61bebfbcf11958514b7c987237a02d89d1c4300fc9308a0c77c547ae9

### *Testnet*
- Path-Base-State-Scheme(recommand):  
    - url: https://opbnb-snapshot-testnet.bnbchain.org/geth-pbss-20240612.tar.gz
    - sha256 checksum: 12a91fc1eab8d21e3146ce0d63f4134634576ebb7ff6e4570dac379eec5678b3
- Archived:
    - There is no available archive snapshot at the moment.

Additionally, you can get the latest snapshot url and sha256 checksum as below:

```
$ curl https://opbnb-snapshot-mainnet.bnbchain.org/geth-pbss-latest
geth-pbss-20240525.tar.gz

$ curl https://opbnb-snapshot-mainnet.bnbchain.org/geth-pbss-20240525.tar.gz.sha256
d361af99362f3e6c55984e4aff127fffe9939e5c28274450f4b168b04d87370a  geth-pbss-20240525.tar.gz
```

## Usage

### Step 1: Download the snapshot and decompress it.

```bash
wget -q -O - https://opbnb-snapshot-mainnet.bnbchain.org/geth-pbss-20240525.tar.gz | tar -xvf -
```

### Step 2: Replace the data.

1. Stop the running `op-geth` client, ensuring that it has completely shut down.
2. To back up the original data, execute the following commands:
    ```
    mv ${OPGeth_DataDir}/geth/chaindata ${OPGeth_DataDir}/geth/chaindata_backup
    mv ${OPGeth_DataDir}/geth/triecache ${OPGeth_DataDir}/geth/triecache_backup
    ```
3. Replace the data with the snapshot by running:
    ```
    mv ./geth/chaindata ${OPGeth_DataDir}/geth/chaindata
    mv ./geth/triecache ${OPGeth_DataDir}/geth/triecache
    ```
4. Restart the `op-geth` client and verify the logs.
