<h1 align="center">How to Use ExecutionEngine API in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

| API                          | Return Value  | Description                                       |
| ---------------------------- | ---- | ---------------------------------------- |
| GetExecutingScriptHash | bytearray | Get the hash of a smart contract  |
|GetCallingScriptHash | bytearray | Get the hash of the contract|
|GetEntryScriptHash | bytearray | Get the hash of the entry contract |

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. How to use ExecutionEngine

### 2.1 Import
```
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash, GetCallingScriptHash
```

### 2.2 GetExecutingScriptHash 

```
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash, GetCallingScriptHash

def Main(operation, args):
    if operation == "get_contract_hash":
        return get_contract_hash()
    
    return False


def get_contract_hash():
    return GetExecutingScriptHash()
```

### 2.3 GetCallingScriptHash

```
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash, GetCallingScriptHash

def Main(operation, args):
    if operation == "GetCallingScriptHash_test1":
        return GetCallingScriptHash_test1()
    if operation == "GetCallingScriptHash_test2":
        return GetCallingScriptHash_test2()
    
    return False


def GetCallingScriptHash_test1():
    return GetCallingScriptHash()
    
    
def GetCallingScriptHash_test2():
    return GetCallingScriptHash()
```

### 2.4 GetEntryScriptHash

the contract B

```
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash, GetCallingScriptHash, GetEntryScriptHash
from ontology.interop.System.Runtime import CheckWitness, GetTime, Notify, Serialize, Deserialize

ContractAddress = GetExecutingScriptHash()

def Main(operation, args):
    if operation == "invokeB":
        return invokeB(args[0])
    if operation == "avoidToBeInvokedByContract":
        return avoidToBeInvokedByContract()
        
    return False


def invokeB(param):
    Notify(["111_invokeB", param])
    # the result of GetCallingScriptHash and GetEntryScriptHash is same
    # if they are invoked by the same contract
    callerHash = GetCallingScriptHash()
    entryHash = GetEntryScriptHash()
    Notify([callerHash, entryHash, ContractAddress])
    return [callerHash, entryHash, ContractAddress]

def avoidToBeInvokedByContract():
    # the purpose is to prevent hack from other contract
    callerHash = GetCallingScriptHash()
    entryHash = GetEntryScriptHash()
    if callerHash != entryHash:
        Notify(["You are not allowed to invoke this method through contract"])
        Notify([callerHash, entryHash, ContractAddress])
        return False
    else:
        Notify(["You can implement what you need to do here!"])
        Notify([callerHash, entryHash, ContractAddress])
        return True
```

The contract A invokes the contract B.

```
from boa.interop.System.App import RegisterAppCall
from boa.interop.System.ExecutionEngine import GetExecutingScriptHash, GetCallingScriptHash, GetEntryScriptHash
from boa.interop.System.Runtime import CheckWitness, GetTime, Notify, Serialize, Deserialize



ContractB = RegisterAppCall('01aa64971c03abfcaa78d6d2b69ee20b5f55675f', 'operation', 'args')

ContractAddress = GetExecutingScriptHash()

def Main(operation, args):
    if operation == "invokeA":
        opt = args[0]
        params = args[1]
        return invokeA(opt, params)
    if operation == "checkHash":
        return checkHash()
    return False


def invokeA(opt, params):
    callerHash = GetCallingScriptHash()
    entryHash = GetEntryScriptHash()
    Notify(["111_invokeA",callerHash, entryHash, ContractAddress])
    return ContractB(opt, [params])


def checkHash():
    Notify(["111_checkHash"])
    # to prevent hack from other contract
    callerHash = GetCallingScriptHash()
    entryHash = GetEntryScriptHash()
    Notify([callerHash, entryHash, ContractAddress])
    return True
```


## 3. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
