# Staking FAQ

<ol>
  <li>
    <b>Q:</b> I successfully deployed a contract on Ethereum. Can I directly deploy it on Wanchain with the previously compiled files?  
  </li>
   <b>A:</b> Yes, the bytecode is the same.
   <br/><br/>
   
  <li>
    <b>Q:</b> I deployed a contract on the test chain, but I could not call the contract, what is the reason?  
  </li>
   <b>A:</b> Please change Solidity compiler to 0.5.1 or above.
   <br/><br/>

  <li>
    <b>Q:</b> My validator node has been running for +8 days now, but it seems that the 'Total reward' is still 0. Is there something in the configuration that I forgot to do? 
  </li>
    <b>A:</b> Please update GWAN to the most recent version.
    <br/><br/>

  <li>
    <b>Q:</b> What happens if I register the same pk1/pk2 from 2 addresses? 
  </li>
    <b>A:</b> The second register transaction will fail.
    <br/><br/>  

  <li>
    <b>Q:</b> The node syncing in GWAN is very slow.
  </li>
    <b>A:</b> Update to the newest version of GWAN.
    <br/><br/>

  <li>
    <b>Q:</b> Is it required to keep a copy of the keystore to receive rewards for the PoS Beta Testnet?
  </li>
    <b>A:</b> Yes, please keep it. If you lose it, please get in touch with us at info@wanchain.org. 
    <br/><br/>  

  <li>
    <b>Q:</b> How can I get the JSON keystore if I used the "Extended Setup" method? 
  </li>
    <b>A:</b> The keystore file is stored at ~/.wanchain/testnet/keystore by default.
    <br/><br/>

  <li>
    <b>Q:</b> How can I update the display name, logo, and website of my node?
  </li>
    <b>A:</b> Please email info@wanchain.org.
    <br/><br/>  

  <li>
    <b>Q:</b> What is benefit if I have more than 25 peers? 
  </li>
    <b>A:</b> There is no benefit.  The max peers defaults to 25, but may be modified.
    <br/><br/>

  <li>
    <b>Q:</b> Why do we need 256GB of disk space for a validator node? 
  </li>
    <b>A:</b> This takes into account long term growth. 40GB should be sufficient for the first year.
    <br/><br/>  

  <li>
    <b>Q:</b> For the final release, will we be able to register from WAN Wallet so that the keystore file or mnemonic phrase never leaves the machine? 
  </li>
    <b>A:</b> Yes this will be available when PoS launches on the mainnet.
    <br/><br/>

  <li>
    <b>Q:</b> I have my validator node's keystore, how can I import it to the Wan Wallet? 
  </li>
    <b>A:</b> The option is in the Wan Wallet menu under Wan Wallet > Developer > Assets > Wanchain > Import Keystore File.
    <br/><br/>  

  <li>
    <b>Q:</b> If a deployed a smart contract before POS, will it still be available after the switch on the mainnet? 
  </li>
    <b>A:</b> Yes, all smart contracts deployed before POS is rolled out on the mainnet will be unchanged by the rollout.
    <br/><br/>

  <li>
    <b>Q:</b> Is ok that some nodes did not receive any reward in last epoch? 
  </li>
    <b>A:</b> This is normal. A total of 49 slots are open for nodes to be chosen to participate within each epoch, and the same node may potentially fill multiple slots, so at most 49 nodes (but often less than 49 nodes) will be chosen to participate and receive rewards each epoch. The process is probabilistic with the chance to be chosen going up with the amount of stake and locking time. 
    <br/><br/>  

  <li>
    <b>Q:</b> I can see my node on http://testnet.wanstats.io/ but not on http://testnet.wanscan.org/vlds. Does the latter happen later? 
  </li>
    <b>A:</b> Yes, there can be a delay of several minutes. Also please verify your register transaction’s status at http://testnet.wanscan.org/. 
    <br/><br/>

  <li>
    <b>Q:</b> What are some other options besides AWS for running a node?
  </li>
    <b>A:</b> You can also try <a href="https://cloud.google.com/compute/">Google Cloud</a>.
    <br/><br/>  

  <li>
    <b>Q:</b> When registering my validator node through MyWanWallet.io, I keep getting a notice about insufficient funds. What should I do? Does my gas have to be a certain amount? 
  </li>
    <b>A:</b> Please wait for the gasLimit to be automatically estimated before making the transaction. 
    <br/><br/>
  <li>
    <b>Q:</b> Is a fixed IP needed for Wanchain Validator nodes? 
  </li>
    <b>A:</b> It is not needed.
    <br/><br/>  
  <li>
    <b>Q:</b> Can I use Ledger address to register as validator node? 
  </li>
    <b>A:</b> Not we do not currently support Ledger used to directly run a validator node.
    <br/><br/>  
 
  <!--<li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  
  <li>
    <b>Q:</b> 
  </li>
    <b>A:</b> 
    <br/><br/>  

-->

</ol>


   

  




