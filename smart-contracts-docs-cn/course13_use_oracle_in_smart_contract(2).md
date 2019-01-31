<h1 align="center">How to Use Oracle in Smart Contract(2)</h1>
<p align="center" class="version">Version 0.1</p>

## 1. Introduction of Ontology oracle

![framework](https://upload-images.jianshu.io/upload_images/150344-fe85d3ebf8c4604b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![flow.png](https://upload-images.jianshu.io/upload_images/150344-4712326e94c4da2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 2. Application contract

Note: You need to invoke this smart contract in the MainNet or in the TestNet that can be monitored by the third-party oracle nodes.

```python
from ontology.interop.System.App import RegisterAppCall
from ontology.interop.System.ExecutionEngine import GetExecutingScriptHash
from ontology.interop.System.Runtime import Notify, Serialize, Deserialize
from ontology.builtins import *
from ontology.interop.Ontology.Runtime import Base58ToAddress

oracleContract = RegisterAppCall('e0d635c7eb2c5eaa7d2207756a4c03a89790934a', 'operation', 'args')

def main(operation, args):
    if operation == 'sendRequest':
        return sendRequest()
    if operation == 'getResult':
        if len(args) == 1:
            return getResult(args[0])
    return False


def sendRequest():

    req = """{
        "scheduler":{
            "type": "runAfter",
            "params": "2018-06-15 08:37:18"
        },
        "tasks":[
            {
                "type": "httpGet",
                "params": {
                    "url": "https://data.nba.net/prod/v2/20181129/scoreboard.json"
                }
            },
            {
                "type": "jsonParse",
                "params":
                {
                    "data":
                    [
                        {
                            "type": "Array",
                            "path": ["games"],
                            "sub_type":
                            [
                                {
                                    "type": "Struct",
                                    "sub_type":
                                    [
                                        {
                                            "type": "String",
                                            "path": ["gameId"]
                                        },
                                        {
                                            "type": "String",
                                            "path": ["vTeam", "teamId"]
                                        },
                                        {
                                            "type": "String",
                                            "path": ["vTeam", "score"]
                                        },
                                        {
                                            "type": "String",
                                            "path": ["hTeam", "teamId"]
                                        },
                                        {
                                            "type": "String",
                                            "path": ["hTeam", "score"]
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    }"""

    res = oracleContract('CreateOracleRequest',[req,Base58ToAddress('ATS1zQv7U9kUEatSEwSHYgvd9ZQ5Xtgum3')])

    return True

def getResult(txHash):
    res = oracleContract('GetOracleOutcome', [txHash])
    if not res:
        return ''
    a = Deserialize(res)
    b = Deserialize(a[0])
    Notify(a)
    return True
```

The result is as follows.

```text
[
    [
        ["0021800316", "1610612744", "128", "1610612761", "131"],
        ["0021800317", "2610612744", "96", "2610612761", "131"],
        ["0021800318", "3610612744", "128", "3610612761", "131"]
    ]
]
```

## 3. Contributing 

```
Please feel free to give any suggestion and help us make video better!
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
