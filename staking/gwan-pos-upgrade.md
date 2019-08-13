
# Wanchain GWAN Client PoS Upgrade

Wanchain’s consensus will upgrade to proof of stake with a hard fork at block height 4046000

 On August 12, 2019, the Wanchain’s official client GWAN was released with support for Galaxy Proof of Stake Consensus. The Wanchain mainnet will hard fork at block height of 4046000 to complete the switch to PoS consensus. 

Please be sure to upgrade your GWAN client as soon as possible. Otherwise, you will not be able to synchronize blocks under the new consensus mechanism.

The latest GWAN version number is: v2.1.2

The download address is: [https://github.com/wanchain/go-wanchain/releases/tag/v2.1.2](https://github.com/wanchain/go-wanchain/releases/tag/v2.1.2)

After the download is complete, you can use the following command to verify that the version number is correct:

    $ ./gwan version

The new version of GWAN is fully compatible with the old version of the chain data, so you can directly replace the old version of GWAN with the new version of GWAN for a smooth upgrade.

The following is a brief description of the steps:
> **Note:** Specifics may vary according to your local environment. These instructions are provided for your reference. If you are in doubt, please ask for help in the official [WanDevs Gitter](https://gitter.im/wandevs/community). Please contact @molin0000 with any of your questions.

**1.** Download the latest version of GWAN at:

 [https://github.com/wanchain/go-wanchain/releases/tag/v2.1.2](https://github.com/wanchain/go-wanchain/releases/tag/v2.1.2) 

Select the version that matches your operating system.

After unzipping, use the ./gwan version command to query and confirm the version number.

![](https://cdn-images-1.medium.com/max/3572/0*vd2lX59FrREegzc2.png)

**2.** Back up the old node

Back up the command line startup parameters (highlighted in red in the screenshot) and old GWAN files.

![](https://cdn-images-1.medium.com/max/2000/0*4l7bEAy5s154bplY.png)

**3**. Stop the old version of the GWAN node from running with the following command

    $ pkill gwan

![](https://cdn-images-1.medium.com/max/2000/0*QmaoHJPio9BIFIlz.png)

**4.** Replace the old version of GWAN node with the new version

![](https://cdn-images-1.medium.com/max/2000/0*Bh6KyoCLxSbwQLbl.png)

**5.** Start with the new version of GWAN

Start the new version of GWAN using the original boot method and startup parameters

Check the GWAN log to ensure that you can start and synchronize new blocks properly.

The upgrade is now complete.

![](https://cdn-images-1.medium.com/max/2000/0*oI-SogZwFQlXdBfw.png)

If you use Wanchain’s full-node wallet, you will be prompted to upgrade after opening the wallet. Please select the DOWNLOAD NEW VERSION button to upgrade. After the upgrade is successful, it can be used normally.

![](https://cdn-images-1.medium.com/max/2800/0*gTYeYeLs9nDkXuEr.png)

