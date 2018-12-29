<h1 align="center">How to Use Runtime API in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

| API                          | Return Value  | Description                                       |
| ---------------------------- | ---- | ---------------------------------------- |
| Runtime.GetTime                 | uint | Return timestamp of the most recent block           |
| Runtime.CheckWitness(hash_or_pubkey : byte[]) | bool | Verify operational permissions of user or contract                   |
| Runtime.Notify(object[])     | void | In smart contract, sending notifications (including socket notifications or rpc queries) to clients that are executing this smart contract |
| Runtime.Log(string)          | void | In smart contract, sending logs ( including socket notifications) to clients that are executing this smart contract       |
| Serialize(item) |byte array |Serializes an item into a bytearray|
| Deserialize(item)|original type | Deserializes an item from a bytearray|
| GetCurrentBlockHash|string | Return block hash of the most recent block |
| Base58ToAddress(base58_address)|byte array|transfer a base58 address to address in form of byte array|
| AddressToBase58(address)|string |transfer an address in form of byte array to a base58 address |

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. How to use Runtime API

`Import package`
```
from ontology.interop.System.Runtime import GetTime, CheckWitness, Log, Notify, Serialize, Deserialize
from ontology.interop.Ontology.Runtime import Base58ToAddress, AddressToBase58, GetCurrentBlockHash
```

`Log`: In smart contract, sending logs ( including socket notifications) to clients that are executing this smart contract

```
from ontology.interop.System.Runtime import GetTime, CheckWitness, Log, Notify, Serialize, Deserialize

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    Log("hello world")
```

`Notify`: In smart contract, sending notifications (including socket notifications or rpc queries) to clients that are executing this smart contract

```
from ontology.interop.System.Runtime import GetTime, CheckWitness, Log, Notify, Serialize, Deserialize

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    Notify("hello world")
```

`GetTime`: Return timestamp of the most recent block

```
from ontology.interop.System.Runtime import GetTime

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    time=GetTime()
    return time # return a uint num
```

`GetCurrentBlockHash`: Return block hash of the most recent block

```
from ontology.interop.Ontology.Runtime import GetCurrentBlockHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False
    
def demo():
    block_hash = GetCurrentBlockHash()
    return block_hash
```

`Serialize`: Serialize the data from original type to byte array

`Deserialize`: Deserialize the data from byte array to original type

```
from ontology.interop.System.Runtime import GetTime, CheckWitness, Log, Notify, Serialize, Deserialize
from ontology.interop.System.Storage import Put, Get, GetContext

def Main(operation, args):
    if operation == 'serialize_to_bytearray':
        data = args[0]
        return serialize_to_bytearray(data)
    if operation == 'deserialize_from_bytearray':
        key = args[0]
        return deserialize_from_bytearray(key)
    return False


def serialize_to_bytearray(data):
    sc = GetContext()
    key = "1"
    byte_data = Serialize(data)
    Put(sc, key, byte_data)


def deserialize_from_bytearray(key):
    sc = GetContext()
    byte_data = Get(sc, key)
    data = Deserialize(byte_data)
    return data

`Base58ToAddress`: transfer a base58 address to address in form of byte array

`AddressToBase58`: transfer an address in form of byte array to a base58 address

```
from ontology.interop.System.Runtime import Log
from ontology.interop.Ontology.Runtime import Base58ToAddress, AddressToBase58

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    base58_addr="AV1GLfVzw28vtK3d1kVGxv5xuWU59P6Sgn"
    addr=Base58ToAddress(base58_addr)
    Log(addr)
    base58_addr=AddressToBase58(addr)
    Log(base58_addr)
```


