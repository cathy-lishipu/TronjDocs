# RPC API Client

## Creating client

Refer to [Quickstart](Quickstart.md) for creating clients.

## RPC APIs

Tronj wraps RPC APIs defined in Google Protobuf, makes the use of the interfaces  become convinient.

The APIs can be simply divided into two types: *system contract* and *smart contract*.

Tron network has two types of resources: *bandwidth* and *energy*. *System contracts* consume only bandwidth and *Smart contracts* may need both(only trigger calls).

### System Contract

```java
public void freezeBalance() {
        System.out.println("============= freeze balance =============");
        TronClient client = TronClient.ofShasta("3333333333333333333333333333333333333333333333333333333333333333");
        try {
            client.freezeBalance("TJRabPrwbZy45sbavfcjinPJC18kjpRTv8", 1_000_000L, 3L,1, "TVjsyZ7fYF3qLF6BQgPmTEZy1xrNNyVAAA");
        } catch (Exception e) {
            System.out.println("error: " + e);
        }
    }
```

### Smart Contract

There are two types of smart contract calls: constant and trigger. Refer to [Smart Contract](Smart Contract.md).

## Javadoc

Refer to [contract](./javadocs/client/org/tron/tronj/client/contract/Contract.html), [Tronclient](./javadocs/client/org/tron/tronj/cilent/TronClient.html).

