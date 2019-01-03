<h1 align="center">How to Upgrade a Smart Contract</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction

| API                          | Return Value  | Description                                       |
| ---------------------------- | ---- | ---------------------------------------- |
| Destroy                 | none |      Destroy a smart contract      |
| Migrate | bool | Upgrade a smart contract. The existing contract will be replaced by the newly migrated contract                  |

For more details, you can view the [API-doc](http://dev-docs.ont.io/#/docs-en/DeveloperGuide/smartcontract/05-sc-api) and the [source code](https://github.com/ontio/ontology-python-compiler) here.

## 2. Destroy

The existing contract will be deleted from the persistent storage area.

### Example

```
from ontology.interop.Ontology.Contract import Migrate
from ontology.interop.System.Contract import Destroy
from ontology.interop.System.Runtime import Notify

def Main(operation, args):
    if operation == "destroy_contract":
        return destroy_contract()

    return False


def destroy_contract():
    Destroy()
    Notify(["The contract has been destoryed"])
    return True
```

## 3. Migrate

The existing contract will be replaced by the newly migrated contract. The data saved by the old contract will also be migrated to the new contract. The old contract will be deleted after migration. 

### Migrate parameters

| Param                         | Description                                       |
| ----------------------------  | ---------------------------------------- |
|script| avm code|
|need_storage| Need persistent storage or not |
|name| Author name|
|version| Contract version|
|author| Contract author |
|email| Developer email |
|description| Contract description|

### Example

```
from ontology.interop.Ontology.Contract import Migrate
from ontology.interop.System.Contract import Destroy
from ontology.interop.System.Runtime import Notify

def Main(operation, args):
    if operation == "migrate_contract":
        if len(args) != 7:
            return False
        avm_code = args[0]
        need_storage = args[1]
        name = args[2]
        version = args[3]
        author = args[4]
        email = args[5]
        description = args[6]
        return migrate_contract(avm_code)

    return False


def migrate_contract(avm_code, need_storage, name, version, author, email, description):
    res = Migrate(avm_code, need_storage, name, version, author, email, description)
    if res:
        Notify(["Migrate successfully"])
        return True
    else:
        return False
```

Follow up question: How to improve this contract? 

Answer: Add CheckWitness(). 
