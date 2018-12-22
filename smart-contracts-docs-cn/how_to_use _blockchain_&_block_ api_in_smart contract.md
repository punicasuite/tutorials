<h1 align="center">How to Use Blockchain & Block API in Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction 

There are five major APIs in Ontology smart contract and blockchain API is one of them. Blockchain API supports basic blockchain query and operation such as getting current block height. Block API supports query about transaction. More API will be available in the future. 

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. How to use Blockchain API

### 2.1 Import

```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash
```

### 2.2 Blockchain API

#### GetHeight

```
from boa.interop.System.Runtime import Notify
from boa.interop.System.Blockchain import GetHeight

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    height=GetHeight()
    Notify(height)
    return height
```

#### GetHeader

```
from boa.interop.System.Runtime import Notify
from boa.interop.System.Blockchain import GetHeader

def Main(operation, args):
    if operation == 'demo':
        block_height=args[0]
        return demo(block_height)
    return False


def demo(block_height):
    header=GetHeader(block_height)
    Notify(header)
    return header
```



#### GetTransactionByHash

```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    # tx_hash="9f270aa3a4c13c46891ff0e1a2bdb3ea0525669d414994aadf2606734d0c89c1"
    tx_hash=bytearray(b"\xc1\x89\x0c\x4d\x73\x06\x26\xdf\xaa\x94\x49\x41\x9d\x66\x25\x05\xea\xb3\xbd\xa2\xe1\xf0\x1f\x89\x46\x3c\xc1\xa4\xa3\x0a\x27\x9f")
    tx=GetTransactionByHash(tx_hash)
```

#### GetTransactionHeight

```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    # tx_hash="9f270aa3a4c13c46891ff0e1a2bdb3ea0525669d414994aadf2606734d0c89c1"
    tx_hash=bytearray(b"\xc1\x89\x0c\x4d\x73\x06\x26\xdf\xaa\x94\x49\x41\x9d\x66\x25\x05\xea\xb3\xbd\xa2\xe1\xf0\x1f\x89\x46\x3c\xc1\xa4\xa3\x0a\x27\x9f")
    height=GetTransactionHeight(tx_hash)
```

#### GetContract

```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    # contract_hash="d81a75a5ff9b95effa91239ff0bb3232219698fa"
    contract_hash=bytearray(b"\xfa\x98\x96\x21\x32\x32\xbb\xf0\x9f\x23\x91\xfa\xef\x95\x9b\xff\xa5\x75\x1a\xd8")
    contract=GetContract(contract_hash)
    return contract
```

#### GetBlock

There are two ways to get block.

1. Get block by height

```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    block=GetBlock(1408)
    return block
```

2. Get block by block hash

You need to reverse block hash of hex string first and then transfer it to byte array. For example, if block hash of hex string is `e40315e22fc30b4648e3546d33927317f7175dc4c866ea443077798240c5e016`, reversing it to `16e0c5408279773044ea66c8c45d17f7177392336d54e348460bc32fe21503e4
` and then transferring it to `\x16\xe0\xc5\x40\x82\x79\x77\x30\x44\xea\x66\xc8\xc4\x5d\x17\xf7\x17\x73\x92\x33\x6d\x54\xe3\x48\x46\x0b\xc3\x2f\xe2\x15\x03\xe4`. It is an important procedure. Otherwise, you would get an error which indicates that there is no block of this block hash.


```
from boa.interop.System.Blockchain import GetHeight, GetHeader, GetBlock, GetTransactionHeight, GetContract, GetTransactionByHash

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    block_hash=bytearray(b'\x16\xe0\xc5\x40\x82\x79\x77\x30\x44\xea\x66\xc8\xc4\x5d\x17\xf7\x17\x73\x92\x33\x6d\x54\xe3\x48\x46\x0b\xc3\x2f\xe2\x15\x03\xe4')
    block=GetBlock(block_hash)
```

## 3. How to use Block API

### 3.1 Import

```
from boa.interop.System.Block import GetTransactions, GetTransactionCount, GetTransactionByIndex
```

### 3.2 Block API

#### GetTransactionCount

```
from boa.interop.System.Blockchain import GetBlock
from boa.interop.System.Block import GetTransactionCount

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    block=GetBlock(1408)
    count=GetTransactionCount(block)
    return count
```

#### GetTransactions

```
from boa.interop.System.Blockchain import GetBlock
from boa.interop.System.Block import GetTransactionCount

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    block=GetBlock(1408)
    txs=GetTransactions(block)
    return txs
```

#### GetTransactionByIndex

```
from boa.interop.System.Blockchain import GetBlock
from boa.interop.System.Block import GetTransactionByIndex

def Main(operation):
    if operation == 'demo':
        return demo()
    return False


def demo():
    block=GetBlock(1408)
    tx=GetTransactionByIndex(block,0) # index starts from 0.
    return tx
```

## 4. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
