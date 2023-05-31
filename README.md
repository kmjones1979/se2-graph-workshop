# Scaffold-ETH 2 x The Graph Workshop

### Todays Agenda!

1. Setup Scaffold-ETH 2
2. Demo of Scaffold-ETH 2
3. Solidity by Example
4. Install Metamask
5. SpeedRunEthereum
6. 🚩 Challenge 0: 🎟 Simple NFT Example
7. Setup Scaffold-ETH 2 branch with The Graph Integration
8. Demo of The Graph integration
9. Extra Credit - Adding Additional Events
10. Extra Extra Credit - Querying from an Application

### Requirements

Before you begin, you need to install the following tools:

- [Node (v18 LTS)](https://nodejs.org/en/download/)
- Yarn ([v1](https://classic.yarnpkg.com/en/docs/install/) or [v2+](https://yarnpkg.com/getting-started/install))
- [Git](https://git-scm.com/downloads)
- [Docker](https://docs.docker.com/get-docker/)

## 1. Setup Scaffold-ETH 2

> To get started with Scaffold-ETH 2, follow the steps below:

1. Clone this repo & install dependencies

```
git clone https://github.com/scaffold-eth/scaffold-eth-2.git
cd scaffold-eth-2
yarn install
```

2. Run a local network in the first terminal:

```
yarn chain
```

> This command starts a local Ethereum network using Hardhat. The network runs on your local machine and can be used for testing and development. You can customize the network configuration in `hardhat.config.ts`.

3. On a second terminal, deploy the test contract:

```
yarn deploy
```

> This command deploys a test smart contract to the local network. The contract is located in `packages/hardhat/contracts` and can be modified to suit your needs. The `yarn deploy` command uses the deploy script located in `packages/hardhat/deploy` to deploy the contract to the network. You can also customize the deploy script.

4. On a third terminal, start your NextJS app:

```
yarn start
```

> Visit your app on: `http://localhost:3000`. You can interact with your smart contract using the contract component or the example ui in the frontend. You can tweak the app config in `packages/nextjs/scaffold.config.ts`.

> Run smart contract test with `yarn hardhat:test`

- Edit your smart contract `YourContract.sol` in `packages/hardhat/contracts`
- Edit your frontend in `packages/nextjs/pages`
- Edit your deployment scripts in `packages/hardhat/deploy`

## 2. Demo of Scaffold-ETH 2

> Steps will be added later here...

<pre>


<<<<>>>> 10 Minute BREAK <<<<>>>>


</pre>

## 3. Solidity by Example

- [Solidity by Example](https://solidity-by-example.org/)

1. Incorporate the following variables and functions into your smart contract.

```
    uint public count;

    // Function to get the current count
    function get() public view returns (uint) {
        return count;
    }

    // Function to increment count by 1
    function inc() public {
        count += 1;
    }

    // Function to decrement count by 1
    function dec() public {
        // This function will fail if count = 0
        count -= 1;
    }
```

2. Redploy and test.

## 4. Install Metamask

- [Install Metamask](https://metamask.io/)

## 5. Register on Speed Run Ethereum

- [SpeedRunEthereum](https://speedrunethereum.com/)

## 6. 🚩 Challenge 0: 🎟 Simple NFT Example

- [Challenge 0](https://speedrunethereum.com/challenge/simple-nft-example)

<pre>


<<<<>>>> 10 Minute BREAK <<<<>>>>


</pre>

## 7. Setup Scaffold-ETH 2 build with The Graph Integration

- [👨‍🚀 Build a dApp quick with The Graph and Scaffold-ETH 2 🏗️](https://mirror.xyz/cryptomastery.eth/uGHEHnskoVwX-mWjAiidXfGt6QowCoKl_yX4okwZc0E)

> First, we will start out with a special build of Scaffold-ETH 2 written by Simon from Edge and Node… Thanks Simon! 🫡

```
git clone -b subgraph-package \
  https://github.com/scaffold-eth/scaffold-eth-2.git \
  scaffold-eth-2-subgraph-package
```

> Once you have this checked out on your machine, navigate into the directory and install all of the dependencies using yarn.

```
cd scaffold-eth-2-subgraph-package && \
  yarn install
```

> Next, we will want to start up our local blockchain so that we can eventually deploy and test our smart contracts. Scaffold-ETH 2 comes with Hardhat by default. To spin up the chain just type the following yarn command…

```
yarn chain
```

> You will keep this window up and available so that you can see any output from hardhat console. 🖥️

> Next we are going to spin up our frontend application. Scaffold-ETH 2 comes with NextJS by default and also can be started with a simple yarn command. You will need to open up a new command line and type the following…

```
yarn start
```

> You will also want to keep this window up at all times so that you can debug any code changes you make to NextJS, debug performance or just check that the server is running properly.

> Next, you will want to open up a third window where you can deploy your smart contract, along with some other useful commands found in Scaffold-ETH. To do a deploy you can simply run the following…

```
yarn deploy
```

> You should get a tx along with an address and amount of gas spent on the deploy. ⛽

> If you navigate to http://localhost:3000 you should see the NextJS application. Explore the menus and features of Scaffold-ETH 2! Someone call in an emergency, cause hot damn that is fire! 🔥

## 8. Demo of The Graph Integration

> Now that we have spun up our blockchain, started our frontend application and deployed our smart contract, we can start setting up our subgraph and utilize The Graph!

1. First, navigate into the subgraph directory. ⌨️

```
cd packages/subgraph
```

2. Next, you will want to run the following to clean up any old data. Do this if you need to reset everything.

```
yarn clean-node
```

3. We can now spin up a graph node by running the following command… 🧑‍🚀

```
yarn run-node
```

> This will spin up all the containers for The Graph using docker-compose. You will want to keep this window open at all times so that you can see log output from Docker.

> Note: If you are running Docker Desktop on Mac you might encounter the following errors… If so please checkout this fix below.

```
CRIT Database does not use C locale. Please check the graph-node documentation for how to set up the database locale, error: database collation is `en_US.utf8` but must be `C`, pool: main, shard: primary, component: ConnectionPool thread 'tokio-runtime-worker' panicked at 'Database does not use C locale. Please check the graph-node documentation for how to set up the database locale: database collation is `en_US.utf8` but must be `C`', store/postgres/src/connection_pool.rs:976:13 note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace thread 'main' panicked at 'called `Result::unwrap()` on an `Err` value: JoinError::Panic(...)', /graph-node/store/postgres/src/connection_pool.rs:484:10
```

> To fix this, stop the existing node and clean up the data. 🧹

```
yarn stop-node && yarn clean-node 
```

> Then add the following to the environment section of your docker-compose.yml file.

```
      # workaround for https://github.com/docker/for-mac/issues/6270?
      PGDATA: "/var/lib/postgresql/data"
      POSTGRES_INITDB_ARGS: "-E UTF8 --locale=C"
```

> Then go ahead and start it up again.

```
yarn run-node
```

> As stated before, be sure to keep this window open so that you can see any log output from Docker. 🔎

> Now we can open up a fourth window to finish setting up The Graph. 😅

4. In this forth window we will create our local subgraph! You will only need to do this once.

```
yarn local-create
```

> You should see some output stating your Subgraph has been created along with a log output on your graph-node inside docker.

5. Next we will ship our subgraph! You will need to give your subgraph a version after executing this command. (e.g. 0.0.1).

```
yarn local-ship
```

> This command does the following all in one… 🚀🚀🚀

- Copies the contracts ABI from the hardhat/deployments folder
- Generates the networks.json file
- Generates AssemblyScript types from the subgraph schema and the contract ABIs.
- Compiles and checks the mapping functions.
- … and deploy a local subgraph!

> You should get a build completed output along with the address of your Subgraph endpoint.

```
Build completed: QmYdGWsVSUYTd1dJnqn84kJkDggc2GD9RZWK5xLVEMB9iP

Deployed to http://localhost:8000/subgraphs/name/scaffold-eth/your-contract/graphql

Subgraph endpoints:
Queries (HTTP):     http://localhost:8000/subgraphs/name/scaffold-eth/your-contract
```

> Go ahead and head over to your subgraph endpoint and take a look!

> Here is an example query…

```
  {
    greetings(first: 25, orderBy: createdAt, orderDirection: desc) {
      id
      greeting
      premium
      value
      createdAt
      sender {
        address
        greetingCount
      }
    }
  }
```

> If all is well and you’ve sent a transaction to your smart contract then you will see a similar data output!

> Next up we will dive into a bit more detail on how The Graph works so that as you start adding events to your smart contract you can start indexing and parsing the data you need for your front end application.

## 9. Extra Credit - Adding Additional Events

- [👨‍🚀 Build a dApp quick with The Graph and Scaffold-ETH 2 🏗️](https://mirror.xyz/cryptomastery.eth/uGHEHnskoVwX-mWjAiidXfGt6QowCoKl_yX4okwZc0E)

Scroll down to "Adding Additional Events"

## 10. Extra Extra Credit - Querying from an Application

- [👨‍🚀 Build a dApp quick with The Graph and Scaffold-ETH 2 🏗️](https://mirror.xyz/cryptomastery.eth/uGHEHnskoVwX-mWjAiidXfGt6QowCoKl_yX4okwZc0E)

Scroll down to "Adding Additional Events"

### Resources / More help!

- [Kevin's Social Media Contacts](https://hihello.me/p/6a93d967-1d9f-4818-ae0c-2dc9f86e01aa)
- [Scaffold-ETH Stuff](https://hihello.me/p/b914b816-fb27-4909-9525-16c74c7e7eef)
- [0 to Buidl Guidl](https://lulox.notion.site/0-to-BuidlGuidl-4e1e835ba37c414199fe7a63cb5807e3)
- [Austin's Web2 to Web3 Curriculum](https://github.com/austintgriffith/web2-to-web3-curriculum)
- [Naders Web3 Resources for Developers](https://naderdabit.notion.site/Nader-s-web3-Resources-for-Developers-a200ed2ef21c4d578dc158df2b882c63)
- [Eda's Developer Resources](https://github.com/edakturk14/ethereum-developer-resources)