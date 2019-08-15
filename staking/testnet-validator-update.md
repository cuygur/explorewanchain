# Testnet Validator 2.1.2 Update

Both Wanchain's mainnet and testnet GWAN version has been updated to 2.1.2. If you want to continue running the test network, please upgrade to the 2.1.2 version to avoid forking.

If you do not want to continue running the test network node, but want to go to the mainnet node, please make sure to log out of the test network to ensure that the test network can continue to function normally.

## Test Network Validator Node Update

Use the following script to update your validator node to the latest 2.1.2 version

Versions below 2.1.2 will stop at block number 4,204,545 and cannot continue to sync.

```
$ rm updateValidator.sh
$ wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/updateValidator.sh && chmod +x updateValidator.sh && ./updateValidator.sh
```

After the update is completed, be sure to check the work log of the new version of gwan through the `sudo docker logs -f gwan` command to see if it worked.

If you find a `reorg` related ERROR message, such as: `Impossible reorg because reorg length is bigger than K`, you need to remove the chain resynchronization as follows:

```
sudo docker stop gwan
sudo docker rm gwan
sudo rm -rf .wanchain/testnet/gwan
rm updateValidator.sh
wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/updateValidator.sh && chmod +x ./updateValidator.sh && ./updateValidator.sh
```

## Test Network Validator Node Exit Method

You may use MyWanWallet to exit from the staking by using the staking smart contract and selecting the stakeUpdate function. Simply update your lockEpochs to 0, and your node will automatically exit at the end of the cycle.


For the loadScript method, you can use the script at this url https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/stakeUpdate.js to exit. After filling in the corresponding address and password, fill in the locktime value to 0 and run it through the ipc console of gwan using loadScript().
```
$ wget https://raw.githubusercontent.com/wanchain/go-wanchain/develop/loadScript/stakeUpdate.js

$ vi stakeUpdate.js

# Replace with your address and password and set locktime to 0

$ cp stakeUpdate.js .wanchain/

$ docker exec -it `docker ps -q` /bin/gwan attach /root/.wanchain/testnet/gwan.ipc

> loadScript('/root/.wanchain/stakeUpdate.js')

# After returning successfully, you can stop Docker 

> exit

$ sudo pkill gwan
$ sudo docker rm gwan
```

After the main network has been officially launched, registration and exit can be performed through the GUI light wallet, and the operation is more convenient.
