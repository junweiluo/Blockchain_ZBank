# Build a blockchain step by step

* Create a new project directory for your new network. 

Activate Ethereum virual environment.
Create a folder <Blockchain-ZBank) that contains all blockchain tools.

* Create accounts for two (or more) nodes for the network with a separate `datadir` for each using `geth`.

 ./geth account new --datadir node1
 ./geth account new --datadir node2

* Run `puppeth`, name your network, and select the option to configure a new genesis block.

Open a new terminal, activate Ethereum virtual environment, navigate to the project folder

./puppeth

Specify a network name:

<your choice>

What would you like to do?

2. Configure new genesis

What would you like to do?

1. Create new genesis from scratch	

Which consensus engine to use

2. Clique - proof of authority

Which accounts should be pre-funded? (advisable at least one)

> 0x

* Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

Which accounts should be pre-funded? (advisable at least one)

> 0x

> 0x

* You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)

> no

Specify your chain/network ID if you want an explicit one (default = random)

>

* Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
> 2

* Export genesis configurations. This will fail to create two of the files, but you only need `networkname.json`.
 1. Modify existing configurations
 2. Export genesis configurations
 3. Remove genesis configuration
> 2

Which folder to save the genesis specs into? (default = current)
>

* Screenshot the `puppeth` configuration once complete and save it to the Screenshots folder.
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/03.puppeth_configuration.png)
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/04.puppeth_configuration.png)

* Initialize each node with the new `networkname.json` with `geth`.

Open a new terminal, activate virtual environment, navigate to project folder.

![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/05.initiate_node1.png)
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/06.initiate_node2.png)

* Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.

In a different terminal.

./geth --datadir node1 --networkid 1000 --unlock <address> --mine --minerthreads 1 --allow-insecure-unlock
 
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/07.unlock_node1.png)

* Set a different peer port for the second node and use the first node's `enode` address as the `bootnode` flag.

In a differernt terminal

./geth --datadir node2 --networkid 1000 --port 30304 --rpc —unlock <Address> --bootnodes "enode:<from node1>" --allow-insecure-unlock
 
* Be sure to unlock the account and enable mining on the second node!

![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/08.unlock_node2.png)

* You should now see both nodes producing new blocks, congratulations!

### Send a test transaction

* Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

* You will need to use a custom network, and include the chain ID, and use ETH as the currency.
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/09.setup_account.png)

* Import the keystore file from the `node1/keystore` directory into MyCrypto. This will import the private key.

* Send a transaction from the `node1` account to the `node2` account.
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/10.send_ETH.png)
* Copy the transaction hash and paste it into the "TX Status" section of the app, or click "TX Status" in the popup.
![](https://github.com/junweiluo/Blockchain_ZBank/blob/master/Screenshots/11.successful_transaction.png)
* Screenshot the transaction metadata (status, tx hash, block number, etc) and save it to your Screenshots folder.

* Celebrate, you just created a blockchain and sent a transaction!

### Create a repository, and instructions for launching the chain

* Create a `README.md` in your project directory and create documentation that explains how to start the network.

* Remember to include any environment setup instructions and dependencies.

* Be sure to include all of the `geth` flags required to get both nodes to mine and explain what they mean.

* Explain the configuration of the network, such as it's blocktime, chain ID, account passwords, ports, etc.

* Explain how to connect MyCrypto to your network and demonstrate (via screenshots and steps) and send a transaction.

* Upload the code, including the `networkname.json` and node folders.

### Remember, *never* share your mainnet private keys! This is a testnet, so coins have no value here!

### Challenge mode

* Create a separate `bootnode` dedicated to connecting peers together

* There will be a new DevOps engineer joining the team, add an additional sealer address to the network on the fly!
