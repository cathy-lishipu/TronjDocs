### generateAddress  

Generate random address.

**RETURN**  

Address in hex.

### Transfer

Transfer TRX. amount in SUN. 

**BODY PARAMS**  

*1. fromAddress(String)**  

fromAddress is the owner address.

*2. toAddress(String)**  

toAddress is the recipient address.  

*3. amount(int)**  

amount is the amount of TRX to transfer in SUN.  

**RETURN**  

transfer success or failure.

### TransferTrc10

Transfers TRC10 Asset  

**BODY PARAMS**  

*1. fromAddress(String)**  

fromAddress is the owner address.  

*2. toAddress(String)**  

toAddress is the recipient address.  

*3. tokenId(int)**  

asset name

*4. amount(int)**  

amount is the amount of TRX to transfer in SUN.  

**RETURN**  

transfer success or failure.

### freezeBalance

Freeze balance to get energy or bandwidth, for 3 days.  

**BODY PARAMS**  

*1. ownerAddress(String)**  

owner address, default hexString.  

*2. frozenBalance(long)**  

TRX freeze amount, the unit is sun.

*3. frozenDuration(long)**  

TRX freeze duration, only be specified as 3 days.

*4. resourceCode(int)**  

resource type, can be "ENERGY" or "BANDWIDTH"

```java
public TransactionReturn freezeBalance(String ownerAddress, long frozenBalance, long frozenDuration, int resourceCode) throws IllegalNumException{

        ByteString rawFrom = parseAddress(ownerAddress);
        FreezeBalanceContract freezeBalanceContract=
                FreezeBalanceContract.newBuilder()
                        .setOwnerAddress(rawFrom)
                        .setFrozenBalance(frozenBalance)
                        .setFrozenDuration(frozenDuration)
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

**RETURN**  

freeze balance success or failure.

### unfreezeBalance 

Unfreeze balance to get TRX back.  

**BODY PARAMS**  

*1. ownerAddress(String)**  

owner address, default hexString.  

*2. resourceCode(int)**  

resource type, can be "ENERGY" or "BANDWIDTH"  

**RETURN**  

unfreeze balance success or failure.

### voteWitness 

Vote for witnesses  

**BODY PARAMS**  

*1. ownerAddress(String)**  

owner address, default hexString.  

*2. votes(Map)**  

key: 'vote_address' stands for the address of the witness you want to vote, default hexString.  

value: 'vote_count' stands for the number of votes you want to vote.

```java
public TransactionReturn voteWitness(String ownerAddress, HashMap<String, String> votes) throws IllegalNumException{
        ByteString rawFrom = parseAddress(ownerAddress);
        VoteWitnessContract voteWitnessContract = createVoteWitnessContract(rawFrom, votes);
        TransactionExtention txnExt = blockingStub.voteWitnessAccount2(voteWitnessContract);

        if(SUCCESS != txnExt.getResult().getCode()){
            throw new IllegalNumException(txnExt.getResult().getMessage().toStringUtf8());
        }

        Transaction signedTxn = signTransaction(txnExt);

        TransactionReturn ret = blockingStub.broadcastTransaction(signedTxn);

        return ret;
    }
```  
**RETURN**  

Vote for witnesses success or failure.

### getNowBlock

Query the latest block information. 

**RETURN**  

Block object.

### getBlockByNum  

Returns the Block Object corresponding to the 'Block Height' specified (number of blocks preceding it).  

**BODY PARAMS**  

*1. blockNum(long)**  

blockNum is the block height.  

**RETURN**  

Block object.

### getNodeInfo

Get current API node’ info.  

**RETURN**  

NodeInfo object.

### listNodes

List all nodes that current API node is connected to.  

**RETURN**  

NodeList object.

### getTransactionInfoByBlockNum

Get transactionInfo from block number.  

**BODY PARAMS**  

*1. blockNum(long)**  

blockNum is the block height.  

**RETURN**  

TransactionInfoList object.

### getTransactionInfoById 

Query the transaction fee, block height by transaction id.

**BODY PARAMS**  

*1. txID(String)**  

Transaction hash, i.e. transaction id.  

**RETURN**  

TransactionInfo object.

### getAccount 

Get account info by address.  

**RETURN**  

Account object.

### listWitnesses 

List all witnesses that current API node is connected to.  

**RETURN**  

WitnessList object.
