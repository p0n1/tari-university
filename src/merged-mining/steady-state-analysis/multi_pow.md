# Cost Based Steady-State Analysis of Multiple PoW

- [Aim](#aim)
- [Introduction](#introduction)
	- [Question](#question)
		- [Definition of Control](#definition-of-control)
		- [Hashrate](#hashrate) 
    	- [Mining Pool Difficulty](#mining-pool-difficulty) 	
    - [Game Theory](#game-theory)
- [Attack Vectors](#attack-vectors)
	- [51% attack](#51%-attack)
	- [Selfish Mining](#self-mining)
- [Calculating-the-Cost-of-an-Attack](calculating-the-cost-of-an-attack)
- [Mining-Centralization](#mining-centralisation)
- [Brief look at Myriadcoin](#brief-look-at-myriadcoin)
- [Bitcoin Algorithms](#bitcoin-algorithms)  
	- [Bitcoin Difficulty Algorithm](#bitcoin-difficulty-algorithm)
	- [Bitcoin Blocktime Algorithm](#bitcoin-blocktime-algorithm) 
- [Monero Algorithms](#monero-algorithms)
	- [Monero Difficulty Algorithm](#monero-difficulty-algorithm)
	- [Monero Blocktime Algorithm](#monero-blocktime-algorithm) 
- [Universal Difficulty Algorithm](#universal-difficulty-algorithm)
- [Hypothesis](#hypothesis) 
	- [Assumptions](#assumptions)
- [Implementation](#method)
	- [Scenario 1](#scenario-1)
	- [Scenario 2](#scenario-2)
	- [Scenario 3](#scenario-3)
	- [Scenario 4](#scenario-4)
	- [Scenario 5](#scenario-5)
- [Conclusions and Remarks](#conclusions-and-remarks)
- [Future Work](#future-work)
- [References](#references)
- [Contributors](#contributors)

## Aim 

The aim of this report is to provide an analysis of simulations built that calculate the cost to control the network with variations in the number and type of mining algorithm. The  report will discuss various methods of using multiple PoW algorithms which changes the cost to attack in a variety of ways depending on the configuration. 

## Introduction 

### Question 

**What is the cost to control the network?**

#### Definition of Control 

The use of the word 'control' encompasses the question 'what is the chance of mining $n$ number of blocks in a row to a certain threshold'. 

So to rephrase the question, what is the probability of mining $n$ blocks in a row? Let $n$ = 20, 50, 100 

A series of scenarios have been considered, where multiple mining algorithms with varied hashraties and ease at which it takes to control the network discussed.    

#### Hashrate

Hash rate, similarly known as hash power, is the unit that measures how much power a cryptocurrency network using proof-of-work is consuming to be continuously functional, i.e. how much hash power it is consuming to generate blocks at the normal mean time. [[1]]

##### Mining Pool Difficulty

Each mining pool sets its own difficulty, which is lower than that of the network, to award the participants in accordance with the work they are doing. [[2]] But how does one know what the hashing power is of a particular machine?  It's by the diff of the submitted shares coupled with the time needed to generate said shares.  Higher diff/longer time is eqivalent to lower diff/shorter time.  Hashpower at the pool level is back calculated via diff of shares and time; for the whole Network it is based on solved blocks and time.

#### Game Theory

Game theory is the study of strategic  descision making. This is how many corpotations make decisions while keeping in mind the actions that their competitors will take. Game teory was devised by John Van Neumann and Osker Morgenstern in 1944 and was considered a breakthrough in the study of oligopoly markets. 

Since then the game theory has found a life of its own and has seen widespread implementations in various other technologies and fields. 

##### Block Mining 

Through a series of computations, miners find a block and add it to the blockchain. In Ethereum, adding the block gives the miners a reward nof 5 ether and in bitcoin, the mining reward is 25 BTC (both as of writing). Miners have a lot of power in the blockchain system and if they do choose to cheat for their own personal gain, they can cause havoc in the system. 

To mitigate that, the blockchain uses game theory mechanics to keep the system bulletproof. In order to understand how game theory keeps the miners honest, let’s take a look at another peer-to-peer system which has allowed its users to, time and again, get away with cheating.

Torrenting is one most popular peer to peer systems in the world. While using torrents, users have two roles: downloading and seeding. After downloading a file, they are supposed to share it the network via a method called seeding. However, they get no compensation for seeding the said file and hence more often than not they refuse to do so. Most torrent users are “cheats” because they do not seed their files. They can get away with cheating because the system doesn’t have a “punishment model” the way blockchain does.

How can miners cheat?

- They can include an invalid transaction and give themselves extra coins.
- Add blocks randomly without worrying about Proof of work
- Mine on top of invalid blocks to get more BTC.
- Mine on top of a sub-optimally scoring block.

**Consider the block below:**

![What is Cryptocurrency Game Theory: A Basic introduction](https://blockgeeks.com/wp-content/uploads/2017/08/What-is-Cryptocurrency-Game-Theory-A-Basic-introduction-12-e1502212222697.png)

The blocks in blue are the main chain. Now suppose there is a miner who, in blue block 51, spends 20 bitcoins to get 500 litecoins (hypothetically). And now he wants to create a parallel chain with a new block 51 (red), where in he never did this transaction. So, to simplify what he just did, let’s do a quick recap:

- In blue block 51 spends 20 bitcoins to get 500 litecoins.
- Creates a new chain (fork) from block 50 and in the alternate block 51, he doesn’t do the litecoin transaction.
- In the end, he comes out with his original 20 BTC and 500 new litecoins.

What just happened here is called “double spending.” Obviously now miners can, theoretically, mine on top of the new red chain and keep double spending and mining extra bitcoins. As you can imagine, this can destroy the bitcoin system.

So why don’t miners do that? Is it because they are all good and honorable people? You can’t make a system based on the morals of a person, morality is not quantifiable after all. This is where the true genius of blockchain comes in. The blockchain was designed in a way that it is a self-enforcing Nash Equilibrium. The reason why that happens is that mining has a recursive punishment system.

**The Nash Equilibrium in mining and the punishment system.**

- If a miner creates an invalid block then others won’t mine on top of it because of a rule that has been defined in blockchain mechanics. Any block that is mined on top of an invalid block becomes an invalid block. Using this rule, miners will simply ignore the invalid block and keep on mining on top of the main chain aka the blue chain in the diagram.
- This similar logic stands for sub-optimally scoring block. Look at the diagram again. No miner will want to mine on Red Block 52 because the Blue Block 53 will have a higher score than the red block.

Both of these scenarios get mitigated because miners., as a group will choose the most stable state aka the state with a Nash Equilibrium. Obviously, you can make all the miners mine on the red block and make it the new blockchain, however, the number of miners is so vast that an event like that simply cannot be coordinated (we will talk about this in a bit). As the co-ordination game states, if a majority of the people in the group are not changing their state, the minority will not have any incentive to stay in the new state. Seeing this, why will a miner spend all their computation power and risk ostracization in a futile cause?

**Why will users use the main chain instead of the other chain?**

So, now that we have seen the reason WHY miners will prefer the blue chain…What about the users? In the blockchain game, there are two players, miners, and users. Why will users prefer the blue chain over the red chain? Once again, game theory mechanics come into play.

- The first thing that you need to keep in mind is that cryptocurrency has value is because the people give it value. So, why will a normal user assign a value to coins coming out of the blue chain and not to the coins coming out of the red chain? The reason is simple. The main chain is a Schelling point from the users perspective. They give it value because the main chain seems natural and special to them.
- Bounded Rationality: Another reason why users will value the main chain more is that they are simply used to it. Like bounded rationality states, people will simply opt for the simplest solution every time. Moving through a newer chain needlessly complicates things.

###### What is the Proof Of Work Takeover Problem?

Before we start explaining this, let’s bring back our old diagram again for reference:

![What is Cryptocurrency Game Theory: A Basic introduction](https://blockgeeks.com/wp-content/uploads/2017/08/What-is-Cryptocurrency-Game-Theory-A-Basic-introduction-12-e1502212222697.png)

Vitalik Buterin gave a great example of the Takeover problem and we are going to expand on it. Suppose, someone makes a hypothetical smart contract for an activity. The terms of the contract go like this:

- Any miner can join the activity by sending a very large deposit into the contract.
- The miners must send shares of the partially completed blocks that they have mined into the contract and the contract verifies it and also verifies that you are a miner and that you have sufficient hash power.
- Before 60% of the miners in the system join you can leave anytime you want.
- After 60% of the miners join, you will be bound to the contract until the 20 blocks have been added to the hard fork chain aka the red chain.

Yes, it is indeed very diabolical and you can see the problem that this attack can have. Not only will the new chain grow bigger and longer, since 60% of the entire miners are bound contractually to this new chain this will quickly make the original older chain aka the blue chain irrelevant. This will make double spends all over the place and the value of the currency will fall fast.

Now, you might be asking why miners will join in a takeover?

**Well, let’s see their incentive for joining:**

- The possible reward at the end.
- No risk of joining on their part.

**What is their incentive to follow through with the contract?**

- The huge amount they have deposited in the beginning.
- Once again, the possibility of a great reward.

Theoretically, a takeover like this can end any currency, but this is not that likely to happen because of…You guessed it…. game theory mechanics.

###### Grim Trigger argument to the rescue!

Think of our king argument when we first talked about grim triggers. If a king is killed and usurped, what will stop the new king from getting killed and from this becoming an endless bloody cycle? To stop this from happening, the best course of action is to not kill the original king in the first place.

Similarly, let’s use this logic for blockchains. If a blockchain is taken over and destroyed and the miners are diverted into a new chain, what is stopping that new chain from being taken over by the majority anytime soon? To stop these endless hardforks (aka the red chains in the diagram) from happening, it is important that we don’t do the takeover in the first place.

**However, there are certain places where the Grim Trigger argument does fail, and obviously, there are places where it works pretty spectacularly:**

- The argument fails when the miners are not bound to singular currency. If the miners are working on several currencies, then they can simply group to take over a low-value currency.
- The argument holds up if they are bound and loyal to a particular currency. After all, it is in their direct interest to uphold and maintain the value and legitimacy of the currency.
- If the currency requires specialized ASICs, then the grim trigger argument holds up. If a currency can only be mined by specialized software, then miners will make sure that nothing happens to that particular currency and that it doesn’t lose value. Specialized ASICs after all, can only work for a particular currency. Otherwise, it is useless. Plus, they are expensive.
- The argument doesn’t hold up if the currency can be mined using CPUs. CPUs are not expensive after all, and it can be used to mine other currencies.
- However, if the miners who own the CPUs have a stake in the currency, the argument holds up because they don’t want to lose the stake that they have invested in the currency. This is a sort of proof-of-stake. [[3]]

## Attack Vectors 

### 51% attack

In Proof of Work (PoW) cryptocurrencies, nodes typically are set up to recognize the blockchain with the most blocks (and therefore the most hashing power) as the correct version of history. Miners with > 50% of the network hashing power can take advantage of this by sending funds to one address on the main chain, while sending the same funds to another address on a forked copy of the blockchain that they are silently mining with more hashing power than the main chain.

Since other nodes only know about the main chain, they will see the first transaction as valid, and exchanges, etc will accept this transaction as valid. This malicious node can later release these silently mined blocks, and other nodes will accept this as the new 'correct chain' since it is longer. This will cause the original transaction to effectively dissappear, and nodes will recognize the funds as being sent to the address from the new chain instead. This is known as a 'double spend' attack.

Most bigger cryptocurrencies have sufficient mining capacity behind them, making it extremely expensive to acquire the necessary hardware to pull an attack like this off. Smaller cryptocurrencies have less hashing power securing the network, making it possible to simply rent hashing power from miners on a service like NichHash for a few hours. This significantly reduces the capital costs of an attack.

Recently there have been a number of 51% attacks including against Bitcoin Gold where $18 Million was stolen. [[4]]

#### NiceHash

**NiceHash** is a Slovenian cryptocurrency hash power broker with integrated marketplace that connects sellers of hashing power (miners) with buyers of hashing power using the sharing economy approach.

Buyers select the crypto-currency that they want to mine, a pool on which they want to mine, set the price that they are willing to pay for it, and place the order. Once the order is fulfilled by miners who are running NiceHash Miner on their machines, buyer gets the crypto-currency from the pool. This means that buyers aren't required to run complex mining operations themselves, and there is no capital investment in mining hardware required.''[[5]]

### Selfish Mining 

Selfish mining is a strategy for mining bitcoin in which groups of miners collude to increase their revenue. Bitcoin was invented to decentralise production and distribution of money. But selfish mining can result in centralization of bitcoin mining operations. 

Selfish mining was first proposed by Cornell researchers Sirer and Eyal in 2013. They proved that miners can earn more bitcoins by hiding newly-generated blocks from the main blockchain and creating a separate fork. 

Bitcoin mining relies on miners who solve cryptographically complex puzzles to generate coins. Income from the activity varies because the process is dependent on several factors, from the difficulty of puzzles being solved to electricity costs to hte quality of Internet connections. The bitcoin protocol is configured to reward miners in proportion to their mining output. This ensures that even if miners organise themselves into large pools, the rewards are still dependent on coins produced by individual miners in teh public blockchain. 

But the above scenario assumes that miners will make their newly-generated blocks avaiable on bitcoin's public blockchain. Sirer and Eyal showed that miners can increase their share of overall revenue by hiding new blocks and making them avaiable to systems within their private network. This practice speeds up the discovery process and irons out infrastructure problems related to mining, such as network latency and electricity costs. 

Intiailly, the forked blockchain will be shorter than the public blockchain. However, selfish miners can strategically time their display of new blocks such that honest miners from teh public blockchain abandon their own chain and join the private chain. Subsequently, the private chain mines new blocks within its pool and hides the newly-generated blocks. 

In the meanwhile, the public blockchain continues mining new blocks. The process is repeated until the private blockchain is greater the public one. Now the private chain reveals its blocks again, and miners from the piblic chain abandon their blocks to join the private chain becauuse it is more lucrative. Sirer and Eyal analyzed resources wasted for both chains and determined that selfish miners possessed a competitive advantage over a miner on the public blockchain because their rewards are comparatively greater due to less wastage. 

"Once a selfish mining pool reaches the threshold (of a public blockchain),rational miners will preferentially join selfish miners to reap the higher revenues as compared to other pools," the reproacher write. According to them, the scenario may result in a situation where the selfish mining chain becomes a majority of the public blockchain. This will collapse bitcoin's decentralised nature and a selfish pool manager will control the system. [[6]]

## Calculating the Cost of an Attack 

Using the prices NiceHash lists for different algorithms we are able to calculate how much it would cost to rent enough hashing power to match the current network hashing power for an hour. Nicehash does not have enough hashing power for most larger coins, so we also calculated what percentage of the needed hashing power is available from Nicehash.

Note that the attack cost does not include the block rewards that the miner will receive for mining. In some cases this can be quite significant, and reduce the attack cost by up to 80%. [[4]]

## Mining Centralization 

While the use of proof-of-work (PoW) to solve the double spending problem was Satoshi Nakamoto's key breakthrough with Bitcoin, it is also viewed as one of the weakest points of the system in terms of its potential to be attacked. 

Someone who controls 51% of the computing power pointed at the Bitcoin network is able to choose which transactions can be processed. Someone who controls the majority of the network hashrate can also reorganise the history of network transations in a malicious attempt to spend the same money twice. 

That said, gaining such a large percentage of the network hashrate would be no easy task, seeing as current estimates put the network hashrate at around 70 million terahashes per second. 

During the future of Bitcoin minin gat the Bitcoin 2019 conference, Streng made it clear that he does not view current level of centralization in Bitcoin mining as acceptable. 

While Satoshi's orginal vision of the mining process involved the concept of one vote per computer, that optimistic vision was thrown out rahter early in Bitcoin's history. By 2012, hardware devices built for the specifdic purpose of mining Bitcpin had been developed, and Bitcoin mining was on its way towards specialization and industrialization. 

While Corallo acknowledged miners can gain an advantage by obtaining access to the cheapest electricity in the world, he also pointed out that the availability of cheap power in chunks of 10 to 100 megawatts is somewhat limited and these sorts of setups won’t necessarily account for a large chunk of the overall network hashrate. [[7]] 

Decentralisation of mining power is important to keep control of a coin democratic. [[8]]

## Brief look at MyraidCoin 

Myriadcoin is the first coin to implement five different proof-of-work hashing algorithm in the same coin. These mining algorithms are Scypt, SHA256D, Qubit, Skein and Groestl. This multiple hashing algorith, has the same chance of solving  the next block and has its own independent difficulty while using the smae difficult adjustment method. 

Each algoritm aims for a block generation time of 2.5 minutes. Any existing CPU, Gpu and ASIC miners can be used to mine Myriadcoin. Over the five algorithms, a block should be found on average every 30 seconds. 

Difficult is adjusted after every block. 

Correct implemntation of Mulit-Algo leads to higher secuirty and prevents centralisation of mining power. 

A single algo can only mine six consecutive blocks. 

The process of searching for blocks that meet this proof-of-work threshold is called mining, and the incentives for doing it arise from teh block reward and transaction fees that users wishing to send coins can pay. Miners searching for valid blocks compete with each other on the network. As a consequence, the speed at which a miner can search for outputs from the proof-of-work function will influence the amount of blocks they generate and allow them to collect more rewards. When cryptocurrencies were first developed, the first blocks were generated by programs that use a computer's CPU to do the proof-of-work calculation. It was quickly realised that the properties of the proof-of-work algorithm used could be used to search for valid blocks on Graphics Processing Units (GPUs) by exploiting parellelisation, and that ultimately Application specific integrated circuits (ASICs) could be created to search for blocks. At each stage, the efficiency brought by the new methods rendered old methods obsolete and unable to compete economically, resulting in a centralisation of mining, especially in regions where power (the principle operating expense) is cheaply available.

Myriadcoin was created to address the issues surrounding the proof-of-work system used to allow blocks to be added to the blockchain by allowing multiple types of hardware to be used in the mining process (e.g. CPU, GPU, ASIC). This was accomplished by using multiple different proof-of-work systems to accept blocks, and it was the first coin to use this for this purpose. Currently, it uses five different hashing algorithms as proof of work, with each algorithm aimed to support a different segment of miners:

- SHA256d and Scrypt for ASIC miners (merge minable)
- Skein and Myr-Groestl for GPU miners
- Yescrypt for GPU and CPU miners

This design structure was chosen to make Myriadcoin resistant to ASIC specialization and centralization as the hardware requirements for the algorithms are different. Myriadcoin is also resistant to consensus attacks such as a 51% attack. 51% attacks can occur when an entity controls over 50% of the network's hashrate, which would allow the controller to exclude transactions from the blockchain and reverse transactions created while they maintain control over the network. In Myriadcoin, the possibility for this is reduced as a user would need to control over 50% of the hashing power across multiple algorithms. [[7]]

## Bitcoin Algorithms 

### Bitcoin Difficulty Algorithm

#### Target 

The taget is a 256-bit number that all Bitcoin clients chare. TheSHA_256 hash of a cblock's header must be lower than or equal to the current target for the block to be accepted by the network. The lower the target, the more difficult it is to generate a block. 

Block generation is not a long, set problem, instead it is similar to a lottery. Each hash results in a random number in the range of 0 to 256-bit. If the hash is below the target, then the block has been won, if not, the nonce is incremented and the guessing process continues. 

For reasons of stability and low latency in transactions, the network tries to produce one block every 10 minutes. Every 2016 blocks, every Bitcoin client ompares the actual time it took to generate these blocks with the two week goal and modifies the target by percentage difference. This makes the proof-of-work problem more or less difficult. A single retarget never changes the target by more than a factor of 4 either way to prevent large changes in difficulty. [[9]] https://en.bitcoin.it/wiki/Target

The bitcoin network has a global block difficulty. Valid block must have a hash below this target. Mining pools also have a pool-specific share difficulty setting a lower linit for shares. [[10]],[[11]]

Difficulty changes every 2016 blocks. This is calculated using the following formula:

$$
difficulty = \frac{difficulty1target}{currenttarget}
$$

Where the target is a 256-bit number 

difficulty_1_target can take various values. Traditionally it's a hash function first 32 bits of which are equal to 0 while all the rest are 1 (it is also called diff or pool difficulty). Bitcoin protocol provides target as a type with floating point and limited accuracy. Different Bitcoin clients often determine cryptocurrency difficulty based on this data. 

Difficulty is changed every 2016 blocks based not the time it took to discover 2016 previous blocks will take exactly 2 weeks. If previous 2016 blocks were found in more than two weeks the cryptocurrency mining will be lowered, and if they were mined faster than that it will be raised. The more (or less) time was spent on finding the previous 2016 blocks the more will difficulty be lowered (raised) 

Each block stores a packed representation, termed Bits, of its actual hexadecimal target. 

![Bitcoin mining difficulty chart](https://en.bitcoinwiki.org/upload/en/images/thumb/f/f0/Difficulty.jpg/500px-Difficulty.jpg)

The image above highlights the Bitcoin mining in relation to its price. 

### Bitcoin Blocktime Algorithm

Average time of finding a single block can be calculated using this formula

$$
Time = \frac{difficulty x 2 x 32}{hashrate}
$$

Where 'difficulty' is the current cryptocurrency difficulty level of BTC difficulty network and 'hashrate' is the amount of hashes a miner finds per second. 

## Monero Algorithms

### Monero Difficulty Algorithm

The difficulty adjusts with each block. 

The adjustment algorithm examines 720 prior blocks, starting from 15 blocks ago. 

Of those 720 blocks, the 60 highest and lowest block times are excluded from the analysis, which leaves 600 blocks 

Out of those 600 blocks, the average block time is determined. This average is then used to adjust the difficulty proportionally in order to target a 120 seconds. The unit of difficulty is therefor "hashes". 

When there is a large and sudden change in hashrate, due to the April 6th PoW change, it will therefore take 15+60=75 blocks before the change in hashrate starts to affect the difficulty. The change to difficulty when adjusting to the new hashrate will be gradual, and after 

Calculate network hashrate from current difficulty?

$$
difficulty*120/secondsforblock
$$

(120 here is hard coded value, estimated time for single block)

### Monero Blocktime Algorithm

## "Universal" Difficulty Algorithm 

```
T = target solvetime
n = number of blocks in averaging
r = a dilution aka tempering aka buffering factor
w = a weighting function based on n. It's 1 for all but LWMA. In LWMA it increases from 1 to n from oldest to more recent blocks, giving them more weight.

target = avg(n targets) / r * [(r-1) + sum(n  w*STs)/sum(n w's) / T] 

Less accurately:
difficulty = avg(n Ds) * r / [ (r-1) + sum(n  w*STs)/sum(n w's) / T  ]
 
For clarity, here it is w=1 (no increased weight given to more recent blocks like LWMA and OSS)

target = avg(n targets) / r * [(r-1) + avg(n STs) / T] 

w=1, r=1  Dark Gravity Wave (a Simple Moving Average in deep disguise)
w=1, n=1 for EMA. Larger r means smoother, slower response.
w=1,  r=4 for Digishield, r=2 for Grin
r=1, w = function of n.   LWMA
r = 4, and simple w function.  OSS (like a combination of LWMA and Digishield)
```

[[12]] 



**LWMA Description**
This sets difficulty by estimating current hashrate by the most recent difficulties and solvetimes. It divides the average difficulty by the Linearly Weighted Moving Average (LWMA) of the solvetimes. This gives it more weight to the more recent solvetimes. It is designed for small coin protection against timestamp manipulation and hash attacks. The basic equation is: https://github.com/zawy12/difficulty-algorithms/issues/3

```
next_difficulty = average(Difficulties) * target_solvetime / LWMA(solvetimes)
```



## Tari Algorithm 



## Hypothesis

Scenario 5 best, better than 2 last 3 

### Assumptions 

- Assume the system is in equilibrium 
- Model is steady state
- Define cost that is agnostic of hashrate 
- Hashrate is constant --> Difficulty is constant 

## Implementation

This simulation takes a snapshot of at each second. 



N = 150 blocks (Simulation 150 blocks)

All blocks solved at 1 minute 

t= 60s 

- want to see effect of jumping between hashrate



Monte Carlo Simulation 

$n/1000000 = p$

5? random generator to simulate PoW (allocate hashrate)

### Scenario 1 

We control some fraction of the Tari merge mined hashrate greater than 50%.  

$n$ hashes mining Tari, you need more --> argue the cost is zero  

### Scenario 2 

| Merged Mining | Proof of Work |
| ------------- | ------------- |
| 50%           | 50%           |

- How much of the PoW hashrate do you need to buy control to make above statement true 

### Scenario 3

| Merged Mining | Proof of Work | Proof of Work |
| ------------- | ------------- | ------------- |
| 33%           | 33%           | 33%           |

- Thought as a bad idea, flick between the 2- what would happen as they jump between each PoW

### Scenario 4

| Merged Mining | Merged Mining |
| ------------- | ------------- |
| 50%           | 50%           |

### Scenario 5 

| Merged Mining | Merged Mining | Proof of Work |
| ------------- | ------------- | ------------- |
| 33%           | 33%           | 33%           |

## Conclusions and Remarks

#### Future Work 

Consider the dynamic aspects of the hashrate. Scale for Myriad. 
Is the block time affected by sudden increase in hash rate. This is a dynamic problem. 

These simulations will pave the way for secondary study which would encompass adjusting difficulty dynamically. 

- alpha trimmed mean 
- linearly weighted moving average (LWMA)
- moving median 

### Block timestamp

Each block contains a Unix time timestamp. In addition to serving as a source of variation for the block hash, they also make it more difficult for an adversary to manipulate the block chain.

A timestamp is accepted as valid if it is greater than the median timestamp of previous 11 blocks, and less than the network-adjusted time + 2 hours. "Network-adjusted time" is the median of the timestamps returned by all nodes connected to you. As a result block timestamps are not exactly accurate, and they do not need to be. Block times are accurate only to within an hour or two.

Whenever a node connects to another node, it gets a UTC timestamp from it, and stores its offset from node-local UTC. The network-adjusted time is then the node-local UTC plus the median offset from all connected nodes. Network time is never adjusted more than 70 minutes from local system time, however.

Bitcoin uses an unsigned integer for the timestamp, so the year 2038 problem is delayed for another 68 years. [[12]]

Synchronizing time across machines is difficult due to clock drift and network latencies. The timestamp of a block in Monero is specified by the miner, and the nodes only enforce that the timestamp of a new block is greater than the median of the last 60 blocks. If the nodes used their local clock to enforce timestamp, there would be some risk of disagreement of the validity of the newest block, and therefore a potential chain fork could result. Searching anything related to Bitcoin would be of use too, because identical issues with time are present on that system.

A system could require that the timestamps strictly increase or remain equal, but that could force a miner to put a timestamp that they viewed as incorrect in subsequent blocks. [[13]]



## Notes from Zawy12

What is N, T?

N- the size of an average window in a difficulty algorithm (consodered more importantat than the algorithm- if the algorithm is at least as good as a simple moving average)

Choosing N tries to achieve a balance between a fast response to price (and other causes of hash rate changes) and minimizing accidental variation that accidentally attracts or discourages hashrate with an incorrect difficulty. Smaller N gives faster response but higher variation. The speed at which the difficulty can keep up with price changes is proportional to N*T. The accidental variation in D in block time is proportional to 1/SQRT(N). Approximately, we want to minimize some function like this:

`A/SQRT(N) + B*N*T`
i.e.: variation + slowness

A and B are some unknown scaling factors that relate the relative importance of 1/SQRT(N) and N*T.

- The choice is between wanting a fast speed of response by lower N to keep up with network hashrate changes and not wanting random variation casued by lower B to encourage 



## References 

[[1]] "Explaining Hash Rate or Hash Power in Cryptocurrencies" [online].
Available: <https://coinsutra.com/hash-rate-or-hash-power/>. Date accessed: 2019&#8209;11&#8209;15.

[1]: https://coinsutra.com/hash-rate-or-hash-power/

"Explaining Hash Rash"

[[2]] "Bitcoin Forum- Question about Mining Pool Difficulty" [online].
Available: <https://bitcointalk.org/index.php?topic=5137845.0>. Date accessed: 2019&#8209;11&#8209;15.

[2]:https://bitcointalk.org/index.php?topic=5137845.0

"Bitcoin Forum- Question about Mining Pool Difficulty"

[[3]] "What is Cryptocurrency Game Theory: A Basic Introduction" [online].
Available: <https://blockgeeks.com/guides/cryptocurrency-game-theory/>. Date accessed: 2019&#8209;11&#8209;18.

[3]: https://blockgeeks.com/guides/cryptocurrency-game-theory/

"What is Cryptocurrency Game Theory"

[[4]] "Crypto51" [online].
Available: <https://www.crypto51.app/about.html>. Date accessed: 2019&#8209;11&#8209;1.

[4]: https://www.crypto51.app/about.html

"Crypto51"

[[5]] "NiceHash Wikipedia" [online].
Available: <https://en.wikipedia.org/wiki/NiceHash>. Date accessed: 2019&#8209;11&#8209;18.

[5]: https://en.wikipedia.org/wiki/NiceHash

"NiceHash"

[[6]] "Selfish Mining" [online].
Available: <https://www.investopedia.com/terms/s/selfish-mining.asp>. Date accessed: 2019&#8209;11&#8209;18.

[6]: https://www.investopedia.com/terms/s/selfish-mining.asp

"Selfish Mining"

[[7]] "Bitcoin Mining Centralization is 'Quite Alarming', But A Solution is in the Works" [online].
Available: <https://www.forbes.com/sites/ktorpey/2019/07/28/bitcoin-mining-centralization-is-quite-alarming-but-a-solution-is-in-the-works/#49b8e6dd530b>. Date accessed: 2019&#8209;11&#8209;15.

[7]: https://www.forbes.com/sites/ktorpey/2019/07/28/bitcoin-mining-centralization-is-quite-alarming-but-a-solution-is-in-the-works/#49b8e6dd530b

"Bitcoin Mining"

[[8]] "MyriadCoin Wikipedia" [online].
Available: <https://en.bitcoinwiki.org/wiki/MyriadCoin>. Date accessed: 2019&#8209;11&#8209;13.

[8]: https://en.bitcoinwiki.org/wiki/MyriadCoin

"MyriadCoin Wiki"

[[9]] "Target" [online].
Available: <https://en.bitcoin.it/wiki/Target>. Date accessed: 2019&#8209;11&#8209;19.

[9]: https://en.bitcoin.it/wiki/Target

"Target"

[[10]] "Difficulty Wikipedia" [online].
Available: <https://en.bitcoin.it/wiki/Difficulty>. Date accessed: 2019&#8209;11&#8209;13.

[10]: https://en.bitcoin.it/wiki/Difficulty

"Difficulty Wiki"

[[11]] "Difficulty in Mining Wikipedia" [online].
Available: <https://en.bitcoinwiki.org/wiki/Difficulty_in_Mining>. Date accessed: 2019&#8209;11&#8209;15.

[11]: https://en.bitcoinwiki.org/wiki/Difficulty_in_Mining

"Difficulty in Mining Wiki"

[[12]] "'Universal' Difficulty Algorithm" [online].
Available: <https://github.com/zawy12/difficulty-algorithms/issues/41>. Date accessed: 2019&#8209;11&#8209;18.

[12]: https://github.com/zawy12/difficulty-algorithms/issues/41

"'Universal' Difficulty Algorithm"

[[12]] "'Block timestamp" [online].
Available: https://en.bitcoin.it/wiki/Block_timestamp. Date accessed: 2019&#8209;11&#8209;18.

[12]: https://en.bitcoin.it/wiki/Block_timestamp

"Timestamp Question"

[[13]] "'Block timestamp" [online].
Available: https://monero.stackexchange.com/questions/3300/timestamp-question. Date accessed: 2019&#8209;11&#8209;18.

[13]: https://monero.stackexchange.com/questions/3300/timestamp-question

"Timestamp Question"



## Contributors

- <https://github.com/kevoulee>