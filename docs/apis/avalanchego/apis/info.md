---
sidebar_position: 11
---

# Info API

This API can be used to access basic information about the node.

:::info
This API set is for a specific node, it is unavailable on the [public server](../public-api-server.md).
:::

## Format

This API uses the `json 2.0` RPC format. For more information on making JSON RPC calls, see
[here](issuing-api-calls.md).

## Endpoint

```text
/ext/info
```

## Methods

### `info.getBlockchainID`

Given a blockchain’s alias, get its ID. (See [`admin.aliasChain`](admin.md#adminaliaschain).)

**Signature:**

```sh
info.getBlockchainID({alias:string}) -> {blockchainID:string}
```

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getBlockchainID",
    "params": {
        "alias":"X"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "blockchainID": "sV6o671RtkGBcno1FiaDbVcFv2sG5aVXMZYzKdP4VQAWmJQnM"
  }
}
```

### `info.getNetworkID`

Get the ID of the network this node is participating in.

**Signature:**

```sh
info.getNetworkID() -> {networkID:int}
```

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNetworkID"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "networkID": "2"
  }
}
```

### `info.getNetworkName`

Get the name of the network this node is participating in.

**Signature:**

```sh
info.getNetworkName() -> {networkName:string}
```

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNetworkName"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "networkName": "local"
  }
}
```

### `info.getNodeID`

Get the ID of this node.

**Signature:**

```sh
info.getNodeID() -> {
    nodeID: string,
    nodePOP: {
        publicKey: string,
        proofOfPossession: string
    }
}
```

- `nodeID` is this node's ID
- `nodePOP` is this node's BLS key and proof of possession

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNodeID"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "result": {
    "nodeID": "NodeID-5mb46qkSBj81k9g9e4VFjGGSbaaSLFRzD",
    "nodePOP": {
      "publicKey": "0x8f95423f7142d00a48e1014a3de8d28907d420dc33b3052a6dee03a3f2941a393c2351e354704ca66a3fc29870282e15",
      "proofOfPossession": "0x86a3ab4c45cfe31cae34c1d06f212434ac71b1be6cfe046c80c162e057614a94a5bc9f1ded1a7029deb0ba4ca7c9b71411e293438691be79c2dbf19d1ca7c3eadb9c756246fc5de5b7b89511c7d7302ae051d9e03d7991138299b5ed6a570a98"
    }
  },
  "id": 1
}
```

### `info.getNodeIP`

Get the IP of this node.

**Signature:**

```text
info.getNodeIP() -> {ip: string}
```

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNodeIP"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "result": {
    "ip": "192.168.1.1:9651"
  },
  "id": 1
}
```

### `info.getNodeVersion`

Get the version of this node.

**Signature:**

```sh
info.getNodeVersion() -> {
    version: string,
    databaseVersion: string,
    gitCommit: string,
    vmVersions: map[string]string,
    rpcProtocolVersion: string,
}
```

where:

- `version` is this node's version
- `databaseVersion` is the version of the database this node is using
- `gitCommit` is the Git commit that this node was built from
- `vmVersions` is map where each key/value pair is the name of a VM, and the version of that VM this
  node runs
- `rpcProtocolVersion` is the RPCChainVM protocol version

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getNodeVersion"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "result": {
    "version": "avalanche/1.9.1",
    "databaseVersion": "v1.4.5",
    "rpcProtocolVersion": "18",
    "gitCommit": "79cd09ba728e1cecef40acd60702f0a2d41ea404",
    "vmVersions": {
      "avm": "v1.9.1",
      "evm": "v0.11.1",
      "platform": "v1.9.1"
    }
  },
  "id": 1
}
```

### `info.getVMs`

Get the virtual machines installed on this node.

**Signature:**

```sh
info.getVMs() -> {
    vms: map[string][]string
}
```

**Example Call:**

```bash
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getVMs",
    "params" :{}
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "result": {
    "vms": {
      "jvYyfQTxGMJLuGWa55kdP2p2zSUYsQ5Raupu4TW34ZAUBAbtq": ["avm"],
      "mgj786NP7uDwBCcq6YwThhaN8FLyybkCa4zBWTQbNgmK6k9A6": ["evm"],
      "qd2U4HDWUvMrVUeTcCHp6xH3Qpnn1XbU5MDdnBoiifFqvgXwT": ["nftfx"],
      "rWhpuQPF1kb72esV2momhMuTYGkEb1oL29pt2EBXWmSy4kxnT": ["platform"],
      "rXJsCSEYXg2TehWxCEEGj6JU2PWKTkd6cBdNLjoe2SpsKD9cy": ["propertyfx"],
      "spdxUxVJQbX85MGxMHbKw1sHxMnSqJ3QBzDyDYEP3h6TLuxqQ": ["secp256k1fx"]
    }
  },
  "id": 1
}
```

### `info.isBootstrapped`

Check whether a given chain is done bootstrapping

**Signature:**

```sh
info.isBootstrapped({chain: string}) -> {isBootstrapped: bool}
```

`chain` is the ID or alias of a chain.

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.isBootstrapped",
    "params": {
        "chain":"X"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "result": {
    "isBootstrapped": true
  },
  "id": 1
}
```

### `info.peers`

Get a description of peer connections.

**Signature:**

```sh
info.peers({
    nodeIDs: string[] // optional
}) ->
{
    numPeers: int,
    peers:[]{
        ip: string,
        publicIP: string,
        nodeID: string,
        version: string,
        lastSent: string,
        lastReceived: string,
        benched: string[],
        observedUptime: int,
        observedSubnetUptime: map[string]int,
    }
}
```

- `nodeIDs` is an optional parameter to specify what NodeID's descriptions should be returned. If
  this parameter is left empty, descriptions for all active connections will be returned. If the
  node is not connected to a specified nodeID, it will be omitted from the response.
- `ip` is the remote IP of the peer.
- `publicIP` is the public IP of the peer.
- `nodeID` is the prefixed Node ID of the peer.
- `version` shows which version the peer runs on.
- `lastSent` is the timestamp of last message sent to the peer.
- `lastReceived` is the timestamp of last message received from the peer.
- `benched` shows chain IDs that the peer is being benched.
- `observedUptime` is this node's primary network uptime, observed by the peer.
- `observedSubnetUptime` is a map of Subnet IDs to this node's Subnet uptimes, observed by the peer.

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.peers",
    "params": {
        "nodeIDs": []
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "numPeers": 3,
    "peers": [
      {
        "ip": "206.189.137.87:9651",
        "publicIP": "206.189.137.87:9651",
        "nodeID": "NodeID-8PYXX47kqLDe2wD4oPbvRRchcnSzMA4J4",
        "version": "avalanche/1.9.4",
        "lastSent": "2020-06-01T15:23:02Z",
        "lastReceived": "2020-06-01T15:22:57Z",
        "benched": [],
        "observedUptime": "99",
        "observedSubnetUptimes": {},
        "trackedSubnets": [],
        "benched": []
      },
      {
        "ip": "158.255.67.151:9651",
        "publicIP": "158.255.67.151:9651",
        "nodeID": "NodeID-C14fr1n8EYNKyDfYixJ3rxSAVqTY3a8BP",
        "version": "avalanche/1.9.4",
        "lastSent": "2020-06-01T15:23:02Z",
        "lastReceived": "2020-06-01T15:22:34Z",
        "benched": [],
        "observedUptime": "75",
        "observedSubnetUptimes": {
          "29uVeLPJB1eQJkzRemU8g8wZDw5uJRqpab5U2mX9euieVwiEbL": "100"
        },
        "trackedSubnets": [
          "29uVeLPJB1eQJkzRemU8g8wZDw5uJRqpab5U2mX9euieVwiEbL"
        ],
        "benched": []
      },
      {
        "ip": "83.42.13.44:9651",
        "publicIP": "83.42.13.44:9651",
        "nodeID": "NodeID-LPbcSMGJ4yocxYxvS2kBJ6umWeeFbctYZ",
        "version": "avalanche/1.9.3",
        "lastSent": "2020-06-01T15:23:02Z",
        "lastReceived": "2020-06-01T15:22:55Z",
        "benched": [],
        "observedUptime": "95",
        "observedSubnetUptimes": {},
        "trackedSubnets": [],
        "benched": []
      }
    ]
  }
}
```

### `info.getTxFee`

Get the fees of the network.

**Signature:**

```sh
info.getTxFee() ->
{
    txFee: uint64,
    createAssetTxFee: uint64,
    createSubnetTxFee: uint64,
    transformSubnetTxFee: uint64,
    createBlockchainTxFee: uint64,
    addPrimaryNetworkValidatorFee: uint64,
    addPrimaryNetworkDelegatorFee: uint64,
    addSubnetValidatorFee: uint64,
    addSubnetDelegatorFee: uint64
}
```

- `txFee` is the default fee for making transactions.
- `createAssetTxFee` is the fee for creating a new asset.
- `createSubnetTxFee` is the fee for creating a new Subnet.
- `transformSubnetTxFee` is the fee for converting a PoA Subnet into a PoS Subnet.
- `createBlockchainTxFee` is the fee for creating a new blockchain.
- `addPrimaryNetworkValidatorFee` is the fee for adding a new primary network validator.
- `addPrimaryNetworkDelegatorFee` is the fee for adding a new primary network delegator.
- `addSubnetValidatorFee` is the fee for adding a new Subnet validator.
- `addSubnetDelegatorFee` is the fee for adding a new Subnet delegator.

All fees are denominated in nAVAX.

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.getTxFee"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "txFee": "1000000",
    "createAssetTxFee": "10000000",
    "createSubnetTxFee": "1000000000",
    "transformSubnetTxFee": "10000000000",
    "createBlockchainTxFee": "1000000000",
    "addPrimaryNetworkValidatorFee": "0",
    "addPrimaryNetworkDelegatorFee": "0",
    "addSubnetValidatorFee": "1000000",
    "addSubnetDelegatorFee": "1000000"
  }
}
```

### `info.uptime`

Returns the network's observed uptime of this node.

**Signature:**

```sh
info.uptime({
    subnetID: string // optional
}) ->
{
    rewardingStakePercentage: float64,
    weightedAveragePercentage: float64
}
```

- `subnetID` is the Subnet to get the uptime of. If not provided, returns the uptime of the node on
  the primary network.

- `rewardingStakePercentage` is the percent of stake which thinks this node is above the uptime
  requirement.
- `weightedAveragePercentage` is the stake-weighted average of all observed uptimes for this node.

**Example Call:**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.uptime"
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

**Example Response:**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "rewardingStakePercentage": "100.0000",
    "weightedAveragePercentage": "99.0000"
  }
}
```

#### **Example Subnet Call**

```sh
curl -X POST --data '{
    "jsonrpc":"2.0",
    "id"     :1,
    "method" :"info.uptime",
    "params" :{
        "subnetID":"29uVeLPJB1eQJkzRemU8g8wZDw5uJRqpab5U2mX9euieVwiEbL"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/ext/info
```

#### **Example Subnet Response**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "rewardingStakePercentage": "74.0741",
    "weightedAveragePercentage": "72.4074"
  }
}
```
