# Wanchain主网验证节点创建教程

## 通过脚本部署节点

### 运行脚本创建并启动validator

在ssh登录到云服务器后，执行如下命令：

```
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/deployMainnetValidator.sh && chmod +x deployMainnetValidator.sh && ./deployMainnetValidator.sh
```

脚本将提示您输入validator的名字，这个名字用作wanstats网站上的监控显示名称，不代表区块链浏览器上的名称。

脚本将提示您输入validator账号的密码。在输入密码时屏幕上看不到任何输入的内容是正常的，输入完成后按回车即可。

脚本将提示您进行密码二次确认。

*请务必牢记此密码并妥善备份，此密码如果遗失没有任何办法可以恢复*

脚本执行完成后，会输出Important提示，包括：validator地址、2个公钥以及keystore的json内容，*请将其完整备份*下来供后续注册使用。

当节点运行发生意外导致数据全部丢失时，可用此备份内容配合密码恢复全部信息，所以请务必妥善备份。

如果需要重启节点，请使用如下命令：

```
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/restartValidator.sh && chmod +x restartValidator.sh && ./restartValidator.sh
```

可以使用如下命令查看工作日志：

```
sudo docker logs -f gwan
```

停止日志查看按Ctrl-C
