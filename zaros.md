


## Zaros a perpetuals DEX 
* Zaros utilize cross-margin trading accounts which means that the total available fund or (equity) in a users account can be used to support all open positions simultaneously.
* Users can use over 15 tokens as margin collateral and have the option to create multiple trading accounts as needed.
* Zaros connects liquid Re(staking) tokens (LSTs & LRTs) with perpetual futures
* users have the ability to trade with leverage of up to 100x
  
## Leverage trade, FX and Commodities
* with Boosted (Re)staking vaults you can supercharge your LRTs and LSRs yields by earning points, additional ETH from Zaro's trading fees, all through ZLP Vaults.
  
## ZLP Vaults - Market Making Vaults
* this is the smart contract takes the underlying collateral provided by the lp's, and lock it to increase the caps  of Zaros perpetual future markets 
* [Question]: how do you prevent 
* [Question]: how is the pricefeed gotten? [answer] chainlink
* LPs earn fees paid by the traders, in exchange for lending their collateral
* [Question]: how is the fee calculated ? 

* I think the DAO is responsible for spinning up new ZLP Vaults. 


  
* you can become market maker of the zero protocol by providing liquidity to any of the ZLP Vaults listed(meaning that there will be more than 1 LP vault in this case)
* a liquidity provider earns collateral's yield and rewards like EigenLayer Points, while also earning ETH real yield and zPoints 

## Create Multiple Trading Account
* traders can create as many trading accounts on Zaros, enabling them to implement different margin strategies. 

## Skew and Open Interest Caps
* zeros markets have skew caps and open interest cap
* `Skew:` in trading refers to how people thinks the price of an asset will move in the future
* `implied volatility(IV):` this is like the measure of how much people expect the price of an asset to move up or down
* `High IV`: means people thinks the price will move a lot
* `Low IV`: means they think it will stay pretty stable
* `Out-of-money (OTM) Options:` these are options that currently wont make any money if you use them right now, for example an OPM call options might be buying a stock at $120 when the stock is currently at $100 
* Skew is the diffrence in these expectation (IV) for options that bet on the price going up (`call option`) vs going down (`put options`)
* `positive Skew`: poeple thinks there is a bigger chance the price will go up alot
* `negative Skew`: people thinks there's a big chance the price will go down alot
* `Skew caps`: this refers to limits or controls placed on how much the expected price movement (volatility) can differ between optionsbetting on the price going up (calls) and those betting on the price going down (puts)

* `Open interest cap`:this are limits on how many contracts (like options or futures) can be held 
* `Open interest`: this is the total number of these contracts that are currently active
* `caps`: these are the maximum limits set to prevent anyone from holding too many of these contracts

* the protocols also allow trading of new or risky type of token
* [Question]: how do you account of tokens with less than 18 decimals in this case?
* [Question]: how do you account for weird erc20 tokens like erc777, rebasing tokens etc
* [Question]: what kind of problem should occurs in this case when traders buy or sell assets?

## Stablecoin
* `USDz` is the protocol overcollaterized stablecoin that is native to the Zeros ecosystem. meaning that is specifically designed to be used within the Zeros platform, likely to be used for some transaction or activities(`ps:i'm not sure`)
* desinged to serve as a stable and reliable source of value within the protocol, enabling leverage trading meaning that you can borrow money to trade more than you actually have , for example with 10x leverage you can trade $10,000 worth of assets with just $1000.
* `USDz` is primally used for paying traders's position
  
* `[Example]`:Imagine you made a profit trading on Zaros. You get some USDz minted and added to your account. If you want, you can swap this USDz for other assets like Ether or Bitcoin, as long as these assets are in the ZLP Vaults and worth $1. The system uses real-time price information to make sure you get the correct amount. The USDz is backed by more assets than necessary, so you can trust its value to stay stable.
* so these LSTs that are deposited by LPs serves as the backing for the market liquidity, hence USDz
* [Question]: since USDz is been backed by REstaking tokens, how do it stay stable? maintaining $1 since the tokens that do back it are not stable
* [Question]: how can i make this USDz to be unstable?

* Upon closing a position, the trader receives USDz, which can be converted (burned) for any available collateral from a ZLP Vault using a low-latency oracle.

* USDz is paid out to profitable positions, and is accounted as debt by the CreditBranch
* `Example`:Imagine you made a successful trade and earned some profit. The Zaros platform pays you in USDz, the stablecoin used within the system. The CreditBranch, which manages credit, records this payment as a debt. This is like the system saying, "We have given you this much USDz as your profit, and we are keeping track of it as an amount we owe to balance our books."
* [Question]: what if an experienced group of traders entered the protocol in the begining  and made away with a huge pool balance, that means LPs will be unable to unstake and take there funds, 

## Tree Proxy Pattern 
* simplified terminology compared to EIP-2535[Diamond-proxy]
* `EIP-7201` compatible: meaning that it follow some certain rules to be able to work with other system that folllow such rules
* composability over inheritance
* upgradeability

| Tree Proxy Pattern Vocabulary | Common Name                 |
| ----------------------------- | --------------------------- |
| Root                          | Proxy                       |
| Branch                        | Implementation (Module)     |
| Leaf                          | Functions and Storage       |
| LookupBranch                  | List of Delegated Functions |
| LookupTable                   | Namespace's Lookup          |
| RootUpgrade                   | Upgrade                     |


`Leaf` - Denotes functions, the smallest unit within the architecture, thoroughly unit tested to ensure reliability.

`Branch` - Represents modules, a collection of functionalities grouped by logic or purpose.

`Root (Proxy)` - Acts as the entry point to the architecture, channeling requests to appropriate modules.

## Zaro's Core
* they are supported by 3 key external actors
* `Chainlink`: supplys Data feeds, darta streams and keepers
* `AccountNFT`: base on the ERC721, represents a traders account within the ecosystem, enabling traders to manage multiple accounts, each tailored to diffrent trading strategy
* `USDz`

## Liquid Providers
* deposits their LSTs(liquid staking tokens) and LRTs(liquid (Re)staking tokens) into ZLP vaults earning 70% of the perpetual trading fees generated
* designed to support Liquid (Re)Staking tokens like `Lido’s $wstETH and Etherfi’s $weETH`
* certain vaults may also rrward LPs with zPoints


## Zaros Perps Engine: Overview

## Core Components
* **Branches**
* `LookupBranch.sol` - Manages the namespace's Lookup operations across the system.
* `SettlementBranch.sol` - Handles all settlement processes.
* `PerpsAccountBranch.sol` - Oversees accounts and their interactions within the platform.
* `PerpMarketBranch.sol` - Controls the creation and management of perpetual markets.
* `OrderBranch.sol` - Facilitates order management and execution.
* `LiquidationBranch.sol` - Executes liquidation procedures for undercollateralized positions.
* `GlobalConfigurationBranch.sol` - Manages global settings and configurations.
* `UpgradeBranch.sol` - List of delegated functions.


* **Leaves**
* `Branch.sol` - The base contract for all branches, defining common behaviors and functionalities.
* `LookupTable.sol` - A utility contract for efficient data lookup and retrieval.
* `SettlementConfiguration.sol` - Defines parameters and settings for the settlement process.
* `MarketOrder.sol` - Represents market orders within the system.
* `Position.sol` - Manages traders' positions.
* `PerpMarket.sol` - Details the properties and behaviors of a perpetual market.
* `MarketConfiguration.sol` - Specifies market-specific settings and configurations.
* `OrderFees.sol` - Governs the fee structure for order processing.
* `MarginCollateralConfiguration.sol` - Outlines the collateral requirements and margin settings.
* `PerpsAccount.sol` - Contains account-specific data and logic.
* `GlobalConfiguration.sol` - Holds the global settings applicable across the Zaros platform.
* `RootUpgrade.sol` - Manages upgrades to the root (proxy) to introduce new functionalities or improvements.

* **Root**
`Perps Engine` - The core engine that powers the Zaros Perpetual Swaps ecosystem.

## cross margin and NFT based trading account
* `Cross-Margin:` Instead of keeping separate margin balances for each trade, all trades share a common margin balance. 
* `Multi-Account System:` Traders can manage multiple trading accounts within one main account.
* `ERC-721 NFTs`: Each trading account is represented by a unique ERC-721 token, a type of non-fungible token (NFT) that can be managed within a single Ethereum Virtual Machine (EVM) wallet.

## Overview of Zaros Market Engine
* the engine supported by modular architecture, including critical components such as

* `FeeBranch.sol:`
* Function: Manages transaction fees within the system.
* Role: Ensures that fees are calculated and processed correctly for all market activities.
  
* `CreditBranch.sol:`
* Function: Handles credit operations, such as issuing and managing credit to traders.
* Role: Provides and controls the credit available to users, ensuring smooth trading operations.
  
* `CollateralBranch.sol:`
* Function: Manages collateral, which is the assets that traders deposit to secure their trades.
* Role: Ensures that collateral is handled correctly, maintaining the security and integrity of the market.
  
* `ZLPBranch.sol:`
* Function: Manages the ZLP (Zaros Liquidity Pool) operations.
* Role: Oversees the liquidity pool, ensuring there is enough liquidity to support trading activities and settlements.


# Perpetuals DEX

* **Introduction**, In trading
* `going long, or buying or longing trade`, is a strategy where traders purchase an asset with the expectation that its value will increase over time, while
* `going short, or selling short or shorting trade`, is a strategy where traders sell an asset with the hope that its value will decrease in the future. Going short is often employed by traders who believe that a particular asset is overvalued and will eventually decline in price.

* **Oracle and Keepers**
* Zaros uses Chainlink Data Feeds and Data Streams, which are instrumental in connecting Zaros smart contracts with aggregated pricing data 
* `Chainlink Data Feeds`: Facilitate secure, transparent access to aggregated pricing data, crucial for the dependability of Zaros Perpetuals DEX.
* `Chainlink Data Streams`: Offer real-time, low-latency market data delivery off-chain, which can be verified onchain, enabling Zaros Perpetuals DEX to match the performance of centralized exchanges without sacrificing transparency or decentralization.

* **Key functions of Keepers**
* `Liquidation Process`: Keepers continuously monitor positions to ensure they meet maintenance margin requirements, initiating liquidations proactively to uphold market stability. In this case it's used an eventTrigger keeper.
* `Market Orders`: These keepers, activated by zaros custom logic, are tasked with executing market orders by opening and closing them.

### Chains
* Zaros will initially launch on Arbitrum, with plans for deployment on Monad following its release.

### Available Markets
Cryptocurrency Market-Pairs
 | Market   | Description            |
 | -------- | ---------------------- |
 | BTCUSD   | Bitcoin/US Dollar      |
 | ETHUSD   | Ethereum/US Dollar     |
 | LINKUSD  | LINK/US Dollar         |
 | ARBUSD   | Arbitrum/US Dollar     |
 | AAVEUSD  | AAVE/US Dollar         |
 | BNBUSD   | Binance Coin/US Dollar |
 | SOLUSD   | Solana/US Dollar       |
 | LTCUSD   | Litecoin/US Dollar     |
 | DOGEUSD  | Doge/US Dollar         |
 | UNIUSD   | Uniswap/US Dollar      |
 | XRPUSD   | Ripple/US Dollar       |
 | OPUSD    | Optimism/US Dollar     |
 | MATICUSD | Matic/US Dollar        |
 | ATOMUSD  | Atom/US Dollar         |
 | FTMUSD   | Fantom/US Dollar       |
 


| Commodity | Market                            |
| --------- | --------------------------------- |
| XAUUSD    | Gold/US Dollar                    |
| WTIUSD    | West Texas Intermediate/US Dollar |
| HGGUSD    | Copper/US Dollar                  |


| Currency Pair | Description             |
| ------------- | ----------------------- |
| EURUSD        | Euro/US Dollar          |
| GBPUSD        | British Pound/US Dollar |
| JPYUSD        | Japanese Yen/US Dollar  |



### Zaros setup
* account are created using just email or apple ID

### Account Abstraction implementation
* By implementing Account Abstraction, transactions can be batched and there is no longer a need for the network's native token to pay fees
* this means that transaction will be created batch by batch and be processed as batch also you can use any token you want to pay the fee not only native tokens like Ethereum
  
* [Example]: Imagine you want to send money to several friends and pay for a service on the blockchain. Without account abstraction, you would do each transaction one by one and pay a fee for each, using the blockchain's main token. With account abstraction:
* You batch all these actions into one transaction.
* You pay one fee for the entire batch.
* You use any token you have, not just the blockchain’s main token.

* Account Abstraction also enables users to sign transactions without the need for a private key or seed phrase

### Collaterals
* They are the tokens traders deposit in other to be able to perticipate in the perp future
* This below is the list of collateral that can be used in Zaros

| Collateral | Name                  |
| ---------- | --------------------- |
| USDC       | USD Coin              |
| USDz       | USDz                  |
| AAVE       | Aave                  |
| ARB        | Arbitrum              |
| ETH        | Ethereum              |
| IMX        | Immutable X           |
| INJ        | Injective             |
| LDO        | Lido                  |
| LINK       | ChainLink             |
| TIA        | Celestia              |
| USDC.e     | USD Coin on Avalanche |
| USDT       | Tether USDC           |
| wBTC       | Wrapped Bitcoin       |
| weETH      | Wrapped Ether         |
| wstETH     | Wrapped stETH         |


## Funding Rate

### Zaros Funding Mechanism & Price Marking
* To calculate the premium discount, we utilize the following formula:
* premiumDiscount = markPrice / indexPrice
* This ratio provides insight into the relationship between the mark price and the index price.
  
## Funding rate calculation
* `Funding Rate`: This is a fee paid between buyers and sellers of a perpetual futures contract to keep the contract price close to the actual market price of the underlying asset. Think of the funding rate as a tool to keep the contract price close to the real price of the asset.
* `Premium Discount`: The difference between the price of the perpetual contract and the price of the underlying asset.
* `Interest Rate:` A fixed rate used to help calculate the funding rate.
* `Clamp Range:` A range of acceptable values for the funding rate adjustment. If the calculated funding rate is outside this range, special rules apply.

### Scenario 1: Outside the Clamp Range
* [Example]
* `Interest Rate:` Let’s say the interest rate is 5%.
* `Initial Calculation`: Using the formula, we try to adjust the funding rate.
* `Outside Clamp Range`: If the result is too high or too low, we just set the funding rate to 5% to keep it stable.

### Scenario 2: Within the Clamp Range
* For funding rate calculations within the acceptable range, we use a clamp function to ensure the rate stays between -0.05% and 0.05%. This keeps the funding rate stable and prevents extreme values. The formula fundingRate = premiumDiscount + clamp((interestRate - premiumDiscount), -0.05%, 0.05%) ensures that adjustments are made within safe limits.

* `Clamp Function`: This function ensures that the difference between the interest rate and the premium discount stays within the clamp range of -0.05% to 0.05%.

* `Adjustment Calculation:`
* `Formula`: fundingRate = premiumDiscount + clamp((interestRate - premiumDiscount), -0.05%, 0.05%)
* `Clamp Function`: If the value of (interestRate - premiumDiscount) is outside the range of -0.05% to 0.05%, it is adjusted (clamped) to stay within this range.
  
* [Example]
* `Interest Rate`: Suppose the interest rate is 5%.
* `Premium Discount`: Let’s say the premium discount is 4.95%.
* [Calculation:]
Compute (interestRate - premiumDiscount): 5% - 4.95% = 0.05%.
* `Clamp Function`: Since 0.05% is within the clamp range, no adjustment is needed.
Add the premium discount to the clamped value: 4.95% + 0.05% = 5%.

### Interest Rate Determination
The interest rate is a key component in calculating the funding rate for perpetual futures contracts. It is derived from the difference between the 8-hour TWAP of the quote and base asset lending rates, divided by the number of funding times per day. This rate helps maintain the contract price close to the underlying asset price.

* **Understanding the Components**
* `Interest Rate`: This rate is crucial for calculating the funding rate in perpetual futures contracts.
* `Funding Interval`: The period between each funding payment (typically 1 hour).
* `Funding Times Per Day`: How often funding occurs in a day, typically 3 times.
* `Interest Rate Formula`The interest rate is determined using the following formula:

interestRate = interestQuote − interestBase / fundingTimesPerDay
​
* Where:

* `interestQuote:` The 8-hour Time-Weighted Average Price (TWAP) of the quote asset's lending rate.
* `interestBase`: The 8-hour TWAP of the base asset's lending rate.
* `fundingTimesPerDay`: How often funding occurs per day. Typically, this is 3 times.
  
* [Key-Terms]
* `Quote Asset`: The asset you are trading into (e.g., USDT in a BTC/USDT pair).
* ` Base Asset`: The asset you are trading from (e.g., BTC in a BTC/USDT pair).
* `TWAP (Time-Weighted Average Price)`: An average price over a specified time period, giving equal weight to each price point.
  
* Example Calculation
Let's break down a hypothetical example:

* `interestQuote:` Suppose the 8-hour TWAP of the quote asset's lending rate is 0.03%.
* `interestBase:` Suppose the 8-hour TWAP of the base asset's lending rate is 0.02%.
* `fundingTimesPerDay`: Typically, funding occurs 3 times per day.
  
* interestRate = 0.03% − 0.02% / 3 = 0.01% / 3 ≈ 0.0033%

* This calculated interest rate (approximately 0.0033%) will then be used in the funding rate formula.

* Funding Interval and Funding Times Per Day
* `Funding Interval`: Typically 1 hour.
* `Funding Times Per Day:` fundingTimesPerDay = 24hours / 1hour = 24

* However, in the context of our formula where funding occurs 3 times per day, this value is often set to 3 to simplify the calculations.

* **Simplified Explanation**
* `Interest Rate Calculation`: We determine the interest rate by subtracting the base asset's lending rate from the quote asset's lending rate, then dividing by the number of funding times per day.
* `TWAP:` We use the average lending rates over an 8-hour period for both assets.
* `Typical Values`: Usually, the interest rate is around 0.01% or 1 basis point (bps).

### Understanding the Price Marking Mechanism of Zaros
* Key Concepts
* `Skew Scale`: Adjusts market positions based on desired price impact.
* `Desired Price Impact`: The goal for how much Zaros wants to influence the market price.
* `Impact Notional`: Standard value used to gauge trading impact, typically $100,000.
* `Price Impact Premium:` A factor set by the risk team to adjust the price impact based on market conditions.
  
* Simplified Explanation
* `Skew Scale`: Think of this as a tool Zaros uses to make sure its trades change the market price just the right amount.

* Calculation: Skew Scale = Impact Notional / zaros.Desired Price Impact

* Purpose: Ensures trades are aligned with Zaros’s strategy.

* `Desired Price Impact`: This is Zaros's goal for how much it wants to change the market price with its trades.
* `Components`: It's calculated by multiplying the `priceImpactPremium` by the `cEXPriceImpact`.

* The `priceImpactPremium` is adjusted by the risk team based on market liquidity and other conditions
  
* `Impact Notional`: A standard measure used to keep trading impact consistent, typically set at $100,000.
* Purpose: Helps Zaros adjust its strategy based on different market situations.
  
* `Price Impact Premium`: This is a coefficient set by Zaros's risk team.
* `Role`: Adjusts how much trades impact the price based on how liquid (active) the market is and other factors.
* `Importance:` Helps Zaros decide how aggressive or cautious to be with its trades.
  
* [Example]
* Skew Scale Calculation:
* Suppose Zaros wants a Desired Price Impact of 2% and the Impact Notional is $100,000.
  
* Skew Scale = 100,000 / 0.02  = 5,000,000.
  
* This means Zaros will use this scale to adjust its trades to achieve the desired price impact.
Desired Price Impact:

* `Price Impact Premium:` Let's say this is set to 1.5 by the risk team.
* `CEX Price Impact`: Suppose this is 1.33%.
* `Desired Price Impact` = 1.5 * 1.33% = 2%.


## Liquidation

* Liquidation Criteria
* A user's position is subject to liquidation if their Account Value drops below the RequiredMaintenanceMargin. This process is vigilant, with Keepers tasked to continuously monitor positions against maintenance margin requirements. They utilize an eventTrigger mechanism to initiate liquidations

* `Formula`: isLiquidatable = requiredMM + liquidationFeeUsd ≥ marginBalanceUsd
* Note: requiredMM stands for the requiredMaintenanceMargin

* [Example]
* `Required Maintenance Margin (requiredMM):` Let’s say you need $1,000 to maintain your position.
* `Liquidation Fee (liquidationFeeUsd):` Suppose there is a $50 fee for liquidation.
* `Margin Balance (marginBalanceUsd):` Your account currently has $900.
* Using the formula:
* isLiquidatable = $1,000 (requiredMM) + $50 (liquidationFeeUsd) ≥ $900 (marginBalanceUsd)

* Since $1,050 is greater than $900, your position would be liquidated.

* `LiquidationBranch.sol`:This is the contract that handles the liquidation process


## Earn (Re)Staking dApp
* **What Are Boosted (Re)Staking Vaults?**
* Boosted (Re)Staking Vaults, also known as boosted ZLP Vaults, are special types of vaults that are designed to help liquidity providers (LPs) earn more rewards than they would with standard vaults.

* **Key Features**
* `Stacking Rewards`:
Each vault offers a specific number of rewards, which are easy to identify (e.g., dual rewards, triple rewards, quadruple rewards).
This helps investors quickly see how much they can potentially earn from a particular vault.

* `Comprehensive Yield Generation`:
* Participants earn money from various sources:
* `Trading Fees`: Fees collected from trading activities on the Perps DEX.
* `zPoints`: Points that can be earned and possibly converted into rewards.
* `Other Incentives`: Additional rewards from partnerships and integrations with other platforms.
  
* [Simplified-Explanation]
* `Boosted Rewards`: These vaults are like special savings accounts that offer more rewards compared to regular ones. The number of rewards is clearly marked (e.g., double, triple) so you know what to expect.
* `Multiple Income Streams`: By participating in these vaults, you can earn money from different sources, such as trading fees, reward points, and extra bonuses from partnerships.

### Integration
The Earn dApp allows users to earn rewards by integrating with a wide range of projects offering Liquid Staking Tokens and Liquid Reward Tokens, including some of the most prominent ones in the industry.

| Project | Token  | Type |
| ------- | ------ | ---- |
| Lido    | wstETH | LST  |
| EtherFi | weETH  | LRT  |
| Bedrock | uniETH | LRT  |
| Dinero  | pxETH  | LST  |
|         | ynETH  |      |


## Where to get Faucet
If is your first time in Arbitrum Sepolia Network you will need Faucet. you can try to get in https://www.alchemy.com/faucets/arbitrum-sepolia or https://faucet.quicknode.com/arbitrum/sepolia


## INVARIANTS
1. 
​

## More Questions
1. How can a position becomes insolvent?
2. what happens when a position becomes insolvent
3. how is that handle?


## how to avoid stepwise increase in perpetual trading
* instead of the value of the market token or how you are giving people creadit for depositing it liquidity, the value of their deposit, you just have to factor in the current pnl of the trader

## findings
@audit USDC is been used as a collateral , meaning that a user can choose to do some things knowing that they would get blacklisted and then enter a position then before the position can be liquidated the usdc address will get blacklisted , this will cause the liquidation to revert, accuring dept to the protocol

