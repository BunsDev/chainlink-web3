# Web3.py Chainlink library

This is a [web3.py](https://pypi.org/project/web3) library for interacting with Chainlink Ethereum contracts.

## Table of content

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Using this library](#using-this-library)
  - [Installing web3.py](#installing-web3py)
  - [Usage example](#usage-example)
  - [Plugin Methods](#plugin-methods)
    - [Price Feed Addresses](#price-feed-addresses)
    - [`get_price`](#get_price)
- [Found an issue or have a question or suggestion](#found-an-issue-or-have-a-question-or-suggestion)
- [Build & install locally](#build--install-locally)
  - [Build with docker](#build-with-docker)
- [Useful links](#useful-links)


## Prerequisites

- :gear: [Python 3.7.2+](https://www.python.org/)
- :gear: [pip](https://pip.pypa.io/en/stable/)
- :gear: [web3.py 6.0.0+](https://pypi.org/project/web3)

## Installation

```bash
pip3 install chainlink-web3
```

## Using this library

### Installing web3.py

```
pip3 install web3
```

### Usage example

```py
from web3 import Web3, HTTPProvider
from chainlink_web3.utils import ChainlinkUtils

w3 = Web3(HTTPProvider('https://rpc.ankr.com/eth', request_kwargs={'timeout': 180}))

chainlink = ChainlinkUtils(w3=w3)
result = chainlink.get_price('0x72AFAECF99C9d9C8215fF44C77B94B99C28741e8')

print(result)
```

### Plugin Methods

#### Price Feed Addresses

Included in this library are two dicts that contain the Ethereum contract addresses for specific token pairs: [MAINNET_PRICE_FEEDS](##TODO_LINK_HERE##) and [SEPOLIA_PRICE_FEEDS](##TODO_LINK_HERE##). If you cannot find your desired price feed within these dicts, please check [here](https://docs.chain.link/docs/data-feeds/price-feeds/addresses) to make sure it's supported, and if it is, please open an issue or a pull request for the missing price feed so that it can be added to the appropriate dict.

#### `get_price`

```py
def get_price(
    self, 
    price_feed_address: str, 
    aggregator_interface_abi:list = None
    ) -> types.Price:

# class Price:
#     roundId: str
#     answer: str
#     startedAt: str
#     updatedAt: str
#     answeredInRound: str
```

`aggregator_interface_abi` can be found [here](https://github.com/ChainSafe/web3.js-plugin-chainlink/blob/master/src/aggregator_v3_interface_abi.ts).

The `get_price` method, accepts evm address for it's first parameter, and an optional second parameter for specifying the Chainlink Aggregator Interface ABI of the Ethereum smart contract you'd like to interact with (the parameter is defaulted to [aggregator_interface_abi](##TODO_LINK_HERE##)).

Under the hood, this method is calling the `latestRoundData` for the specified price feed, more information about it can be found [here](https://docs.chain.link/data-feeds/price-feeds/api-reference#latestrounddata).

```py
from web3 import Web3, HTTPProvider
from chainlink_web3.utils import ChainlinkUtils, types

w3 = Web3(HTTPProvider('https://rpc.ankr.com/eth', request_kwargs={'timeout': 180}))

chainlink = ChainlinkUtils(w3=w3)
result = chainlink.get_price(types.MAINNET_PRICE_FEEDS['LinkEth'])
# Price(
#     roundId=36893488147419106338, 
#     answer=164576918062797, 
#     startedAt=1697700215, 
#     updatedAt=1697700215, 
#     answeredInRound=36893488147419106338
# )
```

## Found an issue or have a question or suggestion

- :writing_hand: If you found an issue or have a question or suggestion [submit an issue]() or join us on [Discord](https://discord.gg/yjyvFRP)
  ![Discord](https://img.shields.io/discord/593655374469660673.svg?label=Discord&logo=discord)

## Build & install locally

1. Clone repo
2. Install dependencies

```bash
pip3 install wheel
pip3 install setuptools
pip3 install twine
```

3. Run the tests
```bash
python3 setup.py pytest
```

4. Generate .whl file for external use
```bash
python3 setup.py bdist_wheel
```

This creates a `./dist` folder that contains a `.whl` file.

Use the bellow command to install the lib on your local environment:

```bash
pip3 install /path/to/wheelfile.whl
```
### Build with docker

1. Clone repo

2. Create docker image
```bash
chmod +x ./run-docker.sh
./run-docker.sh install
```

3. Test lib
```bash
./run-docker.sh test
```

4. Generate .whl file for external use
```bash
./run-docker.sh build
```

This creates a `./dist` folder that contains a `.whl` file.

Use the bellow command to install the lib on your local environment:

```bash
pip3 install /path/to/wheelfile.whl
```

## Useful links

- [web3.py Documentation](https://web3py.readthedocs.io/en/latest/index.html)
- [Chainlink Documentation](https://docs.chain.link/docs)
