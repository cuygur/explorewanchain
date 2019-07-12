# 常用操作
7.1. 账号创建
$ gwan --testnet account new
执行上述命令后，keystore文件会存储在默认目录 ~/.wanchain/testnet/keystore/ in Ubuntu 或者 ~/Library/Wanchain/testnet/keystore/ in Mac OS.

使用如下命令获取两个星系共识需要用到的公钥。

$ gwan --testnet account pubkeys 'Your Address' 'Your Password'
星系共识需要使用key1和key3，作为SecPk和G1PK。

7.2. 查询余额
// In ubuntu
$ gwan attach ~/.wanchain/testnet/gwan.ipc

// In MacOS
$ gwan attach ~/Library/Wanchain/testnet/gwan.ipc

在链同步完成后，可通过下面指令查询余额。

$ eth.getBalance("Your Address Fill Here")

// Such as address example shown above.
$ eth.getBalance("0x8c35B69AC00EC3dA29a84C40842dfdD594Bf5d27")
7.3. 获取测试币
验证节点请在网页中填表申请测试币。（地址）

普通委托人请通过faucet申请少量测试币。Wanchain-Faucet

其它技术支持信息，还可以邮件联系。

或加入官网上的Gitter/QQ/微信社区群。

www.wanchain.org

Index	Email
1	techsupport@wanchain.org
7.4. Stake注册和代理流程
用户注册一个节点服务器为星系共识验证节点的步骤如下图所示：

img

7.5. 退本金方法
7.5.1. 验证节点退本金
验证人可使用stakeUpdate.js脚本，将locktime设成0，来实现退款。本金将在下个周期开始时，自动退回来源账户。

默认情况下，验证人会自动续期。需要手动操作才能退本金。

7.5.2. 委托人退本金
通过钱包投注的委托人，可直接通过钱包的退款按钮退款。

通过脚本注册的委托人，可通过delegateOut.js脚本完成退本金操作。
