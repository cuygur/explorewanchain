# 常用操作
### 账号创建
```
$ gwan --testnet account new
```

执行上述命令后，keystore文件会存储在默认目录 `~/.wanchain/testnet/keystore/` in Ubuntu 或者 `~/Library/Wanchain/testnet/keystore/` in Mac OS.

使用如下命令获取两个星系共识需要用到的公钥。

```
$ gwan --testnet account pubkeys 'Your Address' 'Your Password'
```

星系共识需要使用key1和key3，作为SecPk和G1PK。

### 查询余额

```
// In ubuntu
$ gwan attach ~/.wanchain/testnet/gwan.ipc

// In MacOS
$ gwan attach ~/Library/Wanchain/testnet/gwan.ipc
```

在链同步完成后，可通过下面指令查询余额。

```
$ eth.getBalance("Your Address Fill Here")

// Such as address example shown above.
$ eth.getBalance("0x8c35B69AC00EC3dA29a84C40842dfdD594Bf5d27")
```

### 获取测试币

请登录http://wanchain.mikecrm.com/USjDMuk进行填表申请。

 

### 如何运行两大节点

非验证节点（全节点）

$ gwan --testnet --rpc --syncmode "full"
 

验证节点

在下面命令中请替换地址为您的个人地址 0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e ，并替换 /tmp/pw.txt 为您地址的密码文本文件。

$ gwan --testnet --rpc --etherbase "0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e" --unlock "0x8d8e7c0813a51d3bd1d08246af2a8a7a57d8922e" --password /tmp/pw.txt--rpc  --mine --minerthreads=1 --syncmode "full"
 

5. Stake注册和委托投注

用户注册一个节点服务器为星系共识验证节点的步骤如下图所示：





用户通过Stake register注册成为验证节点。



Wanchain提供了基于智能合约的注册和注销功能，合约参数如下：

var cscDefinition =[{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}]
 

在智能合约的参数中, feeRate 是委托费率，通过设置合理费率吸引更多的委托人投注。

 

测试者可以直接修改代码目录下的脚本文件来完成验证节点的注册 loadScript/validatorRegister.js，委托人投注脚本loadScript/sendDelegate.js



脚本可在IPC链接到节点后执行。



// This path is a relative path for yourrun.
$ loadScript('loadScript/register.js')


测试者可在浏览器中查询收益信息、收益率预测等。



6. 退本金方法

验证节点退本金


验证人可使用stakeUpdate.js脚本，将locktime设成0，来实现退款。本金将在下个周期开始时，自动退回来源账户。



默认情况下，验证人会自动续期。需要手动操作才能退本金。



stakeUpdate.js脚本如下：

//-------INPUT PARAMS YOU SHOULD MODIFY TO YOURS--------------------

// This is update validator address.
var validatorAddr = ""

// Next period lock epochs.
var lockTime = 0

// baseAddr is the fund source account.(wallet)
var baseAddr = ""

// passwd is the fund source account password.
var passwd = ""

//-------INPUT PARAMS YOU SHOULD MODIFY TO YOURS--------------------

//------------------RUN CODE DO NOT MODIFY------------------
/////////////////////////////////register staker////////////////////////////////////////////////////////////////////////
personal.unlockAccount(baseAddr, passwd)
var cscDefinition = [{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"renewal","type":"bool"}],"name":"partnerIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}];
var contractDef = eth.contract(cscDefinition);
var cscContractAddr = "0x00000000000000000000000000000000000000DA";
var coinContract = contractDef.at(cscContractAddr);
var payload5 = coinContract.stakeUpdate.getData(validatorAddr, lockTime)
console.log("payload5: ", payload5)
var tx = eth.sendTransaction({from:baseAddr, to:cscContractAddr, value:'0x00', data:payload5, gas: 200000, gasprice:'0x' + (200000000000).toString(16)});
console.log("tx5= " + tx)
/////////////////////////////////unregister staker//////////////////////////////////////////////////////////////////////


委托人退本金



通过钱包投注的委托人，可直接通过钱包的退款按钮退款。



通过脚本注册的委托人，可通过delegateOut.js脚本完成退本金操作。



delegateOut.js脚本如下：

// If you want to send to a delegate you can modify and use this script to run.


//-------INPUT PARAMS YOU SHOULD MODIFY TO YOURS--------------------

var validatorAddr = ""

// baseAddr is the fund source account.
var baseAddr  = ""

// passwd is the fund source account password.
var passwd    = ""

//-------INPUT PARAMS YOU SHOULD MODIFY TO YOURS--------------------


//------------------RUN CODE DO NOT MODIFY------------------
personal.unlockAccount(baseAddr, passwd)
var cscDefinition = [{"constant":false,"inputs":[{"name":"addr","type":"address"}],"name":"stakeAppend","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"lockEpochs","type":"uint256"}],"name":"stakeUpdate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"secPk","type":"bytes"},{"name":"bn256Pk","type":"bytes"},{"name":"lockEpochs","type":"uint256"},{"name":"feeRate","type":"uint256"}],"name":"stakeIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"addr","type":"address"},{"name":"renewal","type":"bool"}],"name":"partnerIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateIn","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"delegateAddress","type":"address"}],"name":"delegateOut","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}];
var contractDef = eth.contract(cscDefinition);
var cscContractAddr = "0x00000000000000000000000000000000000000DA";
var coinContract = contractDef.at(cscContractAddr);

// delegateOut
var payloadDelegate5 = coinContract.delegateOut.getData(validatorAddr)
var tx5 = eth.sendTransaction({from:baseAddr, to:cscContractAddr, value:'0x00', data:payloadDelegate5, gas: 200000, gasprice:'0x' + (200000000000).toString(16)});
console.log("tx5= " + tx5)
//------------------RUN CODE DO NOT MODIFY------------------

