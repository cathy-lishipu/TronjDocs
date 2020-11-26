### Transfer

Transfer TRX. amount in SUN. 

### TransferTrc10

Transfers TRC10 Asset

### freezeBalance

Freeze balance to get energy or bandwidth, for 3 days.  

Parameters:resourceCode – Resource type, can be "ENERGY" or "BANDWIDTH"

```java
public TransactionReturn freezeBalance(String from, long balance, long duration, int resourceCode) throws IllegalNumException{

        ByteString rawFrom = parseAddress(from);
        FreezeBalanceContract freezeBalanceContract=
                FreezeBalanceContract.newBuilder()
                        .setOwnerAddress(rawFrom)
                        .setFrozenBalance(balance)
                        .setFrozenDuration(duration)
                        .setResourceValue(resourceCode)
                        .build();
        TransactionExtention txnExt = blockingStub.freezeBalance2(freezeBalanceContract);

        if(SUCCESS != txnExt.getResult().getCode()){
            throw new IllegalNumException(txnExt.getResult().getMessage().toStringUtf8());
        }

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);
        return ret;
    }
```

### unfreezeBalance 

Unfreeze balance to get TRX back.  

Parameters: resource – Resource type, can be "ENERGY" or "BANDWIDTH"

### voteWitness 

Vote for witnesses

```java
public TransactionReturn voteWitness(String owner, HashMap<String, String> witness) throws IllegalNumException{
        ByteString rawFrom = parseAddress(owner);
        VoteWitnessContract voteWitnessContract = createVoteWitnessContract(rawFrom, witness);
        TransactionExtention txnExt = blockingStub.voteWitnessAccount2(voteWitnessContract);

        if(SUCCESS != txnExt.getResult().getCode()){
            throw new IllegalNumException(txnExt.getResult().getMessage().toStringUtf8());
        }

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);

        return ret;
    }
```
###getNowBlock

Query the latest block information. 

### getBlockByNum  

Get block from block number.  

### getNodeInfo

Get current API node’ info.  

### listNodes

List all nodes that current API node is connected to.  

### getTransactionInfoByBlockNum

Get transactionInfo from block number.  

### getTransactionInfoById 

Get transactionInfo from transaction id.  

### getAccount(String address) 

Get account info by address. 

### listWitnesses() 

List all witnesses that current API node is connected to.
