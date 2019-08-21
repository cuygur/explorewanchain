# Command Line Based Delegation

For simple delegation, please delegate through the official [WanWallet](https://github.com/wanchain/wan-wallet-desktop/releases) or [MyWanWallet](https://mywanwallet.nl/).

#### 1）Install docker(Ubuntu):
```
$ sudo wget -qO- https://get.docker.com/ | sh

$ sudo usermod -aG docker YourUserName

$ exit
``` 

#### 2）Create an account and find the validator node information. 

*Please note that before using pos.getStakerInfo to get the validator node information you should confirm that it has been synchronized to the latest block. This can be viewed by eth.blockNumber.*

The verification node information can be found through the command line or through the explorer.

```
$ docker run -d -v /home/YourUserName/.wanchain:/root/.wanchain wanchain/wanpos /bin/gwan

YourContainerID

$ docker exec -it YourContainerID /bin/bash

root> gwan attach .wanchain/testnet/gwan.ipc

> personal.newAccount('YourPassword')

"YourAccountAddress"

> pos.getStakerInfo(eth.blockNumber)
[
  {...},
  {...},
  {  Address: "DelegateAddress",
    Amount: 2e+23,
    Clients: [],
    FeeRate: 10,
    From: "...",
    LockEpochs: 30,
    PubBn256: "...",
    PubSec256: "...",
    StakingEpoch: 117
  }
]
```

Through the above procedure, the local account `YourAccountAddress` and the validator node address `DelegateAddress` with the commission rate `FeeRate` are obtained.

#### 3）Make sure your test account address has sufficient WAN test coins (at least 100 clients)

#### 4）Create script /home/YourUserName/.wanchain/sendDelegate.js

```
//sendDelegate.js

// If you want to send to a delegate you can modify and use this script.


//-------INPUT PARAMS YOU SHOULD MODIFY TO YOURS--------------------

// tranValue is the value you want to stake in minValue is 100
var tranValue = "100000"

// delegateAddr is the validator address copied from the list of validators generated in Step 4
var delegateAddr = "DelegateAddress"

// baseAddr is the fund source account.
var baseAddr  = "YourAccountAddress"

// passwd is the fund source account password.
var passwd    = "YourPassword"

//-------INPUT PARAMS SHOULD BE REPLACED WITH YOURS--------------------


//------------------RUN CODE DO NOT MODIFY------------------
personal.unlockAccount(baseAddr, passwd)
var cscDefinition = [{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}];


var contractDef = eth.contract(cscDefinition);
var cscContractAddr = "0x00000000000000000000000000000000000000da";
var coinContract = contractDef.at(cscContractAddr);

var payloadDelegate = coinContract.delegateIn.getData(delegateAddr)
var tx2 = eth.sendTransaction({from:baseAddr, to:cscContractAddr, value:web3.toWin(tranValue), data:payloadDelegate, gas: 200000, gasprice:'0x' + (200000000000).toString(16)});
console.log("tx2=" + tx2)
//------------------RUN CODE DO NOT MODIFY------------------
``` 

#### 5）Run a bet script in gwan to finish
 
```
$ docker exec -it YourContainerID /bin/bash

root> gwan attach .wanchain/gwan.ipc

> loadScript("/root/.wanchain/sendDelegate.js")
```
