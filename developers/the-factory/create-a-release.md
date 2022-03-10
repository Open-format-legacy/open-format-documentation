# Create a release

To create a release you need to deploy a version of our [Factory contract](https://github.com/simpleweb/music-factory-contracts/tree/main/contracts). You can start with our [whitelabel-starter](https://github.com/simpleweb/whitelabel-starter). Whitelabel has chosen to use the [Polygon Network](https://polygon.technology) due to its speed, reliability and low transactions fees. For this guide we're using [Polygon Mumbai](https://mumbai.polygonscan.com), which is Polygon's test network. **Polygon is built on top of the ethereum blockchain**.

### Prerequisites&#x20;

* **NodeJS installed** - [https://nodejs.org/en/](https://nodejs.org/en/)
* **A basic understanding of how the ethereum blockchain works**
* **A basic understanding of Javascript**

#### Ethereum wallet

* This example requires an ethereum wallet. We recommend using [Metamask](https://metamask.io). Once you've created a wallet, you will need to do two things:
  * Get the private key. Read [this guide](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key) to find out how get your private key from Metamask.
  * Add some MATIC Token from the [Polygon Faucet](https://faucet.polygon.technology). Every transaction on the ethereum blockchain costs [gas](https://www.youtube.com/watch?v=hQ78FVSv-vs). MATIC Token is the network token for the Polygon Network. We need some MATIC tokens in our wallet to cover the gas fees for the deployment transaction in this guide.

#### **Ethereum Node RPC Url**

* We need a way to interact with the ethereum blockchain. This can be done through a node service. We recommend [Alchemy](https://www.alchemy.com). It's completely free to use for development purposes. Once you've create an account, navigate to the dashboard and click **Create App.**  Create an app with the same details as in the image below. It's important that the chain is **Polygon** and the network is **Polygon Mumbai.**

![](<../../.gitbook/assets/Screenshot 2022-03-09 at 15.27.29.png>)

### Project Setup

1. `git clone` [`https://github.com/simpleweb/whitelabel-starter.git`](https://github.com/simpleweb/whitelabel-starter.git)``
2. `cd whitelabel-starter`
3. `yarn install`` `**`OR`**` ``npm install`
4. `cp .env.example > .env`&#x20;
5. Open the project in your favourite code editor. We recommend [Visual Studio Code](https://code.visualstudio.com).

### Environment Setup

#### `RPC_URL`&#x20;

The `RPC_URL` is how we're going to interact with the ethereum blockchain. Once you've [created your App in Alchemy](create-a-release.md#ethereum-node-rpc-url), click on [**View Key**](https://github.com/simpleweb/whitelabel-starter)**.**  Copy the **HTTP** url and add it to your .env:

`RPC_URL=COPIED_HTTP_URL`

![](<../../.gitbook/assets/Screenshot 2022-03-09 at 15.36.25.png>)

#### `WALLET_PRIVATE_KEY`

Every transaction on the ethereum blockchain needs be signed by a wallet. In the same way you need to approve transactions when spending money on your credit card. Add your wallet's private key to your .env:

`WALLET_PRIVATE_KEY=b5cD4...`

### Code

Now that your project and environment is correctly setup, we can start writing some code. Firstly, create an **index.js** file in the root of the whitelabel-starter project. All the necessary packages have already been added and installed.



First we need to import all the required packages and files.

```
// configure dotenv package so it can read the RPC_URL and WALLET_PRIVATE_KEY from your .env
require("dotenv").config();

// import ethers.js
const ethers = require("ethers");

// import the Factory contract ABI
const FactoryContract = require("./abi/theFactory.json");
```

Next we need to create our function to deploy the contract.

```
async function main() {
  const RPC_URL = process.env.RPC_URL;
  const WALLET_PRIVATE_KEY = process.env.WALLET_PRIVATE_KEY;

  // We create a new provider. This is used to interact with the blockchain
  const provider = new ethers.providers.JsonRpcProvider(RPC_URL);

  // We need to create an instance of a wallet using our WALLET_PRIVATE_KEY
  const wallet = new ethers.Wallet(WALLET_PRIVATE_KEY, provider);

  console.log({ wallet });

  // This is simply connecting the wallet above and making it the signer of the transaction
  const account = wallet.connect(provider);

  // Now we use the Factory ABI, Bytecode and account to create an instance of the contract
  const factoryContract = new ethers.ContractFactory(
    FactoryContract.abi,
    FactoryContract.bytecode,
    account
  );

  // Here we call the deploy function on the contract and pass through the required values
  const contract = await factoryContract.deploy(
    [account.address], // Payees
    [100], // Shares
    ethers.utils.parseEther("1"), // Sale Price
    "TRACK", // Name
    "SONG", // Symbol
    100, // Quantity
    250, // Royalties percentage
    "ipfs://" // Metadata URL
  );

  console.log("Transaction Pending...");

  // The transation has been submitted to the blockchain. We now to wait for it to be confirmed
  const receipt = await contract.deployTransaction.wait();

  console.log({ transactionHash: receipt.transactionHash, receipt });
}

main();
```

Save the file and run it. To run the file open up the terminal (in the project directory) and type `node index.js`. If everything is working as expected you should see your wallet object logged in the console and a message saying `Transaction Pending...`. Wait for a minute or so and you should see another log with the `transactionHash`. Copy the `transactionHash` and visit the [PolygonScan (Mumbai) explorer](https://mumbai.polygonscan.com). Enter the `transactionHash` in the search box. Should see something like this:

![](<../../.gitbook/assets/Screenshot 2022-03-10 at 09.39.39.png>)

\
Congratulations! You've created your first release! Now we can [find your release in the subgraph](../the-subgraph/read-from-the-subgraph.md). \
