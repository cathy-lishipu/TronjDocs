# Smart Contract

Smart contract is a key feature of TRON network. It's easy to creating and interacting with smart contracts through Tronj.

## Calling smart contract

There are two types of smart contract calls: *const call* and *trigger call*.

Simply, a *const call* returns result immediately once and no need to sign or broadcast.

*Trigger call* is a type of system contract call, needs signing and broadcasting. It fetches the result through the API.

### Const call

```java
public void getSmartContract() {
        TronClient client = TronClient.ofNile("Your private key");
        try {
          
            Contract cntr = client.getContract("TF17BgPaZYbz8oxbjhriubPDsA7ArKoLX3"); //JST
            System.out.println("Contract name: " + cntr.getName());
            System.out.println("Contract functions: " + cntr.getFunctions().size());
            for (ContractFunction cf : cntr.getFunctions()) {
                System.out.println(cf.toString());
            }
        } catch (Exception e) {
            System.out.println("error: " + e);
        }
    }

//Result
Contract name: JST
Contract functions: 26
# function name() view returns (string )
# function stop() returns (null )
# function approve(guy address, wad uint256 ) returns (bool )
# function setOwner(owner_ address ) returns (null )
# function totalSupply() view returns (uint256 )
# function transferFrom(src address, dst address, wad uint256 ) returns (bool )
# function decimals() view returns (uint256 )
# function mint(guy address, wad uint256 ) returns (null )
# function burn(wad uint256 ) returns (null )
# function balanceOf(src address ) view returns (uint256 )
# function stopped() view returns (bool )
# function setAuthority(authority_ address ) returns (bool result)
# function owner() view returns (address )
# function symbol() view returns (string )
# function burn(guy address, wad uint256 ) returns (null )
# function mint(wad uint256 ) returns (null )
# function transfer(dst address, wad uint256 ) returns (bool )
# function push(dst address, wad uint256 ) returns (null )
# function setSymbol(symbol_ string ) returns (null )
# function move(src address, dst address, wad uint256 ) returns (null )
# function start() returns (null )
# function authority() view returns (address )
# function setName(name_ string ) returns (null )
# function approve(guy address ) returns (bool )
# function allowance(src address, guy address ) view returns (uint256 )
# function pull(src address, wad uint256 ) returns (null )
```

### Trigger call

The first half of the *trigger call* process is similar to the *const call*.

You can easily set `feeLimit`, `memo` and other common attributes via the `TransactionBuilder`.

```java
public void triggerCallDemo() {
        TronClient client = TronClient.ofNile("3333333333333333333333333333333333333333333333333333333333333333");
        try {
            //function 'transfer'
            //params: function name, function params
            Function trc20Transfer = new Function("transfer",
            Arrays.asList(new Address("TVjsyZ7fYF3qLF6BQgPmTEZy1xrNNyVAAA"),
                new Uint256(BigInteger.valueOf(10L).multiply(BigInteger.valueOf(10).pow(18)))),
            Arrays.asList(new TypeReference<Bool>() {}));

            //the params are: owner address, contract address, function
            TransactionBuilder builder = client.triggerCall("TJRabPrwbZy45sbavfcjinPJC18kjpRTv8", "TF17BgPaZYbz8oxbjhriubPDsA7ArKoLX3", trc20Transfer); //JST
            //set extra params
            builder.setFeeLimit(100000000L);
            builder.setMemo("Let's go!");
            //sign transaction
            Transaction signedTxn = client.signTransaction(builder.build());
            System.out.println(signedTxn.toString());
            //broadcast transaction
            TransactionReturn ret = client.broadcastTransaction(signedTxn);
            System.out.println("======== Result ========\n" + ret.toString());
        } catch (Exception e) {
            System.out.println("error: " + e);
        }
    }
```





