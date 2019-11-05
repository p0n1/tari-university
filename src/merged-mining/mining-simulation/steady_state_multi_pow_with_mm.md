# Steady-state Multiple PoW with Merged Mining 

**Blockchain modelling: Investigate merged-mining and mining centralisation**

1. Develop models around merged-mining and mining centralization with upcoming RandomX PoW protocol for Monero, and how this may effect Tari.

## RandomX 

RandomX is a new ASIC resistant PoW algorithm. It is designred to be ASIC restistant through the use of random code execution and memory-hard techniques to prevent specialized mining hardware from dominating the network. 

## Bitcoin Mining Centralization 

While the use of proof-of-work (PoW) to solve the double spending problem was Satoshi Nakamoto's key breakthrough with Bitcoin, it is also viewed as one of the weakest points of the system in terms of its potential to be attacked. 

Someone who controls 51% of the computing power pointed at the Bitcoin network is able to choose which transactions can be processed. Someone who controls the majority of the network hashrate can also reorganise the history of network transations in a malicious attempt to spend the same money twice. 

That said, gaining such a large percentage of the network hashrate would be no easy task, seeing as current estimates put the network hashrate at around 70 million terahashes per second. 

During the future of Bitcoin minin gat the Bitcoin 2019 conference, Streng made it clear that he does not view current level of centralization in Bitcoin mining as acceptable. 

While Satoshi's orginal vision of the mining process involved the concept of one vote per computer, that optimistic vision was thrown out rahter early in Bitcoin's history. By 2012, hardware devices built for the specifdic purpose of mining Bitcpin had been developed, and Bitcoin mining was on its way towards specialization and industrialization. 

While Corallo acknowledged miners can gain an advantage by obtaining access to the cheapest electricity in the world, he also pointed out that the availability of cheap power in chunks of 10 to 100 megawatts is somewhat limited and these sorts of setups won’t necessarily account for a large chunk of the overall network hashrate.

### A New Bitcoin Mining Protocol 

Braiins announced a redesigned mining protocol as part of a new, open, and transpatent Bitcoin mining stack. 

A key aspect of this new mining protocol, known as Stratum v2, is that it allows individula miners, rather than the mining pool operators, choose which transactions go into mined blocks. 

The level of centralizatiopn found with mining pools is much worse that it is with the actual miners, so moving the process of choosing transations from the pools to the individual miners should be a boon for decentralisation. 







## Myriad Coin

- Myriad has 3 PoW and 2 merged PoW algos 
- Seems to be very 51% resistant 
- Interesting but the variance in blocktime is extreme 
- The target block rate is 1 min 
- Algos: each of the 5 Lagos has equal probability to solve the PoW, the difficulty is adjusted to 5min for each. Any algo can build on top of the longest chain, even consecutively. With the 5 algos, any 1 pool can only achieve 20% of the effience hash rate 
- Myriadcoin has 5 algorithms (SHA256d, Scrypt, Skein, Qubit, and Myriad-Groestl) that can independently solve blocks. They have independent difficulties that are adjusted using the same formula. Any algorithm can solve the next block even if it is the same algorithm. Each algorithm targets the same block time and the block r
- Having block times that are almost 50% in the low end opens you up to other attacks 

## Questions  

- Need to simulate to see if its more stable if its more active 
- parametrised sim of this approach. I suspect that it can be tuned to be far better than that data shows
- How it is affected by selfish mining- I suspect it will be fine but the sim should be able to show the effect of that
- Query: You You actually want consensus to be achieved only when every algo has a block, So perhaps 2 * num algos? Hypothesis: I think that if you get the difficulty adjustment right you don't need that. However we are speculating, a sim would answer a lot of these questions



##Notes

- Incentive to mine
- Hybrid mining, tasing power more for the merged mining 
- Two difficulties 
- It would be difficult to game? Bigger barrier to entry 
- Can’t start to mine- have to wait for the Monero chain (not ideal)
- Game theory 
- Merged miner with a lot of hash power- power is halved- need to overcome 
- Balances out- more hashing power (same on electricity used)
- Nothing stops mining pool for swapping hashing power 
- Difficulty? 
- Check myriad strategies 
- One laptop is the alternate miner- difficulty will increase 
- Look at the hash rate 
- Indication of electricity measure the power that you draw per block that you mine 
- What to mine.com 
- Check algorithm (if merged mined you can compare)
- Algorithms will expend different power 
- You want better revenue per wattage 
- Myriad mining, mainly after Monero 
- GPU power
- Check balance on a power level 
- Blake Blake ASICs not working 
- Race with CPU 
- Merged mining Myriad- 

## Question 

What is the cost to control the network?

### Definition of Control 

Blocks for an attack? Reason for choosing a specific number of blocks?
When we use the word 'control' what is actual meant is the chance of mining $n$ number of blocks in a row to a certain threshold. What is the threshold?
In answering the question, what is $n$, when considering reorgs, they go passed the coinbase transaction, that is a good limit. 

So to rephrase the question, what is the chance of mining $n$ blocks in a row? What is the probability of mining $n$ blocks in a row? Let $n$ = 20, 50, 100 

A series of scenarios will be played out. Which scenario is more efficient? Which is cheaper- buying hashrate is easier?

### Definition of Cost 

### Assumptions 

- Assume the system is in equilibrium 
- Model is steady state
- Define cost that is agnostic of hashrate 
- Hashrate is constant --> Difficulty is constant 


### Input assumptions 

### Method

Monte Carlo Simulation 

$n/1000000 = p$

5? random generator to simulate PoW (allocate hashrate)

#### Scenario 1 

We control some fraction of the Tari merge mined hashrate greater than 50%.  

$n$ hashes mining Tari, you need more --> argue the cost is zero  

#### Scenario 2 

1 x MM 50% 		1 x PoW 50% 
How much of the PoW hashrate do you need to buy control to make above statement true 

#### Scenario 3

1 x MM 33% 		2 x PoW 33% 33%

(Thought as a bad idea, flick between the 2- what would happen as they jump between each PoW)

#### Scenario 4

2 x MM 50% 50%

#### Scenario 5 

2 x MM 33% 33%	1 x PoW 33%


### Hypothesis

Scenario 5 best, better than 2 last 3 

#### Version 2 

Consider the dynamic aspects of the hashrate. Scale for Myriad. 
Is the block time affected by sudden increase in hash rate. This is a dynamic problem. 

#### Thought Process 

- Vary the merged Mined Hashrate controlled (%)



## Game Theory 

### PoW

Bitcoin is a digital currency which was introduced in 2009. Its security is based on a proof of work, and a transaction is only considered valid once the system obtains proof that a sufficient amount of computational work has been exerted by authorising nodes. The miners constantly try to solve cryptographic puzzles puzzles in the form of a hash computation. The process of adding a new block to the blockchain is called mining and these blocks contain a set of transactions. The average time to create a new block in blockchain is ten minutes. Two types of agents participate in the Bitcoin network: miners, who validate transactions and clients, who trade in currency. The blockchain is a shared data structure responsible for storing all transaction history. The blocks are connected with each other in the form of a chain. The first block of the chain is known as Genesis. Each block consists of a Block Header, Transaction Counter and Transaction. 

Each block in the chain is identified by a hash in the header. The hash is unique and generated bu the Secure Hash Algorithm (SHA-256). SHA takes any size plaintext and calculates a fixed size 256-bit cryptographic hash. Each header contains the address of the previous block in the chain. The process of adding blocks in the blockchain is called "mining of blocks". If miners mine a valid block, it publishes the blocks and extends the blockchain by a new block. The creator of the block is rewarded with the bitcoin. 


### Mining 

Bitcoin is a decentralized cryptocurrency payment system, working without a single administrator or a third party bank. A bitcoin is created by miners, using complex mathematical "proof of work" procedure by computing hashes. For each successful attempt, miners get rewards in terms of bitcoin and transaction fees. Miners participate in mining to get this reward as income. Mining of cryptocurrency such as bitcoin becomes a common interest among the miners as the bitcoin market value is very high. As a side effect of this mining process, a lot of electricity is used in it.  

### Electricity 

Electricity is a semi-renewable resource, depending on the type of resource used for its production. Nevertheless, electricity plays an essential role in the bitcoin mining process since the whole mining process is based on it. The electricity consumed by the mining system is directly proportional to the computational power of that system. Moreover, powerful computers that specially designed fro bitcoin mining process, consumes much more electricity than the regular computers. 

Electricity, one of the necessities of the human beings, can be considered as both renewables if it generates from the renewable resource for example solar energy or hydropower or water plants and non-renewable if it produced from the thermal power plant that uses the coal - a non-renewable resource. So, depending on renewable or non-renewable resources, chosen for production of electricity, it can also be considered as semi-renewable which means that it has a combined fraction of both means of electricity production. 

### Selfish Mining 

### Eclipse Mining 

### The Double-Spend Attack 

The first type of deviation is when miners deliberately create forks. This is simple to do: when searching for a valid block, just insert the hash of a block on the the blockchain that is not the last block. 
TO see why a miner might want to create a fork, support in the transaction T, Alice transfers some bitcoins to Bob. Suppose this transaction gets added to the blockchain as part of block b1. Bob only ships the purchased goods to Alice once another block b2 has been appended to b1. When Alice has the goods, she could try the following attack: try to find a valid block b3 extending b0, another block b4 extending b3 and a third block b5 extending b4. Alice does not put transaction T in any of these blocks. 
If Alice successfully creates these three blocks before any other miner extends b2, then she rips off Bob: b1 and b2 are orphaned and Alice's payment to Bob gets canceled, while the goods have already been sent. This attack is sometimes called the double-spend attack, especially in the case where Alice puts a payment T' to Carol in the block b3, promising the same coins to Carol that she already promised to Bob. 

The probability that Alice succeeds in her double-spend attack depends on how much computational power she has. Suppose that of all the computational cycles being devoted to bitcoin mining, Alice controls an x fraction. The fraction x is sometimes called Alice's mining power. Since finding valid blocks just boils down to random guessing or exhaustive search, the probability that Alice is the one who finds the next valid block is well-approximated by x. Finding three blocks in a row before anyone else, as needed in the double-spend attack above, happens with probability only x^3. More generally, if Bob waits for y>=1 blocks to be appended to b1 before shipping the goods, then the probability that a double-spend attack succeeds is only x^(y+2).

How big is x? If just a solo miner, then not very big. However many miners participate in mining pools, where the miners join forces, all working on the same puzzle, and sharing the rewards of finding a valid block among the pool members. The reward is shared proportionally, according to the amount of computation contributed by each member of the pool. 

### Difficulty 

Difficulty is a value used to show how hard it is to find a hash that will be lower than target defined by the system. 

The Bitcoin network has a global block difficulty. Valid blocks must have a hash below this target. Mining pools also have a pool-specific share difficulty setting a lower limit for shares. 

Difficulty changes every 2016 blocks. This is calculated using the following formula:

$$
difficulty = \frac{difficulty_1_target}{current_target}
$$

Where the target is a 256-bit number 

difficulty_1_target can take various values. Traditionally it's a hash function first 32 bits of which are equal to 0 while all the rest are 1 (it is also called diff or pool difficulty). Bitcoin protocol provides target as a type with floating point and limited accuracy. Different Bitcoin clients often determine cryptocurrency difficulty based on this data. 

Difficulty is changed every 2016 blocks based not eh time it took to discover 2016 previous blocks will take exactly 2 weeks. If previous 2016 blocks were found in more than two weeks the cryptocurrency mining will be lowered, and if they were mined faster than that it will be raised. The more (or less) time was spent on finding the previous 2016 blocks the more will difficulty be lowered (raised) 

https://bitcoin.stackexchange.com/questions/5838/how-is-difficulty-calculated

https://en.bitcoinwiki.org/wiki/Difficulty_in_Mining



Hashrate

https://forum.zcashcommunity.com/t/how-to-calculate-network-hasrate-from-current-difficulty/15577

https://coinsutra.com/hash-rate-or-hash-power/



Mining pool difficulty 

https://bitcointalk.org/index.php?topic=5137845.0


### block time 

Average time of finding a single block can be calculated using this formula

$$

Time = difficulty x 2 x 32/ hashrate

Where 'difficulty' is the current cryptocurrency difficulty level of BTC difficulty network and 'hashrate' is the amount of hashes a miner finds per second. 

### Difficulty in Monero

The difficulty adjusts with each block. 

The adjustment algorithm examines 720 prior blocks, starting from 15 blocks ago. 

Of those 720 blocks, the 60 highest and lowest block times are excluded from the analysis, which leaves 600 blocks 

Out of those 600 blocks, the average block time is determined. This average is then used to adjust the difficulty proportionally in order to target a 120 seconds. The unit of difficulty is therefor "hashes". 

When there is a large and sudden change in hashrate, due to the April 6th PoW change, it will therefore take 15+60=75 blocks before the change in hashrate starts to affect the difficulty. The change to difficulty when adjusting to the new hashrate will be gradual, and after 


Calculate network hashrate from current difficulty?

difficulty*120/seconds_for_block (120 here is hard coded value, estimated time for single block)



For version 2

- alpha trimmed mean 
- linearly weighted moving average (LWMA)
- moving median 
- https://en.bitcoin.it/wiki/Block_timestamp
- https://monero.stackexchange.com/questions/3300/timestamp-question