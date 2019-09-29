# Wan Wallet (Old Version)

# Install Wallet
## Download

Download Wanwallet installation file from https://wanchain.org/product

*Wanwallet supports **Linux, Windows, and OSX**, please download corresponding installation file for your OS.*

## How to verify the downloaded file:
1. Navigate to www.wanchain.org

![Navigating to www.wanchain.org](_media/navigatetowanchainorggif.gif)

2. On the left hand side under blockchain developers, click get started.
3. You will be navigated to https://www.wanchain.org/getstarted/ 
4. Scroll down to Wanchain Wallet
5. You will be presented with 4 different types of Wallets with the option of choosing an operating system.

6. <p>Wanchain has Wallets for Windows, OSX and Linux. Select the appropriate operating system and Wallet type. (As shown in the image above)</pr>
    <p>a. Desktop Light<br></pr>
    <pr>b. Desktop<br></pr>
    <pr>c. Offline and <br></pr>
    <pr>d. Mobile<br></pr>
**Example:** If you have a Mac Operating system and intend to download the Desktop wallet, follow the below steps as shown in the image.

![Mac desktop wallet](_media/walletexample.gif)

<pr>7. A pop-up with Wanchain Wallet Application Terms and Conditions will be shown, please read the terms and conditions carefully and at the bottom of the page, the SHA256 Check Value of the files will be shown.<br></pr>
<pr>8. Please note the Sha256 of the file you want to verify.<br></pr>
<pr>9. Click **Agree** and the download will begin.<br></pr>

## Verifying the file after downloading on Mac Operating system:

1. Open Terminal in Mac-OSX. 
2. Type the following command in the terminal:
> $ shasum -a 1 /path/to/file
**Example:**
>shasum -a 256 WanWalletGui-mac-3.0.28.zip

## Alternative Method:
1. Open Terminal
2. Change the directory to the one you have downloaded the file
**Example:** If you have downloaded the file to the desktop, your directory should look like 
/user/desktop
3. Type
>ls 
(This will show all the files in the current directory, check if WanWalletGui-mac-3.0.28.zip exists, if yes, type the following command:
> Shasum -a 256 WanWalletGui-mac-3.0.28.zip

It will return the Sha256 of the above selected file i..e, WanWalletGui-mac-3.0.28.zip

In the above image the Sha256 of the zip file mentioned on the website matches the output. It states that the file is secure and uncorrupted.

Follow the same steps for Desktop and Offline wallet. Please replace the name of the file WanWalletGui-mac-3.0.28.zip to the downloaded file.

## Verifying the file after downloading in Windows Operating system:
1. Navigate to the folder where the file has been downloaded.
2. Press Shift and right click in the window.
3. From the right click menu select OPEN POWERSHELL WINDOW HERE
4. Type the following command:
>certutil -hashfile WanWalletGui-installer-3.0.28.exe sha256
5. Hit enter, a string of 64 characters will be displayed. This is the SHA256 checksum of the application.

![](_media/hashinstructions.PNG)

In the Image above, the Sha256 of the file matches with the one mentioned on the website.
The Sha256 of the file has to match the one provided in the official website. 
**Example:** Downloading the file on windows operating system.

![](_media/windowsfilehash.gif)

This step will help you stay safe and verify if the files have been altered.

**Verifying the file after downloading in Linux Operating system:**

The following command will display SHA256 hash value on a Linux operating system:

>sha256sum <path>/<filename>`


## Installation and launch

Extract the file, run, wallet will begin to sync. Click the "LAUNCH APPLICATION" button to start the wallet

![](media/Wanwalletlaunch.png)


For Linux users: 

Setup by CLI: `sudo dpkg -i WanWalletGui-linux64-2.X.X.deb`

* Start by CLI for main network: `wanwalletgui`                

* Start by CLI for test network: `wanwalletgui --network testnet`

* Or click Wanwalletgui to start under `/usr/local/bin/`

## Toggle main / test network

Wanwallet works with both main and test networks of Wanchain and Ethereum.

Below you can see the Wanchain accounts overview page (also the default start-up page), you can access it anytime by clicking on the Wanchain logo on the upper-left corner.   

Use the menu option below (Develop--->Network) to switch between main network (default network) and test network. <span class="warning">WARNING: Never send assets from the main network to a test network address, as they will then be lost forever.</span>

![](media/Wanwallettogglenetwork.png)



## Create / Import accounts

These 2 options allow you to create new WAN or new ETH account. 

The "CREATE ACCOUNT" button in the upper-right corner only creates new WAN account

![](media/Wanwalletcreateaccount.png)

You can also import an existing WAN or ETH account using a wallet keystore file

    File -> Import accounts -> Drag & Drop -> Done


## Backup Account

The keystore is where your account details are stored. <span class="warning">WARNING: If you lose your keystore files and have no other backup your assets will be lost forever, and no one, including the team at Wanchain, will be able to restore them.</span> Therefore we strongly recommend you backup all keystore files in a place you trust and won’t forget (offline PC device or storage device, etc.)

Do NOT share or reveal your keystore information with anyone, as they will then have full access to all of your funds. If you think your keystore has been leaked to any 3rd party, immediately transfer your assets to a new account.

To find your backup files, navigate as follows.

    File -> Backup -> Accounts -> Keystore

## Backup Application Data

To backup your application data, navigate as follows.

*Click File -> Backup -> Application Data*

You will see files under **WanWalletGui** by default. Please select them all and make copy to a safe place where you can trust.

The Accounts & Application Data stores all your public transaction records, private transaction records and OTA balance. If you delete these files , you will not lose your assets but you will not be able to see your assets at your current wallet at meantime unless you back them up in advance . However, you can always call it back via “Import Account” which we have demonstrated to you in above content.


# Transactions Guide


1. [Cross Chain Transactions](#crosschain)   
  * [ETH to Wanchain](#ethtowan)
  * [WETH to Ethereum](#wethtoeth)
1. [Normal Wanchain Transactions](#wan)
1. [Normal Ethereum Transactions](#eth)   
1. [Private Transactions](#private)   



<div id="crosschain"></div>  

## Cross-Chain Transactions

Crosschain transactions are under this tab

![](media/Wanwalletcrosschain.png)

Before you make a crosschain transaction, please check WAN and ETH balance in your account in Wanwallet GUI or with links below.

Main network：

* ETH: https://etherscan.io/

* WAN: https://www.wanscan.org/


Test network：

* ETH: https://rinkeby.etherscan.io/

* WAN: http://13.58.108.244/

<div id="ethtowan"></div>  

### Send ETH to Wanchain

Click the "ETH >> WETH" tab below to send ETH to Wanchain

![](media/WanwalletETHtoWanchain.png)

Enter your password then press “OK” button to send the transaction.

![](media/WanwalletsendTransaction.png)


#### Confirm/Cancel the transaction

In the "Transaction history" tab, click on the “**Confirm**" button to finalize the cross-chain transaction process once it _**turns red**_.

![](media/Wanwalletconfirmcanceltransaction.png)

If you do not confirm before the HTLC countdown ends, it means you choose to cancel the transaction and refund the ETH from the locked account. 
The "Confirm" button changes to "**Cancel**" and you can click it to cancel the transaction once it _**turns red**_



#### Option A) Confirm transaction

Once the “Confirm” button turns **red**, click it to access “**Confirm Transaction**” page.

![](media/Wanwalletconfirmtransaction1.png)

Enter the password then click “OK” button to finalize transaction 

![](media/Wanwalletconfirmtransaction2.png)



#### Option B) Cancel transaction

Once the “Cancel” button turned **red** (after countdown ends), click it to access “**Cancel Transaction**” page.

![](media/Wanwalletcanceltransaction1.png)

Enter the password then click “OK” button to cancel the transaction 

![](media/Wanwalletcanceltransaction2.png)

<div id="wethtoeth"></div>  

### Send WETH to Ethereum

If you have ETH balance on Wanchain (WETH balance), you can send WETH back to Ethereum.

Click the "WETH >> ETH" tab below to perform this kind of cross-chain transaction.    

![](media/WanwalletWETHtoETH.png)

The process is similar to the ETH to Wanchain one, please refer to section 7 for details about how to confirm or cancel the transaction.


<div id="wan"></div>  

## Normal Wanchain transactions

To make a regular on chain Wanchain transaction, click the "Transfer" button from the home screen of the wallet. 

![](media/wanhome.jpg)

Fill in "To" and "From" accounts, "Amount", and "Fee", then click the "Send" button to complete your transaction.

![](media/wantrans.jpg)

<div id="eth"></div> 

## Normal Ethereum transactions

You can perform Ethereum to Ethereum transactions through the official Wanchain wallet.

Click the "Normal transaction" tab below, fill source and destination accounts, transaction amount, fee preference, then click "SEND"

![](media/WanwalletETHtoETH.png)

<div id="private"></div> 

## Private Transactions

>#### NOTE: Public & Private Addresses  
>Transactions made using public addresses are, as the name suggests, publicly visible. Transactions made using your private address (do not confuse with private key) on the other hand, are not be publicly visible.  
>**Public Address Example**  
>`0xefe000C1b9f9ca9bf063857aAF5fCb7B8A25eaA1`  
>**Private Address Example:**  
>`0x02bddd6c139a10c5c9e81d1d6438dd26bc4a26824a2c729819d21ee1fca8b2dbc203936c798596ac4adcbe89e96c88397894b6dfab14a95ea7e137c31f56b9c81255`  

### Sending Private Transactions

**Step 1**: Click the **Transfer** button on the right to start a private transaction


![](media/WanchainPrivate1.png)

**Step 2**: Click **Switch to Private** in the **From** field and enter a **Private address** in the **To** field. The Recipient will need to share their Private address beforehand. Enter the amount of WAN to send and click **SEND** to start the private transaction. 


![](media/WanchainPrivate2.png)

**Step 3**: Enter the **Password** for your account and click **SEND TRANSACTION** to send a private transaction. 

![](media/WanchainPrivate3.png)


**Step 4**: The latest transaction is displayed at the top of the **Transaction List**. 

![](media/WanchainPrivate4.png)

**Step 5**: On the **Wanchain Explorer**, the **Value**  and the **To** address are masked and hidden from the public.

![](media/WanchainPrivate5.png)


### Receiving Private Transactions

**Step 1**: Click **Details** to view detailed account settings

![](media/WanchainPrivate6.png)


**Step 2**: Click **Get OTA (One Time Address)** to begin the process to receive a private transaction.

![](media/WanchainPrivate7.png)

**Step 3**: Enter the **Password** for your Account and Click **OK**. 

![](media/WanchainPrivate8.png)

**Step 4**: Wait a few minutes for the transaction to be processed and click **Redeem**. 

![](media/WanchainPrivate10.png)

**Step 5**: Click **Redeem** to accept the transaction.

![](media/WanchainPrivate11.png)

**Step 6**: The transaction details are show under **Redeem from OTAs**

![](media/WanchainPrivate12.png)
