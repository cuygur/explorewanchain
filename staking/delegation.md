# Delegation Guide

## Wallet Based Delegation
Since the [Beta version of the light wallet](https://github.com/wanchain/wan-wallet-desktop/releases) was released, delegators can use the visual interface of the wallet to delegate their WAN in Galaxy Consensus. Delegators may also choose to use the command line to delegate WAN.

Wanchain’s Galaxy Consensus has a complete delegation mechanism. As a delegator, a user can select a trusted validator in Wanchain’s network, and delegate his or her WAN to that validator, and get rewards from this kind of indirect staking. The minimum threshold for a delegator is 100WAN.

In the Delegation interface, a user can clearly get the general information of My Stake, My Reward, Average Network Reward and Pending Withdrawal. Meanwhile, he or she can view his or her delegation list and delegation history records.

Click New Delegation, and Select Name and Address under Validator’s Account to choose the node you wish to delegate to, select Address which you want to delegate from under My Account, and input Amount. For the delegation settings, you should pay attention to several parameters:

Quota, which represents how many remaining WAN this validator can receive;

Fee(%), which represents the percentage of WAN which will be deducted from the reward. For example, if the total reward is 50WAN, and the fee is 15%, the delegator will receive a final reward of 42.5WAN.

The following pictures shows a delegator who delegates 100WAN to a validator.

After successful delegation, My Stake shows 100WAN. This delegation record shows in the delegation list. If you want to top-up the delegation amount, you can click Top-up.

After the top-up is successful, the result is as below:

## Command Line Based Delegation

**Step 1:** Install Docker (Ubuntu):
```bash
$ sudo wget -qO- https://get.docker.com/ | sh

$ sudo usermod -aG docker YourUserName

$ exit
```

**Step 2:** Start [GWAN](https://wandevs.org/docs/set-up-wanchain-node/) with Docker, create account, and view delegate node list: (Make sure to replace `YourContainerID`, and `YourPassword` with your own information.)

```javascript
$ docker run -d -v /home/YourUserName/.wanchain:/root/.wanchain wanchain/client-go:2.0.0-beta.5 /bin/gwan --testnet

YourContainerID

$ docker exec -it YourContainerID /bin/bash

root> gwan attach .wanchain/testnet/gwan.ipc

> personal.newAccount('YourPassword')

"YourAccountAddress"

> pos.getStakerInfo(eth.blockNumber)
[
	{...},
	{...},
	{	Address: "DelegateAddress",
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

Take note of the values `YourAccountAddress`, `DelegateAddress`, and `FeeRate` which are returned from the above script.

**Step 3:** Get test WAN for "YourAccountAddress"

See [instructions for getting testnet WAN](staking/get_test_wan.md).

**Step 4:** Create a script file in path: `/home/YourUserName/.wanchain/sendDelegate.js`

```javascript
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
var cscContractAddr = "0x00000000000000000000000000000000000000DA";
var coinContract = contractDef.at(cscContractAddr);

var payloadDelegate = coinContract.delegateIn.getData(delegateAddr)
var tx2 = eth.sendTransaction({from:baseAddr, to:cscContractAddr, value:web3.toWin(tranValue), data:payloadDelegate, gas: 200000, gasprice:'0x' + (200000000000).toString(16)});
console.log("tx2=" + tx2)
//------------------RUN CODE DO NOT MODIFY------------------
```

**Step 5:** Run the registration script in GWAN

Load the script in GWAN to complete delegation.

```
> loadScript("/root/.wanchain/sendDelegate.js")

```

