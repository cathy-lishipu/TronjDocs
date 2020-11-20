# RPC API Client

## Creating client

Refer to [Quickstart](Quickstart.md) for creating clients.

## RPC APIs

Tronj wraps RPC APIs defined in Google Protobuf, makes the use of the interfaces  become convinient.

The APIs can be simply divided into two types: *system contract* and *smart contract*.

Tron network has two types of resources: *bandwidth* and *energy*. *System contracts* consume only bandwidth and *Smart contracts* may need both(only trigger calls).

### System Contract. 

System contract is one feature of TRON network.  

A Transaction in TRON is a system contract call, the TronClient(transaction) APIs include two types: *Send a transaction APIs* and *Query APIs*.

#### Send a transaction APIs
The routine for sending refers to [Sending Transaction](https://github.com/Starsakary/TronjDocs/blob/develop/source/mddocs/Sending%20Transaction.md).

- transfer(String from, String to, long amount)

Transfer TRX. amount in SUN

```java
public TransactionReturn transfer(String from, String to, long amount) {

        ByteString rawFrom = parseAddress(from);
        ByteString rawTo = parseAddress(to);

        TransferContract req = TransferContract.newBuilder()
                .setOwnerAddress(rawFrom)
                .setToAddress(rawTo)
                .setAmount(amount)
                .build();

        TransactionExtention txnExt = blockingStub.createTransaction2(req);

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);
        
        return ret;
    }
```
**# transferTrc10(String from, String to, int tokenId, long amount)** 

Transfers TRC10 Asset

**# freezeBalance(String from, long balance, long duration, int resourceCode)**

Freeze balance to get energy or bandwidth, for 3 days.  

Parameters:resourceCode – Resource type, can be "ENERGY" or "BANDWIDTH"

```java
public TransactionReturn freezeBalance(String from, long balance, long duration, int resourceCode) {

        ByteString rawFrom = parseAddress(from);
        FreezeBalanceContract freezeBalanceContract=
                FreezeBalanceContract.newBuilder()
                        .setOwnerAddress(rawFrom)
                        .setFrozenBalance(balance)
                        .setFrozenDuration(duration)
                        .setResourceValue(resourceCode)
                        .build();
        
        TransactionExtention txnExt = blockingStub.freezeBalance2(freezeBalanceContract);

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);
        
        return ret;
    }
```

**# unfreezeBalance(String from, int resource)** 

Unfreeze balance to get TRX back.  

Parameters: resource – Resource type, can be "ENERGY" or "BANDWIDTH"

**# voteWitness(String owner, HashMap<String, String> witness)**. 

Vote for witnesses

```java
public TransactionReturn voteWitness(String owner, HashMap<String, String> witness) {
        ByteString rawFrom = parseAddress(owner);
        VoteWitnessContract voteWitnessContract = createVoteWitnessContract(rawFrom, witness);
        TransactionExtention txnExt = blockingStub.voteWitnessAccount2(voteWitnessContract);

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);
        
        return ret;
    }
```
#### Query APIs
The Tron wraps many query APIs and utility functions. You can query the chain using a instance.
```java
public void getNowBlock() {
        System.out.println("============= getNowBlock =============");
        TronClient client = TronClient.ofNile("3333333333333333333333333333333333333333333333333333333333333333");
        try {
            client.getNowBlock();
        } catch (Exception e) {
            System.out.println("error: " + e);
        }
}
```
**# getBlockByNum(long blockNum)**  

Get block from block number.  

**# getNodeInfo()**

Get current API node’ info.  

**# listNodes()** 

List all nodes that current API node is connected to.  

**# getTransactionInfoByBlockNum(long blockNum)**

Get transactionInfo from block number.  

**# getTransactionInfoById(String txID)** 

Get transactionInfo from transaction id.  

**# getAccount(String address)** 

Get account info by address. 

**# listWitnesses()** 

List all witnesses that current API node is connected to.

### Smart Contract

There are two types of smart contract calls: constant and trigger. Refer to [Smart Contract](Smart Contract.md).

## Javadoc

Refer to [contract](./javadocs/client/org/tron/tronj/client/contract/Contract.html), [Tronclient](./javadocs/client/org/tron/tronj/cilent/TronClient.html).

