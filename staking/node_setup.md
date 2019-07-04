# Validator Node Setup

This is a guide for helping getting started as a Wanchain Galaxy Consensus validator node. Please join our [Gitter chat room](https://gitter.im/wandevs/community) for additional guidance. 

**Software Environment**
- We recommend using Linux or MacOS
- Docker  
- Install Golang from https://golang.org/ and set GO environment variables `$GOPATH` and `$GOROOT` if you want to build from source code.
- You may use a cloud server such as AWS or run on bare metal. See our [AWS getting started guide](staking/aws.md) for more information.

## Quick start from Script

#### 1) Run a command to create and run validator

After ssh login into cloud server. Run this command below:

```bash
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/deployValidator.sh && chmod +x deployValidator.sh && ./deployValidator.sh
```

The script will prompt you to enter the name of the validator, which is used as the monitor display name on the wanstats website and does not represent the name on the blockchain browser.

The script will prompt you to enter the password for the validator account.

After the script is executed, the account address of the validator and the two public keys will be fed back. Please back it up completely for subsequent registration.

#### 2) Register validator from wallet

Next, you can complete the validator registration behavior through the wallet.

Register via web wallet: https://mywanwallet.io/

When registering in the web wallet, you need to pay attention to first select the network in the upper right corner. The beta phase requires the selection of a testnet network.

Click on the Contract page and select the Staking contract.

After selecting Access, select StakeIn to complete the node registration.

![img](/media/8.png)

**!!!Note!!!**

The `secPk` and `bn256Pk` are the two public keys returned after the script is executed.

The `lockEpochs` is the lock time, which ranges from 7 to 90.

Where `feeRate` is the commission rate, which ranges from 0 to 10000, representing a commission rate of 0.00% to 100.00%.

After filling out, select the wallet type and import the wallet.

The amount locked is entered on the next page.

Follow the prompts to complete the validator registration.

#### 3) Send Tx Gas Fee to Validator address

After the registration is completed, a small transaction fee is also transferred to the verification node address for the execution of the POS protocol fee.

The handling fee is generally not more than 0.01 wan per transaction, so a transfer of 50 wan to the validator account can support longe time use.

Please check the balance of the validator address regularly through the browser to ensure that transaction fees are always available.

## Quick start from Docker

#### Step by step node setup

**Step 1:** Install docker (Ubuntu):
```bash
$ sudo wget -qO- https://get.docker.com/ | sh

$ sudo usermod -aG docker YourUserName

$ exit
```

**Step 2:** Start GWAN with Docker and create account:
```bash
$ docker pull wanchain/client-go:2.0.0-beta.5

$ docker run -d -v /home/YourUserName/.wanchain:/root/.wanchain wanchain/client-go:2.0.0-beta.5 /bin/gwan --testnet

YourContainerID

$ docker exec -it YourContainerID /bin/bash

root> gwan attach .wanchain/testnet/gwan.ipc

> personal.newAccount('YourPassword')

"YourAccountAddress"

> personal.showPublicKey("YourAccountAddress", 'YourPassword')

["YourPK1", "YourPK2"]

> exit

root> echo "YourPassword" > /root/.wanchain/pw.txt

root> exit

```

![img](/media/1.png)

**Step 3:** Get test WAN for "YourAccountAddress":

Follow [6.3. Get test WAN](#63-get-test-wan) to get test WAN.

And after receiving test WAN, continue to step 4.

**Step 4:** Validator Registration

The validator registration can be done visually using the community-developed [mywanwallet] (https://mywanwallet.io/#contracts) web wallet. You can also use script registration as follows.

**!!!WARNING!!!**

In order to protect the security of the account, please do not enable the "--rpc" parameter when using script to register. Please verify before continue. (Recommended to use the GUI wallet for registration)

Create a script file in path: `/home/YourUserName/.wanchain/validatorRegister.js`

```javascript
//validatorRegister.js

// If you want to register as a validator you can modify and use this script.


//-------INPUT PARAMS SHOULD BE REPLACED WITH YOURS--------------------

// tranValue is the value you want to stake
// non-delegate mode validator - minValue is 10000
// delegate mode validator - minValue is 50000 
var tranValue = "50000"

// secpub is the validator node's secpub value
var secpub    = "YourPK1"

// g1pub is the validator node's g1pub value
var g1pub     = "YourPK2"

// feeRate is the percent of the reward kept by the node in delegation - 10000 indicates the node does not accept delegation.
// feeRate range is 0~10000, means 0~100.00%
var feeRate   = 2000

// lockTime is the length of stake locking time measured in epochs - minimum required locking time of 5 epochs
var lockTime  = 30

// baseAddr is the stake funding source account
var baseAddr  = "YourAccountAddress"

// passwd is the stake funding source account password
var passwd    = "YourPassword"

//-------INPUT PARAMS SHOULD BE REPLACED WITH YOURS--------------------


//------------------RUN CODE DO NOT MODIFY------------------
personal.unlockAccount(baseAddr, passwd)
var cscDefinition = [{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}];


var contractDef = eth.contract(cscDefinition);
var cscContractAddr = "0x00000000000000000000000000000000000000DA";
var coinContract = contractDef.at(cscContractAddr);

var payload = coinContract.stakeIn.getData(secpub, g1pub, lockTime, feeRate)
var tx = eth.sendTransaction({from:baseAddr, to:cscContractAddr, value:web3.toWin(tranValue), data:payload, gas: 200000, gasprice:'0x' + (200000000000).toString(16)});
console.log("tx=" + tx)
//------------------RUN CODE DO NOT MODIFY------------------

```
![img](/media/2.png)


![img](/media/3.png)

**Step 5:** Run the registration script in GWAN

If you have not closed the Docker script from **Step 2**, continue with the commands below, otherwise restart the Docker script.

```bash
$ docker exec -it YourContainerID /bin/gwan attach .wanchain/testnet/gwan.ipc

> loadScript("/root/.wanchain/validatorRegister.js")

> exit

$ docker stop YourContainerID

$ docker run -d -p 17717:17717 -p 17717:17717/udp -v /home/YourUserName/.wanchain:/root/.wanchain wanchain/client-go:2.0.0-beta.5 /bin/gwan --testnet --etherbase "YourAccountAddress" --unlock "YourAccountAddress" --password /root/.wanchain/pw.txt --mine --minerthreads=1 --wanstats your-node-name:admin@54.193.4.239:80

```

The "--wanstats your-node-name:admin@54.193.4.239:80" part in parameters is for collection of statistics information of node's operational status and network status in the PoS Beta Testnet.

Please customize "your-node-name" part with the node name you prefer, i.e. "Community-WAN-node_EMEA1". Please avoid using characters other than alphanumeric, dash and underscore, for example do not use spaces in node name.

You can refer to WanStats website to check your node's status and network status. 

The link to WanStats in Beta testing phase is:

http://54.193.4.239/

Setup is now complete, mining will begin as soon as syncing is finished.

![img](/media/5.png)


![img](/media/6.png)

## Delegation

See the [delegation guide](staking/delegation.md) for GUI and command line delegation instructions.

## GWAN Installation 


#### Option 1) Run from Docker

You can run a node from a Docker image. See section above - "Quick start from Docker"

#### Option 2) Download

You can download a binary file or code to run a node.

#### Option 2a) Download BIN

You can download the compiled binary file from the download links below:

(Currently unavailable, please use docker)

| OS            | URL            | MD5             | SHA256
| --------------  | :------------  | :-------------: | :--: |
|Ubuntu|gwan.tar.gz| XXXXXXXXXXXXXXXX |XXXXXXXXXXXXXXXXXXXXXXXXX
|Windows|gwan.tar.gz| XXXXXXXXXXXXXXXX |XXXXXXXXXXXXXXXXXXXXXXXXX
|MacOS|gwan.tar.gz| XXXXXXXXXXXXXXXX |XXXXXXXXXXXXXXXXXXXXXXXXX

#### Option 2b) Download Code and Compile

If you want to compile the Galaxy Consensus code, you should first to install the Golang development environment and config $GOPATH and $GOROOT:

https://golang.org/

You can download the code file and compile to run with the following steps:

If you already have a golang compile and run environment, and you have configured $GOPATH , you can get the code as below:

```bash
$ go get github.com/wanchain/go-wanchain

$ cd $GOPATH/src/github.com/wanchain/go-wanchain

$ git checkout betarelease

$ git pull

$ make
```

Or you can clone from github.com as below:

```bash
$ mkdir -p $GOPATH/src/github.com/wanchain/

$ cd $GOPATH/src/github.com/wanchain/

$ git clone https://github.com/wanchain/go-wanchain.git

$ cd go-wanchain

$ git checkout develop

$ git pull

$ make
```

Then you can find the binary file in path `build/bin/gwan`

## Node Type

You can run a node in two different modes, staking and non staking.

#### Non-staking node

```bash
$ gwan --testnet --syncmode "full"
```

#### Staking-node

In the following command, you should replace the `0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e` with your own account address and replace the `/tmp/pw.txt` file with your own password file with your password string in it.

```bash
$ gwan --testnet --etherbase "0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e" --unlock "0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e" --password /tmp/pw.txt  --mine --minerthreads=1 --syncmode "full"
```

## Common Operations

#### 1) PoS account creation

Before you run a PoS node you should create an account.

```bash
$ gwan --testnet console --exec "personal.newAccount('Your Password')"

// Or run after ipc attach
$ personal.newAccount('Your Password')
```

You can see your address created and printed in the screen, then you can press `Ctrl+C` to exit.

You will get a keystore file with three crypto key words in your path `~/.wanchain/testnet/keystore/` in Ubuntu or `~/Library/Wanchain/testnet/keystore/` in Mac OS.

And you can use a command to get the `Address Public Key` and `G1 Public Key` of your account.

```bash
$ gwan --testnet console --exec "personal.showPublicKey('Your Address', 'Your Password')"

// Or run after ipc attach
$ personal.showPublicKey('Your Address', 'Your Password')
```

These public keys will be used in staking registration.

#### 2) Check balance

You can check your balance in the address when you attach a GWAN console in the `ipc` file or use a console mode at GWAN start.

```bash
// In ubuntu
$ gwan attach ~/.wanchain/testnet/gwan.ipc

// In MacOS
$ gwan attach ~/Library/Wanchain/testnet/gwan.ipc

```

After the node synchronization is finished you can check your balance using the following command.

```bash
$ eth.getBalance("Your Address Fill Here")

// Such as address example shown above.
$ eth.getBalance("0x8c35B69AC00EC3dA29a84C40842dfdD594Bf5d27")
```

#### 3) Get test WAN

If you want to get some test WAN to experiment with Galaxy Consensus, you can fill a form on this URL: (Waiting to update...)

[Wanchain-Faucet](http://54.201.62.90/)

| Index            | Email         | 
| --------------  | :------------  | 
|1| techsupport@wanchain.org| 



#### 4) Registration and delegation

If you have an account with WAN coins and you want to create a Galaxy Consensus validator, you should do it as in the diagram below:

![img](/media/99.png)

You can register as a staking node through Stake register.

We have given a smart contract for registration and unregistration.

The contract interface is shown below.
```javascript
var cscDefinition = [{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}]
```

In the smart contract input parameters, the `feeRate` indicates the percentage of reward kept by the validator from the delegators' reward. 10000 indicates that the validator does not accept delegations. 

If you want to be an delegator and accept delegations from others, you need to set a reasonable percentage for your `feeRate` to attract others to invest.

The `feeRate`'s value ranges from 0 to 10000 and indicates the amount of reward kept by the validator (1000 means the validator will take a 10% fee, and the delegator will keep 90% of the reward).

You can register your stake with a custom script or just modify the module's script in `loadScript/validatorRegister.js`.

The JavaScript file `loadScript/register.js` is used by validators for registration, and `loadScript/sendDelegate.js` is used by test WAN holders for sending their delegation.

In the script file, the password should be replaced with your own in `personal.unlockAccount`.

`secpub`, `secAddr`, `g1pub` should be filled with your account's address public key, account address, and G1 public key. These public keys can be found using the function `personal.showPublicKey` shown above.

`lockTime` should be filled with the stake locking time. The unit of time is epoch. Epoch time is equal to SlotTime * SlotCount. 

The `tranValue` should be filled with the amount of WAN you want to lock in the smart contract for stake registration. You can't get it back until the locking time is up.

#### 5) Check rewards

You can check your balance as shown above to verify whether you have received a reward, and you can use the commands shown below to see which address was awarded and the reward amount for the specified epoch ID.

```bash
// In an attached IPC session to run for epoch 19000.
$ pos.getEpochIncentivePayDetail(19000)
```

#### 6) Unregister and Unlock

Validators can use `stakeUpdate.js` to set lock time to 0. It will be un-register at next period. 

Delegators can use Wan wallet to delegate In or delegate Out.
