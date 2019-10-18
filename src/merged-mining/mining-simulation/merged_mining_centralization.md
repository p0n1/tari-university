# Merged Mining and Mining Centralization 

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

### A New Bitcoin Mining Protocol 

Braiins announced a redesigned mining protocol as part of a new, open, and transpatent Bitcpon mining stack. 

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







Incentive to mine

Hybrid mining, tasing power more for the merged mining 

Two difficulties 

It would be difficult to game? Bigger barrier to entry 

Can’t start to mine- have to wait for the Monero chain (not ideal)

Game theory 

Merged miner with a lot of hash power- power is halved- need to overcome 

Balances out- more hashing power (same on electricity used)

Nothing stops mining pool for swapping hashing power 

Difficulty? 

Check myriad strategies 

One laptop is the alternate miner- difficulty will increase 

Look at the hash rate 

Indication of electricity measure the power that you draw per block that you mine 

What to mine.com 

Check algorithm (if merged mined you can compare)

Algorithms will expend different power 

You want Bette revenue per wattage 

Myriad mining, mainly after Monero 

GPU power

Check balance on a power level 

Blake Blake ASICs not working 

Race with CPU 

Merged mining Myriad- 

## Question 

What is the cost to control the network?

### Definition of Control 

Blocks for an attack? 