## Crypto Trading Bot using VWAP

### Prerequisites

    Node.js (v14 or later)
    npm (v6 or later)
    A Uniswap account
    Ethereum Wallet

### Installation

1. Install the required dependencies:

        npm install

2. Create a config.js file in the root directory with the following content:

        export const data = {
            WETH_ADDRESS: '0xC02aaa39b223FE8D0A0E5C4F27eAD9083C756Cc2', // WETH address
            DAI_ADDRESS: '0x6B175474E89094C44Da98b954EedeAC495271d0F', // DAI address
            wallet: 'YOUR_WALLET_ADDRESS',
            nodeURL: 'YOUR_NODE_URL',
            routerAddress: 'YOUR_ROUTER_ADDRESS',
            routerABI: 'YOUR_ROUTER_ABI',
            decimalABI: 'YOUR_DECIMAL_ABI',
            mode: 'normalMode', // 'buyMode' or 'sellMode'
        };

3. Create an asset.json file in the root directory to define your token assets:

        {
            "0xYourTokenAddress": {
                "amount": "5%",
                "vwap": 0.05,
                "slippage": 0.5,
                "gasPrice": 100,
                "gasLimit": 21000
            }
        }

### Usage

1. Start the server:

        $npm start

        The server will start on port 5000. You can interact with the bot using WebSocket clients or through the provided web interface.

2. WebSocket API

    2.1. Connect

        Connect to the WebSocket server:

        const ws = new WebSocket('ws://localhost:5000/connect');
        ws.onopen = function () {
            ws.send('connectRequest');
        };

    2.2. Commands

        Send commands to the bot through the WebSocket connection:

        Add Token Address:
        {
            "id": "addTokenAddress",
            "tokenAddr": "0xYourTokenAddress",
            "amount": "5%",
            "vwap": 0.05,
            "slippage": 0.5,
            "gasPrice": 100,
            "gasLimit": 21000
        }

        Delete Token Address:
        {
            "id": "deleteTokenAddress",
            "tokenAddr": "0xYourTokenAddress"
        }

        Delete All Tokens:
        {
            "id": "deleteAll"
        }

        Start VWAP Bot:
        {
            "id": "startVwapBot",
            "botStatus": true,
            "walletAddr": "YOUR_WALLET_ADDRESS",
            "mode": "normalMode",
            "nodeURL": "YOUR_NODE_URL",
            "address": "YOUR_PRIVATE_KEY"
        }

        Stop VWAP Bot:
        {
            "id": "stopVwapBot",
            "botStatus": false
        }

        Start Limit Bot:
        {
            "id": "startLimitBot",
            "botStatus": true,
            "walletAddr": "YOUR_WALLET_ADDRESS",
            "mode": "buyMode",
            "tokenAddress": "0xYourTokenAddress",
            "amount": "5%",
            "limitPrice": 1000,
            "slippage": 0.5,
            "gasPrice": 100,
            "gasLimit": 21000,
            "frontrun": false,
            "nodeURL": "YOUR_NODE_URL",
            "address": "YOUR_PRIVATE_KEY"
        }

        Stop Limit Bot:
        {
            "id": "stopLimitBot",
            "botStatus": false
        }