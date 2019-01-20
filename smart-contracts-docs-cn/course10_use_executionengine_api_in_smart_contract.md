<h1 align="center">How to Use ExecutionEngine API in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

| API                          | Return Value  | Description                                       |
| ---------------------------- | ---- | ---------------------------------------- |
| GetExecutingScriptHash | bytearray | Get the hash of a smart contract  |
|GetCallingScriptHash | bytearray | Get the hash of the contract|
|GetEntryScriptHash | bytearray | Get the hash of the entry contract |
|RegisterAction| Notify structure| Push notification|

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

## 3. How to use Action

### 3.1 Import
```
from ontology.interop.System.Action import RegisterAction
```

### 3.2 RegisterAction

`RegisterAction` is used for pushing events. 

params format: string + multiple params

```
from ontology.interop.System.Action import RegisterAction

Transfer = RegisterAction('transfer_test', 'a', 'b', 'c')
Refund = RegisterAction('refund_test', 'to', 'amount')


def Main(operation, args):
    if operation == "test1":
        return test1()
    if operation =="test2":
        return test2()
    return False

def test1():
    a = 3
    b = 8
    c = a + b
    Transfer(a, b, c)
    return True

def test2():
    to = 'somebody'
    amount = 52
    Refund(to, amount)
    return True
```

## 4. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
