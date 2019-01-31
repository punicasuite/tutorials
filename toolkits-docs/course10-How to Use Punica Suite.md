<h1 align="center">How to Use Punica Suite</h1>
<p align="center" class="version">Version 0.1</p>

## 1. What is Punica suite  

[Punica Suite](https://punica.ont.io) is Ontology's dApp development framework and has (almost) everything you need to start developing your Ontology based dApp.

Punica provides developers with a complete set of open-source development tools for dApp development, will allow developers to develop their projects quickly and easily for use on the Ontology blockchain.  Please see below for a list of open-source tools and resources to help get you started.

* [Punica Python CLI](https://github.com/punicasuite/punica-python) or [Punica TypeScript CLI](https://github.com/punicasuite/punica-ts) - used to download, compile, deploy and invoke smart contracts
* [Punica boxes](http://punica.ont.io/boxes/) - pre-configured smart contract templates
* [Solo-chain](https://github.com/punicasuite/solo-chain/releases) - a prebuilt private-net for development 
* [VScode Extension](https://github.com/punicasuite/vscode-ext-ontology) - VScode Extension for Ontology

Advantages：
* Punica is the first dApp development framework for the ontology, which greatly saves development time and allows users to do more with less;
* Provide a large number of teaching materials and teaching videos, so that beginners can quickly get started and fully understand;
* Developed a smart contract testing framework that supports unit testing and functional testing, making it easier and more convenient than SDK testing;
* Smart contract compilation and deployment testing as one, saving development time. The debug function has been integrated in SmartX, and the command line debug function will be supported later.
* Solo-chain allows users to view data on the chain in real time, which is more efficient than test network or building a private network.
* A variety of SDK and dAPI cases are available for a variety of developers.

Learning resource:
* [Punica Website](http://punica.ont.io) - Punica official website that includes suites, tutorials, boxes, and smart contracts. 
* [Tutorials](http://punica.ont.io/tutorials/) - A growing list of tutorials to help you on your Ontology dApp journey
* [Github](https://github.com/punicasuite) - Visit the Punica Suite Github page

## 2. How to install Punica suite

### 2.1 Punica CLI

Punica-Cli is a command line interface designed to allow devlopers to compile, deploy and invoke smart contracts without the need for a full SDK. Punica-Cli is currently available in two languages: [Punica Python CLI](https://github.com/punicasuite/punica-python) or [Punica TypeScript CLI](https://github.com/punicasuite/punica-ts).

#### Features:
* Supports intelligent smart contract compilation, deployment, invocation and testing;
* Supports both Python and TypeScript programming languages;
* Download dApp templates via Punica-Box;
* Smart contract packaging management tools;
* Supports wallet file management.

#### Installation

```shell
pip install punica
```
```
npm install punica-ts -g
```

or 

```shell
python setup.py install
```
**Note: If you are using Python, please ensure you have [Python v3.7](https://www.python.org/downloads/release/python-370/) or above installed.**

#### Available Commands

```shell
punica
Usage: punica [OPTIONS] COMMAND [ARGS]...

Options:
-p, --project PATH  Specify a punica project directory.
-v, --version       Show the version and exit.
-h, --help          Show this message and exit.

Commands:
compile  Compile the specified contracts to avm and...
deploy   Deploys the specified contracts to specified...
init     Initialize new and empty Ontology DApp...
invoke   Invoke the function list in default-config or...
node     Ontology Blockchain private net in test mode.
scpm     Smart contract package manager，support...
smartx   Ontology smart contract IDE,SmartX...
test     Unit test with specified smart contract
unbox    Download a Punica Box, a pre-built Ontology...
wallet   Manager your ontid, account, asset.
```

### 2.2 How to install solo-chain, VSCode extension

For how to install solo-chain and VSCode extension, please refer to [How to Use Solo-chain](https://github.com/punicasuite/tutorials/blob/master/toolkits-docs/course02-How%20to%20Use%20Solo-chain.md) and [How to Use VSCode Extension](https://github.com/punicasuite/tutorials/blob/master/toolkits-docs/course07-How%20to%20Use%20VScode%20Extension.md).

## 3. Get started

### 3.1 Initializing a New Project

You can create an empty Punica project with no smart contracts using the `init` command.

```shell
punica init
```

Once this operation has completed, you will have a project structure with the following items:

- `contracts/`: Directory for Ontology smart contracts.
- `src/`: Directory for DApp source file(s).
- `test/`: Directory for test files to test your application and contracts.
- `wallet/`: Directory for saved Ontology wallet file.

For more usage information, you can use `punica init --help`
```shell
punica init --help
Usage: punica init [OPTIONS]

Initialize new and empty Ontology DApp project.

Options:
-h, --help  Show this message and exit.
```

**Note**: If you are not running punica-cli in the root directory of your project, you need to use the `-p` or `--project` option to specify your DApp project path.

### 3.2 Compile, deploy, invoke

Compile a smart contract
```
punica compile
```

Deploy a smart contract
```
punica deploy
```

Display the list of functions that can be invoked and then invoke a function
```
punica invoke list

punica invoke --functions testHello
```

## Author
```
Please feel free to give any suggestion
Contact: Yue Zhao 
Wechat: 16621171248
Email: messixaviinsta0303@163.com
```
