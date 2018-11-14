#SmartX Debug Example


![smartx debug](../images/debug.png)

## Debug 设置
- **set break point**

  点击左侧的行数设置断点

- **step over** 

  单行调试，如果被执行行是函数调用，直接运行到下一行

- **step into** 

  逐行调试，如果被调用行是函数调用，会跳入到被调用处继续执行

- **stop** 

  结束本次调试
  
- **opcode debug** 

  Opcode 级别的调试，本功能需要点开**Evaluation Stack** 和 **Alt Stack**来观察


## 虚拟机状态

- **Locals**

  合约中Local variable的状态

- **Storages**

  合约中的key,value状态，都是以hex string 或者hex number 形式存储

- **Evaluation Stack**

  虚拟机的计算栈，即正在栈中被计算的变量
  
- **Alt Stack**

  虚拟机的备用栈，关于计算栈以及备用栈的设计，请参考ontology的虚拟机模块源码

- **History**

  虚拟机所有执行的opcode的历史

## Example Code

```python
from boa.interop.System.Storage import GetContext, Get, Put, Delete

BIG_VALUE = 1000

def Main(operation, args):
  
    if operation == "FibnacciTest":
        n = args[0]
        return FibnacciTest(n)   
           
def FibnacciTest(n):
    if n <= 0:
        return False
        
    f = fibnacci(n)
    if f > BIG_VALUE:
        Put(GetContext(), "fibnacci", "true")
        return True
    else:
        Put(GetContext(), "fibnacci", "false")
        return False
    
def fibnacci(n):
    if n == 0 or n == 1:
        return 1

    return fibnacci(n - 1) + fibnacci(n - 2)
```
## Contact Me
```python

Name: Guanjun Hu 
Github: https://github.com/xris-hu
Wechat: 18502127659
Email: tcpdumpp@163.com
```
