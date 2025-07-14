# Neon PoCs

1. [Aave V3 flash loan with composability requests to Solana](./contracts/AaveFlashLoan)
2. [MemeLaunchpad with composability requests to Solana](./contracts/MemeLaunchpad)

Neon Dev Bootcamp – Week 2: Memecoin Launchpad on Solana via Neon EVM
Summary of Implementation
This project involved building a fully on-chain memecoin launchpad using Neon EVM's composability features to interact with Solana's Raydium DEX. The launchpad allows users to participate in a token sale governed by a bonding curve, automatically deploys liquidity pools upon reaching funding goals, and locks liquidity while minting an NFT representation of the LP position—all executed from Solidity smart contracts.

Key Components
Bonding Curve Mechanism – Dynamic token pricing based on deposit amounts, with fees collected during the sale phase.

Automated Raydium Pool Deployment – Once the funding threshold is met, the contract constructs and submits Solana instructions via Neon’s precompiles to:

Initialize a Raydium CPMM pool

Lock liquidity tokens

Mint an NFT representing the locked position

Composability in Action – Demonstrated how Solidity can natively trigger Solana program interactions without leaving the EVM environment.

Technical Workflow
Users deposit wrapped SOL (WSOL) to purchase tokens via the bonding curve.

The contract tracks deposits until the funding goal is reached, then autonomously:

Deploys liquidity to Raydium

Locks the LP tokens

Issues an NFT to the launch creator for fee claims

Post-launch, the contract supports fee collection from swap activity.

Outcome
The implementation proved Neon EVM’s ability to seamlessly bridge Ethereum-based smart contracts with Solana’s high-performance DeFi infrastructure. By leveraging precompiles and helper libraries, complex cross-chain operations (like pool creation and liquidity locking) were executed entirely from Solidity, abstracting away Solana’s account model complexities.



### Secret values setup
Secret values (such as private keys) used in tests and scripts should be stored using Hardhat's encrypted keystore file.
This keystore file is specific to this _Hardhat_ project, you can run the following command in the CLI to display the
keystore file path for this _Hardhat_ project:

```shell
npx hardhat keystore path
```

To store encrypted secret values into this project's Hardhat keystore file, run the following commands in the CLI:

```shell
npx hardhat keystore set PRIVATE_KEY_OWNER
```
```shell
npx hardhat keystore set PRIVATE_KEY_SOLANA
```

You will be asked to choose a password (which will be used to encrypt provided secrets) and to enter the secret values
to be encrypted. The keystore password can be added to the `.env` file (as `KEYSTORE_PASSWORD`)  which allows secrets
to be decrypted automatically when running Hardhat tests and scripts. Otherwise, each running Hardhat test and script
will have the CLI prompt a request to enter the keystore password manually.

> [!CAUTION]
> Although it is not recommended (as it involves risks of leaking secrets) it is possible to store plain-text secrets in
`.env` file using the same keys as listed above. When doing so, user will be asked to confirm wanting to use plain-text
secrets found in `.env` file when running Hardhat tests and scripts.
