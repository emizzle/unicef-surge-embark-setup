

# UNICEF Surge Bangkok - Embark Project Setup

## Slides

1.  What's in a DApp - fundamental components
2.  What is Embark
3.  Installation prerequisites - cover any issues with installation

## Hands-on
Now let's jump in to some hands-on examples

### Embark demo
First, we have the Embark demo DApp. This is a good example of what Embark can do in regards to the four fundamental components of a truly decentralised application.

1. Run `embark` without args to see command-specific help output. We will only be covering some of these today
2. The Embark demo serves as a good starting point to see what kind of functionality Embark offers.
3. Create an Embark demo app
```
cd ~/temp
rm -rf embark_demo
embark demo
cd embark_demo
```
4.  Tour of the DApp structure and components
	1. Contracts
	4. App source
	2. `embark.json` - Embark general configuration
	3. Configs
		1. Explain what environments are 
		2. Blockchain - In development, an account is created for us and loading with tons of ether. In other environments, an account is created with no ether, but it is that account we can use to interact with the blockchain. 
			1. Quick note on that: when we interact with a blockchain, we are interacting using our account. In traditional web terms, this is how we authenticate ourselves.
		3. Contracts - defines how we deploy our contracts, specify contract args. Explain how contracts need to be deployed on the blockchain, that they are issued an address, and anyone on that chain can interact with the contract with them given that address. When deployed, the constructor of the contract is called, and we pass in arguments for the constructor. This is all set up in the contracts config. For example, SimpleStorage is configured to pass in `100` as the initial value. We will get this value from the blockchain later. 
	

5.  Run the DApp with `embark run --nodashboard`
6.  Explain dashboard, services started
	1. **Geth** - local blockchain that we will deploy our contracts to
	2. **IPFS** - p2p file sharing node that is used to store assets and text
	3. Contracts compiled and deployed to geth
	4.  **Pipeline** has run which builds and webpacks all frontend assets for us.
7.  Tour of the DApp frontend and all the fundamental DApp components covered
	1. Run through all the functionality of the demo.
	2. Revisiting our fundamentals:
		1. **Compute**. We can call our smart contract and transact a value. And read it back.
		2. **Storage**. We can store some text in IPFS, and read it back. And we can upload an image, and download it.
		3. **Messaging**.  We can listen on a channel, and echo a message.
		4. **Name System**.  We can resolve a name from an address.  And we can resolve an address to a name.
    
8.  Launch Cockpit and take a tour
	1. **Dashboard** 
	    1. Services running
	    2. Console
		    1. Replicates Embark's console output, but also lets up issue commands, same as the CLI dashboard, type `help` for all commands. 
		    2. Try out some example commands:
			    1.  `web3.eth.defaultAccount` - this is the account created and unlocked for us by geth. Web3 is our javascript connection to the blockchain. It let's us connect to a node (in our case, our local node), then issue commands such as querying contracts, sending txs, and creating/unlocking accounts.
			    2. `EmbarkJS.Storage.isAvailable()` - a command that checks the status of our configured storage provider which is IPFS in this case
			    3. `SimpleStorage.methods.get().call()` - get the initial value stored in our contract 
	    3. Contracts section - this just shows an overview of which contracts have been deployed for us, with deep-linking in to more contract information, which we can get to via the Explorer tab
	2. **Explorer** 
		1. Dashboard shows an overview of the accounts on our node: you can see the account created for us by Geth and WE ARE RICH! Drilling down in the to the account, we can see detailed account information along with all transactions that have occurred in relation to that account.
		2. Summary view of the blocks created on the chain - drilling down in a block gets us detailed block info and all transaction contained in that block.
		3. Summary view of the transactions on the chain - drilling down in to a transaction get us detailed tx info, with the ability to deep link to associated blocks and accounts in relation to that tx. 
	3. **Editor** - there is a built in editor that lets you edit any file in your DApp. We are going to get in to this in more detail later.

9. Run DApp unit tests (`embark test`)
10. In a new terminal, upload the DApp to IPFS
	1. Explain how the DApp is available on our local node, and it will take a while to propagate to other seeds.

### "Real world" example - DReddit
1. Make sure the Metamask extension is disabled
2. Create a new DApp based on the DReddit template
	```
	embark new dreddit-unicef --template embark-framework/dreddit-unicef-surge-2019
	cd dreddit-unicef
	git init
	git add -A && git commit -m "first commit"
	```
3. Run the DApp and run CRA, then tour of the DApp functionality
	1. Run CRA `npm run start` and `embark run --nodashboard`.
	2. While this may not be a real world example, it does show working versions of CRUD operation in Ethereum.
4. Tour of how the DApp code works - all text stored in IPFS, and it's hash is stored in the contract.
5. Show how we can also get/set text in IPFS using EmbarkJS in the console.
6. (Quickly edit the IPFS hash validation in the contract so it fails)
8. Show failing transaction and debug in Embark console
9. Debug the failing transaction in Cockpit
10. Stop the debug session.
11. Edit the contract so that the tx will work 
12. Note automatic build and deploy
13. Re-run the DApp tx
14. Run DApp unit tests
15. Deploy to Ropsten
	1. `Ctrl+c` to kill Embark
	2. `embark blockchain testnet`
		1. In the logs, notice how Embark creates an account for us
		2. Get some Ropsten ETH from [faucet](https://faucet.ropsten.be/) using the created account
		3. In a new terminal, run embark testnet with `embark run testnet --nodashboard --nobrowser`
16. Load the DApp (http://localhost:8000) and show that we can interact with our contract on Ropsten using the account that is unlocked by the light client.
17. Enable the metamask extension, and show how we can interact using our metamask account, instead of the light client account.
18. Load Cockpit and show how txs and blocks are live. Show that we can interact with our contracts on Ropsten.
19. In a new terminal, upload the DApp to IPFS: `embark upload testnet`
