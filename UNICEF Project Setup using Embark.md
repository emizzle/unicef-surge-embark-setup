<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UNICEF Project Setup using Embark</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li><a href="#unicef-surge-bangkok---embark-project-setup">UNICEF Surge Bangkok - Embark Project Setup</a>
<ul>
<li><a href="#slides">Slides</a></li>
<li><a href="#hands-on">Hands-on</a></li>
<li><a href="#real-world-example---dreddit">“Real world” example - DReddit</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h1 id="unicef-surge-bangkok---embark-project-setup">UNICEF Surge Bangkok - Embark Project Setup</h1>
<h2 id="slides">Slides</h2>
<ol>
<li>What’s in a DApp - fundamental components</li>
<li>What is Embark</li>
<li>Installation prerequisites - cover any issues with installation</li>
</ol>
<h2 id="hands-on">Hands-on</h2>
<ol>
<li>Run <code>embark</code> without args to see command-specific help output. We will only be covering some of these today</li>
<li>The Embark demo serves as a good starting point to see what kind of functionality Embark offers.</li>
<li>Create an Embark demo app</li>
</ol>
<pre><code>cd ~/temp
rm -rf embark_demo
embark demo
cd embark_demo
</code></pre>
<ol start="4">
<li>
<p>Tour of the DApp structure and components</p>
<ol>
<li>Contracts</li>
<li>App source</li>
<li><code>embark.json</code> - Embark general configuration</li>
<li>Configs
<ol>
<li>Explain what environments are</li>
<li>Blockchain - In development, an account is created for us and loading with tons of ether. In other environments, an account is created with no ether, but it is that account we can use to interact with the blockchain.
<ol>
<li>Quick note on that: when we interact with a blockchain, we are interacting using our account. In traditional web terms, this is how we authenticate ourselves.</li>
</ol>
</li>
<li>Contracts - defines how we deploy our contracts, specify contract args. Explain how contracts need to be deployed on the blockchain, that they are issued an address, and anyone on that chain can interact with the contract with them given that address. When deployed, the constructor of the contract is called, and we pass in arguments for the constructor. This is all set up in the contracts config. For example, SimpleStorage is configured to pass in <code>100</code> as the initial value. We will get this value from the blockchain later.</li>
</ol>
</li>
</ol>
</li>
<li>
<p>Run the DApp with <code>embark run --nodashboard</code></p>
</li>
<li>
<p>Explain dashboard, services started</p>
<ol>
<li><strong>Geth</strong> - local blockchain that we will deploy our contracts to</li>
<li><strong>IPFS</strong> - p2p file sharing node that is used to store assets and text</li>
<li>Contracts compiled and deployed to geth</li>
<li><strong>Pipeline</strong> has run which builds and webpacks all frontend assets for us.</li>
</ol>
</li>
<li>
<p>Tour of the DApp frontend and all the fundamental DApp components covered</p>
<ol>
<li>Run through all the functionality of the demo.</li>
<li>Revisiting our fundamentals:
<ol>
<li><strong>Compute</strong>. We can call our smart contract and transact a value. And read it back.</li>
<li><strong>Storage</strong>. We can store some text in IPFS, and read it back. And we can upload an image, and download it.</li>
<li><strong>Messaging</strong>.  We can listen on a channel, and echo a message.</li>
<li><strong>Name System</strong>.  We can resolve a name from an address.  And we can resolve an address to a name.</li>
</ol>
</li>
</ol>
</li>
<li>
<p>Launch Cockpit and take a tour</p>
<ol>
<li><strong>Dashboard</strong>
<ol>
<li>Services running</li>
<li>Console
<ol>
<li>Replicates Embark’s console output, but also lets up issue commands, same as the CLI dashboard, type <code>help</code> for all commands.</li>
<li>Try out some example commands:
<ol>
<li><code>web3.eth.defaultAccount</code> - this is the account created and unlocked for us by geth. Web3 is our javascript connection to the blockchain. It let’s us connect to a node (in our case, our local node), then issue commands such as querying contracts, sending txs, and creating/unlocking accounts.</li>
<li><code>EmbarkJS.Storage.isAvailable()</code> - a command that checks the status of our configured storage provider which is IPFS in this case</li>
<li><code>SimpleStorage.methods.get().call()</code> - get the initial value stored in our contract</li>
</ol>
</li>
</ol>
</li>
<li>Contracts section - this just shows an overview of which contracts have been deployed for us, with deep-linking in to more contract information, which we can get to via the Explorer tab</li>
</ol>
</li>
<li><strong>Explorer</strong>
<ol>
<li>Dashboard shows an overview of the accounts on our node: you can see the account created for us by Geth and WE ARE RICH! Drilling down in the to the account, we can see detailed account information along with all transactions that have occurred in relation to that account.</li>
<li>Summary view of the blocks created on the chain - drilling down in a block gets us detailed block info and all transaction contained in that block.</li>
<li>Summary view of the transactions on the chain - drilling down in to a transaction get us detailed tx info, with the ability to deep link to associated blocks and accounts in relation to that tx.</li>
</ol>
</li>
<li><strong>Editor</strong> - there is a built in editor that lets you edit any file in your DApp. We are going to get in to this in more detail later.</li>
</ol>
</li>
<li>
<p>Run DApp unit tests (<code>embark test</code>)</p>
</li>
<li>
<p>In a new terminal, upload the DApp to IPFS</p>
<ol>
<li>Explain how the DApp is available on our local node, and it will take a while to propagate to other seeds.</li>
</ol>
</li>
</ol>
<h2 id="real-world-example---dreddit">“Real world” example - DReddit</h2>
<ol>
<li>Make sure the Metamask extension is disabled</li>
<li>Create a new DApp based on the DReddit template<pre><code>embark new dreddit-unicef --template embark-framework/dreddit-unicef-surge-2019
cd dreddit-unicef
git init
git add -A &amp;&amp; git commit -m "first commit"
</code></pre>
</li>
<li>Run the DApp and run CRA, then tour of the DApp functionality
<ol>
<li>Run CRA <code>npm run start</code> and <code>embark run --nodashboard</code>.</li>
<li>While this may not be a real world example, it does show working versions of CRUD operation in Ethereum.</li>
</ol>
</li>
<li>Tour of how the DApp code works - all text stored in IPFS, and it’s hash is stored in the contract.</li>
<li>Show how we can also get/set text in IPFS using EmbarkJS in the console.</li>
<li>(Quickly edit the IPFS hash validation in the contract so it fails)</li>
<li>Show failing transaction and debug in Embark console</li>
<li>Debug the failing transaction in Cockpit</li>
<li>Stop the debug session.</li>
<li>Edit the contract so that the tx will work</li>
<li>Note automatic build and deploy</li>
<li>Re-run the DApp tx</li>
<li>Run DApp unit tests</li>
<li>Deploy to Ropsten
<ol>
<li><code>Ctrl+c</code> to kill Embark</li>
<li><code>embark blockchain testnet</code>
<ol>
<li>In the logs, notice how Embark creates an account for us</li>
<li>Get some Ropsten ETH from <a href="https://faucet.ropsten.be/">faucet</a> using the created account</li>
<li>In a new terminal, run embark testnet with <code>embark run testnet --nodashboard --nobrowser</code></li>
</ol>
</li>
</ol>
</li>
<li>Load the DApp (<a href="http://localhost:8000">http://localhost:8000</a>) and show that we can interact with our contract on Ropsten using the account that is unlocked by the light client.</li>
<li>Enable the metamask extension, and show how we can interact using our metamask account, instead of the light client account.</li>
<li>Load Cockpit and show how txs and blocks are live. Show that we can interact with our contracts on Ropsten.</li>
<li>In a new terminal, upload the DApp to IPFS: <code>embark upload testnet</code></li>
</ol>

    </div>
  </div>
</body>

</html>
