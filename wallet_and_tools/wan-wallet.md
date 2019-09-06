# Wan Wallet 

![](media/wan_wallet_1.png)
## Wallet Features

Wanchain's first official desktop light wallet is available on Mac, Windows, and Linux. The initial release will support these functions:

* WAN asset management
* Standard transfer and receive transactions
* Making and managing delegations under Galaxy Consensus Proof of Stake
* Ledger hardware wallet support

Upcoming features to be implemented before the end of 2019 include:

* Staking support for validator node operators (will be implemented 3rd quarter along with the launch of Galaxy Consensus on the mainnet).
* Multi-crypto asset management support (4th quarter 2019)
* Private transactions (4th quarter 2019)
* Cross chain transactions (4th quarter 2019)

## Download and Install
Download [Wan Wallet](https://medium.com/r/?url=https%3A%2F%2Fgithub.com%2Fwanchain%2Fwan-wallet-desktop%2Freleases).

Double click the install package and follow the on screen instructions to install.

## Register New Account

When you first open Wan Wallet, you must register a new account. First set your password:

![](media/wan_wallet_2.png)

IMPORTANT: Next record your backup mnemonic phrase. Do not take a screenshot, rather you should write it by hand. Do not share your phrase with anyone. This phrase is the only way to recover your account. 

![](media/wan_wallet_3.png)

*Note: this is a throw away account, NEVER share your seed phrase with anyone Click 'Next' to complete the new account registration process.*

## Generate a New Address 

Wan Wallet supports the creation of multiple addresses for one account, simply click: Wallet > WAN > Create

![](media/wan_wallet_4.png)
*Wallet > WAN > Create*

Accounts may also be renamed as you wish.

## Get Testnet WAN

You can get testnet WAN from our [faucet](http://54.201.62.90/). Follow the instructions in the link to have testnet WAN sent to your account.

## Normal Transactions
Click 'Send', enter sending and receiving account information along with the transaction amount, select the service fee, and click next, and then click send again to complete your transaction.  

Under 'Advanced Options' are additional parameters which advanced users may adjust.

![](media/wan_wallet_5.png)
![](media/wan_wallet_6.png)

## Delegation
Wanchain's newly introduced Galaxy Consensus Proof of Stake has a completely non-custodial delegation mechanism. Users may choose from amongst all available validators the one which they trust to send their delegations too. By delegating their stake to validator nodes in this way, all users have the opportunity to earn consensus rewards. The minimum required amount for delegation is 100 WAN. 

Within the delegation interface users may clearly check their amount of staked WAN, their accumulated rewards from delegation, the yearly return rate for the entire network, and pending withdrawals. Users can also check a table of all their previous delegation transaction history. 

![](media/wan_wallet_7.png)

In order to make a new delegation, click 'New Delegation', choose a validator from the list, under 'My Account', choose the account from which you would like to delegate, and enter the amount you would like to delegate in the 'Amount' field. During the process of delegation, there are several parameters you should pay attention to. First, the validator's 'Quota' represents the amount of WAN that validator is able to accept in delegations. Please also note the 'Fee' parameter. This parameter is the percent fee charged as commission by the validator. For example, if the network reward is 50 WAN and the fee is 15%, then you will receive 42.5 WAN as your reward, and 7.5 WAN will be paid to the validator.

In the images below, a user is delegating 100 WAN to a validator node. 

![](media/wan_wallet_8.png)
![](media/wan_wallet_9.png)

After a completing a delegation, you can see 100 WAN displayed under "My Delegations." Previous delegation details may be viewed from within the delegations history. If the user wishes to increase their delegation, they may click on the 'Top up' button. 

**Note:** Users may exit their delegation at any time, but please note there is ~3 epoch unlocking period after which you can withdraw your WAN.

**Note:** Be sure to turn Contract Data on if you are using a Ledger hardware wallet.

![](media/wan_wallet_10.png)

## Validator Node Registration
To access the validator node menu, make sure that you have checked the "Enable Validator" box inside the Settings menu. The "Validator" option will then appear under the "Galaxy PoS" tab on the left.

![](media/wan_wallet_16.png)

To register your validator node and start staking, click "Register".

![](media/wan_wallet_17.png)

Fill in all the required parameters which were obtained during your [validator setup](staking/node-setup-mainnet) under the "Validator Account" section, and fill in all the information from your funding wallet under "My Account". If you are using Ledger, make certain that you have turned Contract Data on in the settings. When selecting locking period, please note that the longer your locking period, the higher your reward rate. Please use the [staking calculator](http://calculator.wandevs.org/) for reward rate estimates.

![](media/wan_wallet_18.png)

## Hardware Wallet
Currently the Ledger hardware wallet is supported. Follow the on screen instructions to connect your Ledger. Other hardware wallets may be supported in the future. Make sure to turn Contract Data on for validation or delegation transactions.

![](media/wan_wallet_11.png)


## Settings
There are currently three selections under settings, 'Config', 'Backup' and 'Restore'.

Under 'Config', you may choose to require your password to be input for every transaction.

![](media/wan_wallet_12.png)

Under 'Backup', you may enter your password to get your backup mnemonic phrase.

![](media/wan_wallet_13.png)

Under 'Restore', you may enter your backup phrase to restore a previous wallet.

![](media/wan_wallet_14.png)

## Multilingual Support
Under Settings > Language, you may choose between English and Mandarin Chinese. In the future, we will add support for French, Spanish, Japanese, Korean, and other languages.

![](media/wan_wallet_15.png)

Thank you for downloading and testing the new Wan Wallet! If you have any questions, please feel free to get in touch at techsupport@wanchain.org.  
