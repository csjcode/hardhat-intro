# hardhat-intro

```
mkdir hardhat-intro 
cd hardhat-intro
npm init --yes 
npm install --save-dev hardhat 
```

`npx hardhat`

`npm install --save-dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai
`

Add:
`require("@nomiclabs/hardhat-waffle");`

to hardhat.config.js

continue: hardhat.org/tutorial/writing-and-compiling-contracts.html

"print logging messages and contract variables calling console.log() from your Solidity code. To use it you have to import Hardhat'sconsole.log from your contract code."

`import "hardhat/console.sol";`

Deploy live

Create a deploy script: scripts/deploy.js

```
async function main() {

  const [deployer] = await ethers.getSigners();

  console.log(
    "Deploying contracts with the account:",
    deployer.address
  );
  
  console.log("Account balance:", (await deployer.getBalance()).toString());

  const Token = await ethers.getContractFactory("Token");
  const token = await Token.deploy();

  console.log("Token address:", token.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```
Change network if needed ie. another test network 
`npx hardhat run scripts/deploy.js --network <network-name>`

"In this case, running it without the --network parameter would get the code to run against an embedded instance of Hardhat Network, so the deployment actually gets lost when Hardhat finishes running, but it's still useful to test that our deployment code works" (docs)

Deploy the test code above:
`npx hardhat run scripts/deploy.js`

* "To deploy to a remote network such as mainnet or any testnet, you need to add a network entry to your hardhat.config.js file." (Docs)

* Get test deployment api: https://dashboard.alchemyapi.io/

* Hold secrets in .env file
`npm install dotenv --save`

* Get ether for Ropsten test account
https://faucet.ropsten.be/