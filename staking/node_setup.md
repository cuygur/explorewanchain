# Validator Node Setup

This is a guide for helping getting started as a Wanchain Galaxy Consensus validator node. There are two options for setting up a validator node. [Quick Start](staking/node_setup?id=quick-start-from-script), or [Extended Setup](staking/node_setup?id=extended-setup). We recommend users follow the Quick Start guide. Please join our [Gitter chat room](https://gitter.im/wandevs/community) for additional guidance. 

Check your validator node's status at: [http://testnet.wanscan.org/](http://testnet.wanscan.org/)

Check the network status at: [http://testnet.wanstats.io/](http://testnet.wanstats.io/)

**Setup**
- We recommend using Linux or MacOS
- A wallet with the WAN you wish to stake + a small amount of WAN for service fees.
- You may use a cloud server such as AWS or run on bare metal. See our [AWS getting started guide](staking/aws.md) for more information.
- If using AWS, we recommend AWS m4.xlarge with the following configuration
  - CPU: 4
  - RAM:16G
  - Disk 256G
  
*For manual setup you also need:*
- [Docker](https://www.docker.com/)  
- Install Golang from https://golang.org/ and set GO environment variables `$GOPATH` and `$GOROOT` if you want to build from source code.

## Quick Setup

#### 1) Run a command to create and run validator

After ssh login into cloud server. Run this command below:

```bash
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/deployValidator.sh && chmod +x deployValidator.sh && ./deployValidator.sh
```

The script will prompt you to enter the name of the validator, which is used as the display name on the [wanstats website](http://testnet.wanstats.io/) and does not represent the name on the blockchain browser.

The script will prompt you to enter the password for the validator account.

After executing the script you should see three pieces of information that you need to save. That includes your validator public address, a pair of two validator public keys, and a JSON keystore. Keep all this information in a safe place.  

If you need to restart your node, please use the following script:

```
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/restartValidator.sh && chmod +x restartValidator.sh && ./restartValidator.sh
```

You can use the following command to see the validator logs (`Ctrl + c` to exit logs):

```
sudo docker logs -f gwan
```

#### 2) Register validator from wallet

Next, you can complete the validator registration behavior through the web based [MyWanWallet](https://mywanwallet.io/).

When registering in MyWanWallet, make certain to select the 'WAN Testnet' network in the upper right corner.  

Click on the Contract page and select the Staking contract.

After selecting Access, select StakeIn.

![](/media/8.png)

Fill in all the empty fields. 

The `secPk` and `bn256Pk` are the two public keys returned after the script is executed. 

The `lockEpochs` is the lock time, which ranges from 7 to 90 (one epoch is approximately one day, the chance for earning rewards increases with the length of lock time). 

`feeRate` is the commission rate, which ranges from 0 to 10000, representing a commission rate of 0.00% to 100.00%.

After filling out all the fields, select your wallet type.

**!!!WARNING!!!**

Do not use your validator account to fund the staking contract! The best security practice is to fund the account from a separate account secured with a hardware or offline wallet. The account which you use to fund the validator node will also be used to perform all staking related operations.

**!!!WARNING!!!**

Then click 'Write' to begin the transaction.

[](/media/stake_register.png)

In the pop up window, in the 'Amount to Send' field, enter the amount of WAN you will stake in your validator node.

In the 'Gas Limit' field, enter the gas limit for your transaction (21000 is the default, you may need to increase if there is network congestion). 

Click 'Yes, I am sure!' to complete your transaction. You can check your transaction by searching for your validator's address at [http://testnet.wanscan.org/](http://testnet.wanscan.org/). Your node should currently display `Joining` status. After 1-2 epochs (1 epoch ~ 1 day), your node will join the consensus process. To have your node name and logo displayed on the Wanscan website, please get in touch at [techsupport@wanchain.org](techsupport@wanchain.org).

#### 3) Fund Validator Address With Gas Fees
The validator address must be funded with a small amount of WAN in order to pay network fees associated with the consensus process.

Fees are generally not more than 0.01 WAN per transaction, so a transfer of 50 wan to the validator account can support long term use.

Please check the balance of the validator address regularly through the [WanScan](http://testnet.wanscan.org/) to ensure that transaction fees are always available.


## Extended Setup
*This method of setup is for advanced users. We recommend using the Quick Start guide above for most users.*

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

You can refer to THE [WanStats website](http://testnet.wanstats.io/) to check your node's status and network status. 

Setup is now complete, mining will begin as soon as syncing is finished.

![img](/media/5.png)


![img](/media/6.png)


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
