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

When we use the word 'control' what is actual meant is the chance of mining $n$ number of blocks in a row to a certain threshold. What is the threshold?
In answering the question, what is $n$, when considering reorgs, they go passed the coinbase transaction, that is a good limit. 

So to rephrase the question, what is the chance of mining $n$ blocks in a row? What is the probability of mining $n$ blocks in a row? Let $n$ = 20, 50, 100 

A series of scenarios will be played out. Which scenario is more efficient? Which is cheaper- buying hashrate is easier?

#### Hashrate

Hash rate, similarly known as hash power, is the unit that measures how much power a cryptocurrency network using proof-of-work is consuming to be continuously functional, i.e. how much hash power it is consuming to generate blocks at the normal mean time. [[1]]

##### Mining Pool Difficulty

Each mining pool sets its own difficulty, which is lower than that of the network, to award the participants in accordance with the work they are doing. [[2]] But how does one know what the hashing power is of a particular machine?  It's by the diff of the submitted shares coupled with the time needed to generate said shares.  Higher diff/longer time is eqivalent to lower diff/shorter time.  Hashpower at the pool level is back calculated via diff of shares and time; for the whole Network it is based on solved blocks and time.

#### Game Theory

## Attack Vectors 

### 51% attack

In Proof of Work (PoW) cryptocurrencies, nodes typically are set up to recognize the blockchain with the most blocks (and therefore the most hashing power) as the correct version of history. Miners with > 50% of the network hashing power can take advantage of this by sending funds to one address on the main chain, while sending the same funds to another address on a forked copy of the blockchain that they are silently mining with more hashing power than the main chain.

Since other nodes only know about the main chain, they will see the first transaction as valid, and exchanges, etc will accept this transaction as valid. This malicious node can later release these silently mined blocks, and other nodes will accept this as the new 'correct chain' since it is longer. This will cause the original transaction to effectively dissappear, and nodes will recognize the funds as being sent to the address from the new chain instead. This is known as a 'double spend' attack.

Most bigger cryptocurrencies have sufficient mining capacity behind them, making it extremely expensive to acquire the necessary hardware to pull an attack like this off. Smaller cryptocurrencies have less hashing power securing the network, making it possible to simply rent hashing power from miners on a service like NichHash for a few hours. This significantly reduces the capital costs of an attack.

Recently there have been a number of 51% attacks including against Bitcoin Gold where $18 Million was stolen. [[3]]

#### NiceHash

**NiceHash** is a Slovenian [cryptocurrency](https://en.wikipedia.org/wiki/Cryptocurrency) [hash power](https://en.wikipedia.org/wiki/Cryptographic_hash_function) broker with integrated marketplace that connects sellers of hashing power (miners) with buyers of hashing power using the [sharing economy](https://en.wikipedia.org/wiki/Sharing_economy) approach.

Buyers select the crypto-currency that they want to mine, a [pool](https://en.wikipedia.org/wiki/Mining_pool) on which they want to mine, set the price that they are willing to pay for it, and place the [order](https://en.wikipedia.org/wiki/Order_(exchange)). Once the order is fulfilled by miners who are running NiceHash Miner on their machines, buyer gets the crypto-currency from the pool. This means that buyers aren't required to run complex mining operations themselves, and there is no capital investment in mining hardware required.''

https://en.wikipedia.org/wiki/NiceHash

### Selfish Mining 

Selfish mining is a strategy for mining bitcoin in which groups of miners collude to increase their revenue. Bitcoin was invented to decentralise production and distribution of money. But selfish mining can result in centralization of bitcoin mining operations. 

Selfish minig was first proposed by Cornell researchers Sirer and Eyal in 2013. They proved that miners can earn more bitcoins by hiding newly-generated blocks from the main blockchain and creating a separate fork. 

Bitcoin mining relies on miners who solve cryptographically complex puzzles to generate coins. Income from the activity varies because the process is dependent on several factors, from the difficulty of puzzles being solved to electricity costs to hte quality of Internet connections. The bitcoin protocol is configured to reward miners in proportion to their mining output. This ensures that even if miners organise themselves into large pools, the rewards are still dependent on coins produced by individual miners in teh public blockchain. 

But the above scenario assumes that miners will make their newly-generated blocks avaiable on bitcoin's public blockchain. Sirer and Eyal showed that miners can increase their share of overall revenue by hiding new blocks and making them avaiable to systems within their private network. This practice speeds up the discovery process and irons out infrastructure problems related to mining, such as network latency and electricity costs. 

Intiailly, the forked blockchain will be shorter than the public blockchain. However, selfish miners can strategically time their display of new blocks such that honest miners from teh public blockchain abandon their own chain and join the private chain. Subsequently, the private chain mines new blocks within its pool and hides the newly-generated blocks. 

In the meanwhile, the public blockchain continues mining new blocks. The process is repeated until the private blockchain is greater the public one. Now the private chain reveals its blocks again, and miners from the piblic chain abandon their blocks to join the private chain becauuse it is more lucrative. Sirer and Eyal analyzed resources wasted for both chains and determined that selfish miners possessed a competitive advantage over a miner on the public blockchain because their rewards are comparatively greater due to less wastage. 

"Once a selfish mining pool reaches the threshold (of a public blockchain),rational miners will preferentially join selfish miners to reap the higher revenues as compared to other pools," the reproacher write. According to them, the scenario may result in a situation where the selfish mining chain becomes a majority of the public blockchain. This will collapse bitcoin's decentralised nature and a selfish pool manager will control the system. 

https://www.investopedia.com/terms/s/selfish-mining.asp

Given that most of the network follows the 'standard' Bitcoin protocol, a single node (or a pool) which possesses enough computational resources or is extremely well connected to the rest of the network can increase its expected rewards by deviating from the protocol. While the standard protocol requires nodes to immediately publish any block that they find to teh rest of the network, it has been shown that participants can selfishly increase their revenue by selectively withholding blocks. 

https://arxiv.org/pdf/1507.06183.pdf

## Calculating the Cost of an Attack 

Using the prices NiceHash lists for different algorithms we are able to calculate how much it would cost to rent enough hashing power to match the current network hashing power for an hour. Nicehash does not have enough hashing power for most larger coins, so we also calculated what percentage of the needed hashing power is available from Nicehash.

Note that the attack cost does not include the block rewards that the miner will receive for mining. In some cases this can be quite significant, and reduce the attack cost by up to 80%. [[3]]

## Mining Centralization 

While the use of proof-of-work (PoW) to solve the double spending problem was Satoshi Nakamoto's key breakthrough with Bitcoin, it is also viewed as one of the weakest points of the system in terms of its potential to be attacked. 

Someone who controls 51% of the computing power pointed at the Bitcoin network is able to choose which transactions can be processed. Someone who controls the majority of the network hashrate can also reorganise the history of network transations in a malicious attempt to spend the same money twice. 

That said, gaining such a large percentage of the network hashrate would be no easy task, seeing as current estimates put the network hashrate at around 70 million terahashes per second. 

During the future of Bitcoin minin gat the Bitcoin 2019 conference, Streng made it clear that he does not view current level of centralization in Bitcoin mining as acceptable. 

While Satoshi's orginal vision of the mining process involved the concept of one vote per computer, that optimistic vision was thrown out rahter early in Bitcoin's history. By 2012, hardware devices built for the specifdic purpose of mining Bitcpin had been developed, and Bitcoin mining was on its way towards specialization and industrialization. 

While Corallo acknowledged miners can gain an advantage by obtaining access to the cheapest electricity in the world, he also pointed out that the availability of cheap power in chunks of 10 to 100 megawatts is somewhat limited and these sorts of setups won’t necessarily account for a large chunk of the overall network hashrate. [[4]] 

Decentralisation of mining power is important to keep control of a coin democratic. [[5]]

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

This design structure was chosen to make Myriadcoin resistant to ASIC specialization and centralization as the hardware requirements for the algorithms are different. Myriadcoin is also resistant to consensus attacks such as a 51% attack. 51% attacks can occur when an entity controls over 50% of the network's hashrate, which would allow the controller to exclude transactions from the blockchain and reverse transactions created while they maintain control over the network. In Myriadcoin, the possibility for this is reduced as a user would need to control over 50% of the hashing power across multiple algorithms. [[5]]



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

https://github.com/zawy12/difficulty-algorithms/issues/41

## Bitcoin Algorithms 

### Bitcoin Difficulty Algorithm

The bitcoin network has a global block difficulty. Valid block must have a hash below this target. Mining pools also have a pool-specific share difficulty setting a lower linit for shares. [[6]][[7]]

Difficulty changes every 2016 blocks. This is calculated using the following formula:

$$
difficulty = \frac{difficulty_1_target}{current_target}
$$

Where the target is a 256-bit number 

difficulty_1_target can take various values. Traditionally it's a hash function first 32 bits of which are equal to 0 while all the rest are 1 (it is also called diff or pool difficulty). Bitcoin protocol provides target as a type with floating point and limited accuracy. Different Bitcoin clients often determine cryptocurrency difficulty based on this data. 

Difficulty is changed every 2016 blocks based not the time it took to discover 2016 previous blocks will take exactly 2 weeks. If previous 2016 blocks were found in more than two weeks the cryptocurrency mining will be lowered, and if they were mined faster than that it will be raised. The more (or less) time was spent on finding the previous 2016 blocks the more will difficulty be lowered (raised) 

### Bitcoin Blocktime Algorithm

Average time of finding a single block can be calculated using this formula

$$
Time = difficulty x 2 x 32/ hashrate
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

## Hypothesis

Scenario 5 best, better than 2 last 3 

### Assumptions 

- Assume the system is in equilibrium 
- Model is steady state
- Define cost that is agnostic of hashrate 
- Hashrate is constant --> Difficulty is constant 

## Implementation

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
- https://en.bitcoin.it/wiki/Block_timestamp
- https://monero.stackexchange.com/questions/3300/timestamp-question

## References 

[[1]] "Explaining Hash Rate or Hash Power in Cryptocurrencies" [online].
Available: <https://coinsutra.com/hash-rate-or-hash-power/>. Date accessed: 2019&#8209;11&#8209;15.

[1]: https://coinsutra.com/hash-rate-or-hash-power/
"Explaining Hash Rash"

[[2]] "Bitcoin Forum- Question about Mining Pool Difficulty" [online].
Available: <https://bitcointalk.org/index.php?topic=5137845.0>. Date accessed: 2019&#8209;11&#8209;15.

[2]:https://bitcointalk.org/index.php?topic=5137845.0
"Bitcoin Forum- Question about Mining Pool Difficulty"

[[3]] "Crypto51" [online].
Available: <https://www.crypto51.app/about.html>. Date accessed: 2019&#8209;11&#8209;15.

[3]: https://www.crypto51.app/about.html
"Crypto51"

[[4]] "Bitcoin Mining Centralization is 'Quite Alarming', But A Solution is in the Works" [online].
Available: <https://www.forbes.com/sites/ktorpey/2019/07/28/bitcoin-mining-centralization-is-quite-alarming-but-a-solution-is-in-the-works/#49b8e6dd530b>. Date accessed: 2019&#8209;11&#8209;15.

[4]: https://www.forbes.com/sites/ktorpey/2019/07/28/bitcoin-mining-centralization-is-quite-alarming-but-a-solution-is-in-the-works/#49b8e6dd530b
"Bitcoin Mining"

[[5]] "MyriadCoin Wikipedia" [online].
Available: <https://en.bitcoinwiki.org/wiki/MyriadCoin>. Date accessed: 2019&#8209;11&#8209;13.

[5]: https://en.bitcoinwiki.org/wiki/MyriadCoin
"MyriadCoin Wiki"

[[6]] "Difficulty Wikipedia" [online].
Available: <https://en.bitcoin.it/wiki/Difficulty>. Date accessed: 2019&#8209;11&#8209;13.

[6]: https://en.bitcoin.it/wiki/Difficulty
"Difficulty Wiki"

[[7]] "Difficulty in Mining Wikipedia" [online].
Available: <https://en.bitcoinwiki.org/wiki/Difficulty_in_Mining>. Date accessed: 2019&#8209;11&#8209;15.

[7]:https://en.bitcoinwiki.org/wiki/Difficulty_in_Mining
"Difficulty in Mining Wiki"



## Contributors

- <https://github.com/kevoulee>