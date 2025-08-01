# Bitcoin

<br>![miscellaneous image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/miscellany.jpg)


## Table of Contents

+ [**History of money**](#history-of-money)
+ [**Introduction**](#introduction)
+ [**Basic concepts**](#basic-concepts)
+ [**Consensus**](#consensus)
+ [**Nodes**](#nodes)
+ [**Proof of work and consensus**](#proof-of-work-and-consensus)
+ [**Bitcoin wallets**](#bitcoin-wallets)
+ [**Bitcoin whitepaper**](#bitcoin-whitepaper)
+ [**Extending bitcoin**](#extending-bitcoin)
+ [**Scalability**](#scalability)
+ [**Advanced bitcoin**](#advanced-bitcoin)
+ [**Future of Bitcoin**](#future-of-bitcoin)
+ [**FAQ**](#faq)
+ [**References**](#references)


## History of money

Humans are not self-sufficient, nor can exist in isolation. We need things other humans provide, and we provide things other humans need. We do **exchanges** (you give something you have in order to get what you want). Eventually, we invented agriculture and domesticated animals, so we were able to settle down at one place and created a society. Our labor became specialized (farmers, doctors, fishermen...), which increased productivity and quality of goods produced. 

**Barter system**: Until a few thousand years ago, human's exchange system was the barter system (we exchange goods and services with each other directly). The exchange ratio was determined based on demand and supply. However, it had limitations: no common measure of value (each good was pegged to different sets of other goods: 1 wheat bag = 2 fish or 5 haircuts or 4 pots...), need of double coincidence of wants (both parties need what the other provides), indivisibility of certain goods (if my goat is worth 10 pots, I cannot get 5 pots), lack of standards for deferred payments (credit transactions involve disputes about the quality and value of goods used), and storage problems (storing wealth is complicated: stored fishes will spoil).

**Commodity money**: These issues can be solved by using a widely consumed commodity that's always in demand and can be exchange for other goods. Romans used salt (divisible, non-perishable, limited, widely consumed), which was called *salarium* and is the origin of the word "salary". India used cattle. Virginia used tobacco. Carolina used rice. Africa used cowry shells. Brazil used sugar. Mongolia used tea. Anything can be "money" as long as enough people accept it in exchange for their goods and services. Money does not have to be backed by a government to be considered money. Commodities have limitations: storage issues, difficult to transport over long distances, no universal acceptability, and perishability.

**Metallic money**: It's a form of commodity money. Metals (like gold) are valuable, durable, divisible, fungible, homogeneous, scarce, and it's easy to verify its purity. However, they are heavy.

**Gold backed IOUs (Non-legal tender paper currency): To prevent theft, people would leave their gold with a goldsmith, who accepts it for a fee and issues a IOU (I Owe You) note. Anyone with a IOU note can retrieve the gold from the goldsmith. Eventually, IOU notes were accepted as payments. These goldsmiths eventually realized that not everybody claimed their gold at one time, and they had a healthy balance of gold, so they started creating fake IOU notes not backed with any gold. The ratio of gold obligated to repay and the actual gold they had in the vault kept deteriorating and, occasionally, the goldsmiths disappeared overnight along with all the gold, making IOU notes worthless.

**Legal tender coinage**: Fraudsters used metallic money to cheat the public in purity or weight (mix precious metals with less precious metals). The governments decided to solve this by taking control of metallic money minting and stamping them with symbols that guarantee their weight and purity. Problem: it was centralized. Governments ended up debasing the currency (mixing precious metals) whenever they needed money, which increased money supply, decreased value of precious metals in the coins, hurt trust in the currency, deteriorates international trade, and causes domestic inflation.

**Paper money**: The oficial Chinese government currency had copper. It was difficult to use them for large transactions because they were heavy, so some people left their coins to trusted agent who would issue paper promissory notes, which could be used as a currency. It was easy to store, to transport, to carry, to divide, and was not perishable. Eventually, the Chinese emperors issued a nationwide paper currency standard backed by gold or silver that was legal tender (i.e., recognized by law as a mean to settle debt or meet financial obligations). Problem: it was centralized. Whenever the state needed money, they printed more currency, which led to oversupply and hyperinflation. The currency became worthless and China discontinued the use of paper currency in 1455. They would not adopt it again for hundreds of years.

Differences between **money** and **currency**: 

- **Money**: Item of verifiable record that is generally accepted as payment for goods and services and repayment of debts (such as taxes) in a country or socio-economic context. Main functions: medium of exchange, unit of account, store of value, standard of deferred payment (sometimes). It's intrinsically valuable and is a store of value. Example: gold.

- **Currency**: System of money (monetary units) in common use, specially for people in a nation. Monetary unit (in any form) used as a medium of exchange (usually referred to coins and banknotes). Example: dollar.

**Paper money in USA**: In 1690, the colonies started printing paper money denominated in pounds (each colony had its own). However, they printed too much, causing inflation and currencies devaluation. The British parliament ended this money printing with some "Currency acts". During the American Revolution, they states and the Continental congress issued paper money again. Soon, they printed too much and it became worthless by the end of the war. After the war, they created the current dollar, which was based on the Gold Standard (i.e., it represented actual gold and silver the government had in its vaults). But, whenever more money was needed, the government printed more money, reducing the amount of gold each dollar was worth. Many countries started cashing in dollars for actual gold, leading to the collapse of the Gold Pool. In 1971, the government ended the direct convertibility of gold to dollars (Nixon Shock), making the dollar a fiat currency.

**Fiat money**: Currency established as money by government regulation. It has no intrinsic value (no inherent utility) and is not backed by any physical commodity. It has value because parties engaging in exchange agree on its value and the government maintains its value by controlling money supply through a central bank. Virtually all countries follow this model. Problem: it's centralized and they print too much.

**Plastic money**: Money can be kept on banks and, instead of using notes, we can use plastic cards (ATM cards, debit cards, credit cards...) to spend money directly from the bank.

**Digital currencies**: People has tried to create a fully digital currency using computers and internet (like E-gold in 1996). However, it was difficult to solve the *double-spending problem* (computers make it easy to copy files, and it's not clear how to ensure that you cannot spend the same currency twice). Early digital currencies solved this by having a central organization that verifies it. This system works, but it has a single point of failure: the central organization. Hackers would target this central organization, worried governments would litigate and shut them down, and sometimes the parent company would suddenly liquidate.  

**Bitcoin**: It was needed a decentralized system that solved the double-spending problem, that could not be targeted by a government or hacker, and without a parent company. Bitcoin is a decentralized currency that solved this problem using **blockchain** and **proof of work**.

**Satoshi Nakamoto**: Creator of Bitcoin. See a compilations of his publications [here](https://github.com/AnselmoGPP/know_base/blob/master/topics/security/blockchain/satoshi.md).


## Introduction

### Cryptography

**Hash function**: Function that takes an input (any kind of message) of arbitrary length and outputs a value (digest, hash, tag, fingerprint) of fixed length that looks random. It's a deterministic function (it gives the same output for the same input). The slightest change of the input produce a completely different unpredictable output. Example: SHA-256 function outputs a 256 bit hash (it has 2<sup>256</sup> possible signatures).

- **Cryptographic hash function**: Hash function where reversing the process (converting hash to input) is infeasible. The best way would be to guess and check inputs. It's designed for applications that require cryptography, security, privacy, confidentiality, or authentication. Some of the most common ones are **MD5** (and predecessors like MD4) and **SHA-256** (and predecessors like SHA-1). They are key building blocks in many algorithms and protocols, which are critical in many applications: **digital signatures** (Bitcoin, e-commerce protocols, …), **encryption**, message authentication protocols, pseudorandom number generation, password security, etc.

  - When used for **digital signatures**, it has to be computationally efficient (fast to compute), collision resistant (it must be astronomically hard to find two inputs that map to the same output, it must hide any information about the inputs, and output must be well distributed (it must look random, unrelated to the input, not predictable).

**Encryption:**

- **Symmetric encryption**: A and B share a secret key (they had a secret meeting in advance) that they use to encrypt and decrypt the messages they send to each other.

- **Asymmetric encryption**: There is a key pair (X, Y) such that any of these keys can be used to encrypt a message, but only the other key can decrypt it. It's not possible to guess one key from the other. 

  - **Public key cryptography**: Once we generate a key pair, we take one as **public key** (PK) (you can publish it anywhere with your name on it) and the other as **private/secret key** (SK) (kept secret). There is no need to have a secret meeting in advance to share any SK. Uses:

    - Encrypt a message with your public key &rarr; This guarantees that only you can decrypt the message.
    - Encrypt a message with your SK &rarr; It's guaranteed that you are the author of the message, and anyone can decrypt it with your PK.
    - Encrypt a message with your SK, and then again with your friend's PK &rarr; This guarantees that you're the author, and that only your friend can decrypt it (with his SK and your PK).

Public key cryptography (like RSA) can be too slow for communicating long messages. Instead, we usually use asymmetric cryptography for verifying one party and exchanging a key, and then we continue communication using symmetric cryptography (like AES). Example: Part of the TLS protocol (between HTTP and TCP) is a certificate and a digital signature, and it takes part in a handshake.

**Digital signature**: During a handshake, A wants to confirm to B who he is, so A uses his SK to encrypt a message known by both, and sends it to B. Then B can decrypt it using A's PK and check whether it is identical to the original message.

- Signature schemes (like RSA) don't work well with too long (slow encryption) or short (less random encryption) messages so, before encrypting the message we apply a hash function to it (like SHA256) so it becomes a hash of a given length. Since 256 bits is quite short for this kind of signature scheme (we want to avoid a hash that is a small number because it's a security risk), we increase its length by adding some padding or applying a similar mechanism.

- Example 1: In TLS, you exchange a bunch of messages. At some point, you send a certificate containing a PK and a Certificate verify message (TLS 1.3) containing a message (summary of the previous messages, hashed, padded, and encrypted with your SK).

- Example 2: We have a certificate for a server backed by a SK kept on the server. This certificate holds their public key, and a digital signature signed by some certification authority. So, when you do a handshake and the server sends you the certificate, you can verify (take the content of the certificate, hash it, pad it, decrypt it using his PK, and compare them) that it was properly signed by the certification authority you trust.

**Cryptographic hash functions** are used for **asymmetric encryption**, and more specifically, for **public key cryptography**, which is used for **digital signatures**.

There's no mathematical proof that these techniques are secure. We trust them based on how long they've been around.


### Bitcoin

Bitcoin is a fully digital currency. There's no government issuing it, and no bank verifying transactions. Instead, there's a clever system of decentralized trustless verification based on some cryptography math.

Consider a group of people that make exchanges between each other. All exchanges are registered in a ledger. All participants maintain a ledger with all transactions in the group. The currency IS the ledger itself (the money never leave the ledger). Anyone can add lines to the ledger, but only signed transactions are valid, and no overspending is allowed.

**Digital signatures**: To prevent fraudulent lines being added, a payer must sign his payments. Each participant has a pair SK and PK (two strings of bits). The PK can be known by anybody. The SK is secret and only known by his owner. 

- `sign(message, SK) = signature`: The SK + message produce a signature, which is different for each message. Only you can sign a message without your SK, and nobody can produce the same signature as you. 

- `verify(message, signature, PK) = true/false`: The signature can be verified using the message, signature, and PK. 

It's completely infeasible to find a valid signature without knowing the SK (there's no better strategy than guessing and checking random signatures). Also, to ensure that one signed transaction is not copy-pasted, each transaction includes an id, which requires a different signature even for identical transactions.

**Decentralization**: Each participant holds their own copy of the ledger, which removes the need of trust. When A pays something to B, this transaction is broadcasted into the world, so everybody put it into their ledgers. 

**Proof of work** (PoW): How to ensure that everybody receive the same transactions in the same order? Basically, we trust the ledger that has the most computational work put into it. This also makes fraudulent transactions and conflicting ledgers require an infeasible amount of computation to bring about. 

- At the end of a list of transactions (block) we put a number (called PoW) and encrypt the block with a cryptographic hash function. This PoW have to make the hash begin by a certain number of zeros. To find out the PoW we have to guess and check a lot of numbers until we get the hash we look for. Example: The probability of finding a number that produces 30 heading zeros is 1/2<sup>30</sup>. 

- Finding the PoW is expensive, but verifying it is easy. This work is intrinsically tied to the list of transactions. Modifying one transaction changes the hash completely, which also requires to compute the PoW again.

- The number of zeros a PoW must create is changed periodically so it takes 10 minutes on average to find a new block.

**Blockchain**: Data structure of the ledger. Decentralized digital ledger. Each valid block of transactions has a PoW at the end. To ensure the order of the blocks, each block also contains the hash of the previous block at its header. So, if somebody wants to modify a block, he will need to compute the PoW of that block and the following ones. When somebody finds out the block's PoW, he broadcasts the block to the rest of the world so everybody copy it to the blockchain. You can check blocks information at [BlockExplorer](https://blockexplorer.one/).

**Miners**: They create new blocks, looking for a **block reward** and **fees**. Not everybody are miners. Those making transactions just listen for blocks broadcasted by miners and update their own personal copies of the blockchain. If you hear two distinct blockchains with conflicting transaction histories, you take the longest one (who has the most work put into it). If they have the same length, just wait until one of them is longer. This provides a decentralized consensus (we don't trust a central authority but computational work). 

- **Block reward**: The one who finds the PoW gets a **block reward** (he's allowed to put a special non-signed transaction at the top of the block were he gets some money from nobody), incrementing the total money supply.

- **Transaction fee**: When you make a transaction, it can optionally include a fee with it that will go to the miner that includes your transaction in a block. Each block is limited to ~2400 transactions (Visa is capable of handling >24.000/s), which is slow and makes for bigger fees.

Fraud example: Imagine miner A wants to fool B by sending him a block with A paying something to B. The other miners won't be aware of this payment. For A to keep the fraud alive, he would have to keep finding the subsequent PoWs faster than the other miners so his blockchain is longer (only possible with >50% of computing power).

**Bitcoin protocol**: The ledger is the currency (it doesn't need to transform it to another currency). It's based on digital signatures and a PoW. The data structure of the ledger is the blockchain. It's decentralized.


## Basic concepts

**Bitcoin**: Protocol for a decentralized peer-to-peer network that creates consensus without needing a central authority to provide trust.

**bitcoin** (BTC): Currency (token) issued as a reward in the proof-of-work mining process. For plural, don't use s suffix ("I have 3 bitcoin").

**Blockchain**: Public ledger where the network records (transactions) are written.

How do people acquire bitcoin?

- __Earn__: Get paid in bitcoin: Offer a service, sell a product, or get wages paid in bitcoin ([bitwage.com](https://www.bitwage.com/)).
- __Buy__: Exchange national money (fiat) for bitcoin (from an exchange, from a bitcoin ATM, or from another person directly from cash).
- __Trade__: Trade your belongings for bitcoin (sell car, sell house...).

Bitcoin doesn't have a price (commodities do) but an exchange rate (because it's money).

**Price discovery**: The market doesn't set the price/exchange rate, but discovers it. Markets find out what the real value of something is by looking at market movement. The current price is the average of the prices that people agreed and traded on over the past period of time (it can be seen in the Order book).

**Order book**: Graph that shows the buy and sell orders. It looks like two lines separating from the centre and increasing height.

**Spread**: Difference between bid (buy) price and ask (sell) price (example: A wants to sell at 15$ but B wants to buy at 15$, so spread = 5$). Buyers and sellers change their orders until they agree on a price.

**Bitcoin ATM**: ATM machine that exchanges you fiat money for BTC. It has a slot for introducing money, and a camera for scanning a QR code representing a BTC address. It connects to the Internet to use some price provider (such as [bitcoinaverage.com](https://bitcoinaverage.com/)).

**BTC address**: Public identifiable number generated from a SK (the oppossite isn't possible). It's possible to make transfers to/from this address. The owner/s of this address are those who know its SK. Anybody can see its content (amount of BTC) and make transfers to this address, but only the owner/s can transfer from it. A BTC address tells you nothing about the SK. 

The **SK* is 256 bits (77 decimal digits). For convenience (shorter numbers), we represent it using base-58 (each digit is 1 out of 58 possible digits: 26 uppercase letters + 26 lowercase letters + 10 numbers - L - l - O - o), resulting in a 42 character number.

When somebody transfer BTC, they're transfer them to a BTC address. The BTC are always in the blockchain (not my pocket, not my wallet...). Anybody can send BTC to any BTC address.

**Satoshis**: It's the only money unit that actually exist in the system (1 BTC = 100 million sat.). BTC doesn't exist, satoshis do. Nowhere in the BTC system there is a unit of BTC, everything is measured in satoshis.

- 1 BTC = 1000 millibit
- 1 millibit = 1000 bits
- 1 bit = 100 satoshis

Currently, BTC is not a good unit of account yet because it's **volatile**, due to the small size of the market. This makes it difficult to price things. Also, BTC is not legal tender (it's not accepted for paying taxes).

**Bech-32** (Native segwit address): Type of BTC address that uses a 32 character encoding (no uppercase letters used), which has some properties for error correction. Most wallets use this format. It uses prefix bc1q.

**Transaction process**: When a transaction is made, it's required to spend all the money in the origin address. What the wallet does is to send the amount you want to send to the destination address and the rest to an address of yours (called change address), except for a small amount that you may left untouched for the miners to take (fee). If a change address is not provided, all of the rest is left for the miners as fee.

- __Input__: Satoshis that are sent to your address (example: an ATM sends satoshis to your address).
- __Output__: Satoshis sent to destination address + those sent to change address (the fee is left behind).

Blocks activity can be explored with tools such as [blockstream.com](https://blockstream.info/).

**Transaction fees** are necessary because there's a limited space for transactions (by physics, technology, and software). Fees determine who values their transaction more, and support mining as issuance declines.

**Mempool** (queue): When transactions are transmitted into the BTC blockchain they're not automatically included in the very first block because usually there're more transactions and all of them doesn't fit in a block. So, these transactions wait in each node's **mempool** until they're included in the blockchain. The higher the fee, the sooner the transaction is included in a block.

**Confirmations**: At the beginning, the transaction is unconfirmed (still in the mempool, not mined in a block yet). Once it appear in a block, it has 1 confirmation. And the more blocks are mined on top of it, the more confirmations it gets.

BTC works as a **broadcast network** (flood/gossip protocol), which means that any transaction sent to the BTC network is shouted. The wallet sends the transaction to all the BTC nodes it is connected to. These nodes confirm the transaction's validity and send it to all the nodes they're connected. An so on. In ~15 seconds it's spread to the entire BTC network.

For large transactions (TV, car, house...) people may want to wait for several confirmations, which takes time. With little transactions (coffee, pencil, candy...) we usually don't care about confirmations (most probably it will get into a block). The higher the risk, the more confirmation me require. 

**Settlement (or clearing)**: Finalization of a transaction. Moment at with the transaction is no longer reversible. A credit card transaction is approved in a few seconds, but it takes 60 days to clear/settle. Retail transactions are not instantaneous (except if it's cash), but they look so.

Bob may have multiple addresses with little amounts of satoshis (UTXO, unspent chunks of BTC). When he does a big payment, the wallet takes some of his accounts and pay with all of them (because he has a bunch of loose change). It aggregates multiple inputs and makes the payment (payment + change + fees).

The **blockchain** begins with the block 0 (Genesis block). Each block references the hash of the previous block (parent block), which creates an unbreakable chain of blocks. If you modify one block, the subsequent blocks won't reference your block correctly and will also require to be changed. Each block has an amount of BTC in it (mining reward, issuance, subsidy). The mining reward was 50 BTC at the beginning, but it's reduced to a half every 210.000 blocks (~4 years), until it gets to 1 satoshi, and then to 0 (by year ~2141). The maximum supply will be 21 million BTC (almost).

Miners receive two rewards: new coins created with each block and transactions fees from all transactions in the block. Each block has at least one transaction: the **Coinbase transaction**, which is built and signed by the miner (he also adds a fee in it) and contains the new BTC. For security, the reward cannot be spent for 100 blocks.


## Consensus

There are different computers. Some may run the consensus algorithm as expected, while others may do bad things. If the consensus algorithm works, bad computers aren't going to mess things up. A consensus is formed when all good computers agree upon and use a single blockchain. It's a matter of agreeing upon a single block across our good computers.

Traditional consensus algorithms (Paxos, Raft, Practical Byzantine Fault Tolerance, …) doesn't work for BTC.

- They usually assign one vote per computer. BTC allows computers to join or leave the network at any time. However, to get a majority of votes, these algorithms require a certain fixed number of votes. Changes in the number of computers mess this up.
- An attacker may spawn a potentially infinite number of virtual machines and get much more votes.
- They don't tolerate partition very well (i.e., 2 or more consensus are created).

BTC requires a consensus algorithm where:

- New blocks are eventually replicated at all good nodes (consensus reached).
- Newer blocks point to this new block.
- Nodes can join or leave at any time, while maintaining consensus and without causing deadlock.
- The network is partition tolerant (each half forms a consensus, but when the partition heals, so does the consensus).

**Strawman consensus algorithm**: Create a block whenever you want and tell your neighbours about it so they can replicate it. If you hear about a block, tell about it to your neighbours and replicate it. It's like a gossip protocol. This works well if there's one node that creates blocks, but fails if there're two blocks generating blocks at the same time. 

- We may try to resolve forks by picking randomly one of the longest branches. However, it's possible to get a fork where each branch grows forever without consensus (livelock). This is caused because we can add blocks faster than we can learn about other blocks. 

  - Solution: Slow adding blocks, and sleep some random time before adding one. 

  - Problems: The longer the timeout, the lower the odds of a fork, but the longer to reach consensus. The more computers, the shorter the time for someone to timeout (and the longer to reach consensus).

- Network partitions: One or more computers loose communication with the rest of the network, so they start running their own blockchain. Chances are that the largest group grows their blockchain faster. After communication is restored, partition can be healed and a single consensus reached.

- Choose a (cheat-resistant) timeout value empirically: If blocks arrive too quickly, slow down (BTC changes timeout every ~14 days). Solution: to create a block, a math problem must be solved first. This problems must be impossible to solve quickly, but easy to verify. The solution (Proof of Work) must be included in the block. This problem involves adding a number (nonce) to the block in order to make the block hash (the hash to include in the next block) begin with a certain number of zeros. This can only be solved via brute force (try different nonces). 

**Bitcoin rules** (hard rules) (often called, incorrectly, consensus rules): Specific set of rules that all BTC full nodes will unfailingly enforce when considering the validity of a block and its transactions (example: A block can only create a certain number of bitcoin. If it creates more, all full nodes will reject the block). These rules require that all participants in the Bitcoin economy have consensus (with the meaning of the next definition) as to the consensus rules. If the economy disagrees about the consensus rules, then the currency and economy splits into two or more independent pieces. Adding new consensus rules can generally be done as a **softfork**, while removing any consensus rule requires a **hardfork**. Rules regarding the behaviour of the mere network protocol are not consensus rules, even if a change to its behaviour breaks backward-compatibility. The consensus rules are only concerned with the validity of blocks and transactions. 

**Consensus**: Two meanings:

- **Near-unanimity** (non-contentious, near-unanimous): No significant objection among the set of people who "matter". Level of agreement required to roll out a hardfork (no significant section of the Bitcoin economy should actively oppose the hardfork).

- **General agreement**: Strong majority when participants are weighted for expertise/strength of argument (votes of experts have more value). This is commonly the way technical decisions are made in open source projects like Bitcoin.

**Code fork**: An altcoin that is derivative of Bitcoin.

**Chain fork**: Occurrence of multiple blocks at the same height.

[**Hardfork**](https://en.bitcoin.it/wiki/Hardfork): Change to the protocol that makes previously invalid events (blocks, transactions) valid, and therefore requires all users to upgrade. Anything that changes block structure (including block hash), difficulty rules, or amount of valid transactions is a hardfork. 

Some of these changes can be implemented in a softfork by having the new transaction appear to older clients as a pay-to-anybody transaction (of a special form), and getting the miners to agree to reject blocks including the pay-to-anybody transaction unless the transaction validates under the new rules. 

Bitcoin Core has had two accidental hardforks (and many altcoins have had intended hardforks):

- 2013: Due to a BerkeleyDB issue, Bitcoin pre-0.8 hardforked, and there was a chain split. This happened before the foundation of Bitcoin Core. The post mortem is in [BIP 0050](https://github.com/bitcoin/bips/blob/master/bip-0050.mediawiki).
- Bitcoin Core 0.15 accidentally hardforked (see [CVE-2018-17144 full disclosure](https://bitcoincore.org/en/2018/09/20/notice/)). The fix was a softfork deployed in v0.16.3. There was no chain split.
- In August 2019, John Newbery proposed another hardfork to bury CSV and segwit activation.

[**Softfork**](https://en.bitcoin.it/wiki/Softfork): Change to the protocol where only previous blocks/transactions are invalidated. Since old nodes will recognize the new blocks as valid, a softfork is backward-compatible. 

- New transaction types can often be added as softforks, requiring only that the participants (sender and receiver) and miners understand the new transaction type. This is done by having the new transaction appear to older clients as a "pay-to-anybody" transaction (of a special form), and getting the miners to agree to reject blocks including these transaction unless the transaction validates under the new rules (this is how [P2SH](https://en.bitcoin.it/wiki/Pay_to_script_hash) and [Segregated Witness](https://en.bitcoin.it/wiki/Segregated_Witness) were added to Bitcoin.

- Accidental hardforks can be undone using a softforks (this is how [CVE-2018-17144](https://bitcoincore.org/en/2018/09/20/notice/) was fixed in Bitcoin Core 0.16.3).

Softfork enforcing types:

- __MASF__ (Miner-activated softfork): A majority of miners upgrade to enforce new rules.
- __UASF__ (User-activated softfork): Full nodes coordinate to enforce new rules, without support from miners.

Given a set of valid blocks, you can take any subset from it and that subset will also be valid. But in a softfork, only a subset of blocks that were previously valid remain so. Often softforks make certain transactions invalid (example: it could make any transaction that is more than 1KB invalid). The [P2SH](https://en.bitcoin.it/wiki/P2SH) (Pay-to-Script-Hash) was a softfork.

**BFT** (Byzantine Fault Tolerance): Ability of a distributed computer network to remain fault tolerant with valid consensus despite imperfect information or failed components of the network. Prior to BTC, the only way to maintain a BFT, P2P (Peer to Peer) network was by employing a closed or semi-closed group of nodes (selected using a different method than Nakamoto consensus). 

- In [pBFT systems](https://blockonomi.com/practical-byzantine-fault-tolerance/), the consensus model only works in small groups of closed nodes (~50) with substantial communication overhead, which prevent operating at scale. Achieving consensus in systems with arbitrary faults usually requires a specific voting system to help achieve consensus. 

  - In cryptocurrencies using pBFT, the block leader is selected through a voting process and replaced in a round-robin style format each round (no mining system, the leader select the next block, and 2/3 of other nodes have to approve it). This doesn't work well with BTC (thousands of nodes, connection/disconnection at will, malicious participants). Maintaining BFT in Bitcoin (open, distributed, large network) requires rules relying on cryptography and game theory mechanics in order to create a trustless environment necessary for a decentralized consensus.

**Nakamoto consensus**: Set of rules, in conjunction with the PoW consensus model in the network, that govern the consensus mechanism and ensures its trustless nature (consensus build agreement among a network of mutually distrusting participants). Blockchain wouldn't be so powerful without it. It's applied to distributed ledger systems. This made Bitcoin the first BFT open and distributed P2P network that uses a distributed network of anonymous nodes that are free to join and leave the network at will. The PoW adds a cost to participate and discourage malicious actions. Nakamoto consensus is made of 4 parts:

- **PoW**: Designed to prevent double spending (the signature scheme within the UTXO model provides the verifiable ownership of transaction outputs to be spent, but doesn't prevent double spending). The more computing power you have in the network, the more likely you are to mine a block. Thus, the largest blockchain is considered the valid one because it came from the largest pool of computational power. As long as the longest chain and majority of network's hashing power is controlled by hones nodes, the hones chain will grow the fastest. Once a miner finds the PoW for a block, he proposes the block to the network, the network validates it if all transactions are not double spent, and it's added to the longest chain. Since BTC's network is massive, the cost of a 51% attach is enormous.

- **Block selection**: Miners compete to win the block reward for mining the next block. The block leader is not selected through a voting process (unlike in pBFT), but by solving a cryptographic puzzle (increment a nonce in the block until the block's hash have the required number of 0 bits at the beginning). The first miner to find the solution wins and can propagate the block across the network so other mining nodes add it to the longest chain. The process is random and the leader cannot be predicted. The more hashing power, the more probabilities to win, but the more costly to participate. 

- **Scarcity**: BTC's has a limited total supply (21 millions), and it can only be injected into the system through the mining process where the block reward is halved every 210.000 blocks (~4 years).

- **Incentive structure**: BTC's deflationary nature incentivise participants to secure and validate the network, to support BTC's growth in value, and to cooperate. The block reward incentivise miners to validate and secure the network honestly. Nakamoto consensus 


## Nodes

**Node**: Computer that is participating in the global Bitcoin network by speaking a protocol called Bitcoin (a P2P protocol that allows nodes to communicate to each other to propagate transactions and blocks everywhere). A node that wants to advertise his presence listens on specific ports in a way that can be discovered (but many more aren't doing this, or are hidden behind protocols such as Tor, or listening to hidden ports). Anybody can run a node. Nodes validate the consensus rules, not miners. Miners take the transactions nodes decided were valid and give back blocks.

- **Full node** (or fully validating node): Node that validates every transaction and block. Optionally, it can keep a full copy of the blockchain. It communicates, by a random process of connection, with a set of peers that it chooses from the network. When it receives a block or transaction from a peer, it independently verifies it (nodes don't trust each other): it reconciles it with his copy of the ledger and determines if funds were double spent. If the block or transaction verified is incorrect, the node rejects it and stops talking to that peer for a period of time that depends on the level of the offense (ban for 1h, 24h, permanet, etc.). 

**Node**: Every participant in a coin's network. It has specific hardware in order to host or connect to one. Blockchain technology is decentralized, based in a P2P network, with no dedicated servers, not one authority, but a consensus among users. BTC has 2 types of nodes:

- **Full node**: Stores a copy blockchain and thus guarantee the security and correctness of the data on the blockchain by validating data.
- **Lightweight node**: Each user participating. He needs to connect to a full node in order to synchronize to the current network state and participate.

**Consensus**: Rules by which a blockchain network operates and confirms the validity of information written in blocks and/or work performed. Most common consensus are **PoW** (Proof of work) and **PoS** (Proof of stake). 

**Node**: The blockchain relies on full nodes for enforcing rules and validating transactions. Anyone can become a full node (the more there are, the more decentralization and security). In a **51% attack** more than half the network power is concentrated in a single entity (leading to monopoly), allowing it to change consensus and forcing everybody to follow new rules, hardfork, or abandon. However, for the network to evolve, alterations need to be voted on by the community. Types of node:

- **Full node**: Acts as a server in a decentralized network. It maintains consensus between other nodes, verifies transactions, and stores a blockchain copy. It enables custom functions (instant send, private transactions...). When deciding the future of the network, full nodes vote on proposals. If more than 51% don't agree, the proposal is skipped (in some cases, a hardfork may happen, like [Bitcoin Cash Fork](https://coin.info/bitcoin-cash/#forks-tokens)). Two types of full nodes:

  - **Pruned node**: It begins downloading blocks from the beginning and once it reaches the set limit, deletes the oldest ones, retaining only their headers and chain placement. In order to get it, you would first have to go through the entire blockchain to validate all the previous blocks. This node still can verify transactions and be involved in the consensus.

  - **Archival node**: Server which hosts the full blockchain in its database. Different types:

    - Nodes that **can add blocks** to the blockchain: They depend on the consensus rules being enforced and require at least one full archival node to operate.

      - **Mining node** (miner): Full or lightweigh. It aims to prove that they've completed the required work to create a block (PoW). It has to be either full archival node itself or receive data from other full nodes to know blockchain's status and required parameters for the next block. The first to solve the cryptographic problem broadcasts his result to the network so it can be verified by full nodes and, once consensus is achieved, he can add it to the blockchain. Then, the miner gets a reward of a pre-defined amount of coins (coinbase) plus the transaction fees. The coinbase transaction is the first one in the block, included there free or charge by the miner that created the block.

      - **Staking node** (staker): Staking is similar to hold coins while in return receiving an interest back as a reward. Staking is like a lottery. It has a lower entry barrier, but offers less certainty compared to mining. Who will create the next block and get rewarded depends on some pre-defined rules and luck change factored in. Factors include coin age (how long you've had your coins), amount of coins you have, and their ratio to available ones in the network. You don't need expensive machinery, just keeping your wallet online 24/7. You need to be a full archival node. This is a solo endeavor due to lack of transparency in staking pools.

    - Nodes that **cannot add blocks** to the blockchain:

      - **Authority node**: If we allow some centralization (less trust, easier to attack), we can gain some benefits (increased speed, no storage required, easier to upgrade...). There're a few consensus algorithms for this (Delegated proof of stake, Delegated BFT, Proof of authority, etc.). A fixed number of these nodes have to be defined (set by development team or voted by the community). Their task is to create and validate blocks, while distributing information to users on the network. The rest of participants run lightweight nodes, which depend on the broadcasted data to be able to operate on the blockchain.

      - **Masternode**: Cannot add blocks to the blockchain. It just keeps a record of transactions and validate them. It makes the network more secure and can earn a share of the rewards for his services. It requires to lock away some funds as collateral. It's expected to be online 24/7. Hosting on a Virtual Private Server is good practice. 

- **Lightweight node** (SPV node: Simple Payment Verification node): Used in day to day operations. It communicates with the blockchain while relying on full nodes to provide them with the necessary information. They only query the last block's status and boradcast transactions for processing. It doesn't require many resources, but sacrifice security for convenience.

- **Lightning node**: It connects with users outside the blockchain, reducing the network's load, shortening transfer times, and increasing usability. Transaction fees are really low. It opens a separate payment channel between entities. Instead of waiting for each transaction to be confirmed and filling the network with space-wasting data, parties can interact between each other and lower the load on the blockchain. Furthermore, if someone else wants to deal with the same party, the lightning network will search for a path with the least number of intermediaries and lowest transfer fees, thus reducing wait times.

**Forks**: If there's not at least 51% agreement between full nodes, a proposed change to the network is rejected. But, if a developer implements the proposed change and a large part of the community accepts and supports it, a fork happens. Two types:

- **Hard fork**: Change to the network consensus algorithm. Every alteration not compatible with the previous version of the client used (new block reward, block time, transition from PoW to PoS, implementation of masternodes...). After launching a hardfork, every not updated node is rejected by the consensus since it's operating on invalid rules. Many developers and communities avoid major changes because some people may be left out or the transition may compromise the network's security.

- **Soft fork**: Alteration that has no mandatory rule for users to update their nodes. 

  - Example: BTC's Segregated Witness feature. Transactions can be made with or without using this feature but, once 95% of clients are updated to the version that supports SegWit, the consensus will automatically refuse any old transactions without it, making it a smoother transition that doesn't force users to immediately update.

**VPS** (Virtual Private Servers): Using it with your node is optional. In exchange for a small payment, it protects your node from DDoS attacks, not having to maintain any hardware and not worry about your bandwidth capabilities. Otherwise, somebody could hack into your server and steal your funds, providing you're storing your coins in those wallets.


## Proof of work and consensus

**Byzantine generals' problem** (1982): A group of generals, which are separated from each other, have to agree on their next move. Each one has one vote (attack or retreat). After casting a vote, it cannot be changed. All generals have to agree on the same decision and execute it in coordination. They communicate via messages, which can be delayed, destroyed, or lost. Some generals may send a fraudulent message to confuse the rest, leading to a system failure. In a blockchain, each general is a node, and they need to reach consensus on the current system 's state (i.e., the majority of participants must agree on and execute the same action).

**BFT** (Byzantine Fault Tolerance): A BFT system is capable of resisting the types of faults derived from a Byzantine generals' problem (i.e., it's still operative even when some nodes act maliciously or fail to communicate). There're different ways to build a BFT blockchain, depending upon the consensus algorithm used (PoW, PoS, Delegated PoS...).

**Consensus algorithm**: Mechanism through which a blockchain network reaches consensus. While the protocol (Bitcoin) defines the rules, the consensus algorithm (PoW) determines how these rules will be followed. Satoshi used a modified PoW version that made BTC a BFT system. Although PoW is not 100% fault tolerant, it proved to be one of the most secure implementations for blockchain networks. Consensus algorithms still need to overcome some limitations.

**Consensus achievement**: This is when participants in the network agree on the current state of the blockchain.

**PoW** (Proof of Work): Proof that you engaged in a significant amount of computational effort. Usually, it's a proof that you solved a puzzle that is difficult to solve but easy to verify. PoW has been used for deterring spam email or DoS attacks (someone that wants to send a huge amount of messages has to spend too many CPU cycles, which may be expensive). 

- In BTC, the puzzle is: you have to find a number (PoW) such that, when attached to you message (block) and applied a hash function to it, the result is a hash (set of bits) with X number of leading zeros. The best way to find this number is by brute force (test numbers until one outputs the correct result). Verifying the PoW is easy (just hash the message + number and check the leading zeros). The difficulty can be adjusted by changing the number of required zeros. Example: if 15 zeros are required, the probability of finding the number is 2<sup>15</sup>.

**51% attack** (majority attack): The PoW consensus algorithm ensures that miners can only validate a new block if the network nodes collectively agree on its validity. A miner's performance depends on the amount of computational power it has (also called hash rate, or hashing power). The mining power is distributed over many nodes across the world. However, if a single entity can obtain more than 50% hashing power, it could cause network issues such as:

- Exclude or modify order of transactions
- Reverse transactions (allowing double spending)
- Prevent some or all transactions from being confirmed
- Prevent miners from mining

Nevertheless, the attacker won't be able to do some other things such as:

- Reverse other user's transactions
- Prevent transactions from being created and broadcasted
- Change block's reward
- Create coins
- Steal coins that never belonged to him

The bigger the network, the stronger the protection against these attacks. The more valuable BTC becomes, the more miners go to compete for the rewards, which gives miners no incentive to invest large amounts of resources if they're not acting honestly. The bigger the chain, the more difficult to change old blocks because that requires to discard all subsequent blocks. The more confirmations a block has, the greater the cost of altering or reversing it. A successful attack would probably only be able to modify the transactions of a few recent blocks for a short period of time.


## Bitcoin wallets

**BTC wallet**: Program that sends, receives, and stores BTC, and monitors BTC balances. Program used for managing your BTC. It interfaces with the blockchain (ledger of BTC transactions). It monitors addresses in the blockchain and update their own balance with each transaction. 

**Private/Secret key** (SK): Large string of numbers and letters that acts like a password to your wallet. The SK makes your wallet capable of sending your BTC. Whoever knows your SK has power over your BTC. The SK is also used to generate your BTC address, which you give out to people who want to send you BTC. The wallet's core function is the creation, storage and use of the SK (it automates BTC's complex cryptography for you). A standard BTC wallet creates a `wallet.dat` file containing its SK.

You can use a software for generating a SK and PK. The PK is used to generate a unique BTC address. This address is provided to those who want to pay you, so they can transfer BTC from their addresses to your address. The SK is used for signing new transactions and accessing your funds. The SK can be used to recover the PK and BTC address. However, most modern wallets use a seed phrase (see HD wallet below).

**HD wallet** (Hierarchical Deterministic wallet): It generates an initial phrase (mnemonic phrase, seed) made of common words, which is easier to memorize than the SK. If your wallet gets destroyed or stolen, you can enter the seed to reconstruct the SK. This wallet can create, from the same seed, multiple SKs. Thus, it can create multiple BTC addresses, being all of them part of the same wallet.

**Multisig wallet** (Multi-Signature wallet): It allows sending BTC only with the approval of enough SKs. Example: 3 SKs can share a multisig wallet, so sending BTC is only possible with the approval of 2 SKs (often used by escrow services).

There're different types of wallets, each one establishing a compromise between security and convenience:

- Classification based on **weight**:

  - **Full node**: Wallet that stores a blockchain's copy in order to validate every transaction.

  - **Light wallet**: Doesn't hold a blockchain's copy. It relies on full nodes it's connected to in order to validate transactions.

    - **SPV wallet** (Simple Payment Verification wallet): Faster. Consumes less disk space.

- Classification based on **SK storage**:

  - **Hot wallet** (software wallet): Connected to the Internet. Least secure wallet. More convenient.

    - **Web wallet**: Least secure wallet (multiple attack vectors). It relies on a third party and you don't have access to the SK (it's like asking somebody to hold you coins for you). Often used by web services (markets, exchanges, betting site...) that require you to deposit funds on their online wallets. It's convenient for operating fast. Some provide multi-factor authentication for protecting against hackers. It's recommended to use it only for small amounts.

    - **Desktop wallet**: Stores SK in your computer. Requires a malware free computer (which isn't easy). 

    - **Mobile wallet**: Mobile app. Stores SK in your mobile phone. Low security. Low privacy (potential association of your wallet, phone number, and geo-location). Multi-factor authentication is advised. Very convenient, but it's recommended for small amounts.

  - **Cold wallet**: Most secure wallet. Independent from any Internet connection, so it's resistant to hackers. Suitable for long term investors. More secure. Less convenient. 

    - **Hardware wallet**: Physical device that safely store the SK and PK (both generated with a RNG: Random Number Generator). It cannot be hacked even if your device is compromised by malware. It can be safely used with any machine. Most of them provide a seed backup in case it's lost or stolen.

    - **Paper wallet**: Piece of paper with the SK (or seed) and blockchain address printed out (usually, as QR codes). It cannot send partial funds, only all of them at once. Considered obsolete and unreliable.

    - **Brain wallet**: Generate a SK from a chosen text or set of words. You decide your own passphrase and then use an algorithm for generating a SK from it. It's less secure because we are very predictable. 

The more convenient a wallet is, the more unsecure becomes, and viceversa. Use secure wallets for holding large amounts, and convenient wallets for small and regular expenses.


## Bitcoin whitepaper

- [Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf)
- [Explanations](https://static1.squarespace.com/static/567bb4f069a91a95348fa0b2/t/5cd27c8bb208fcb3a45d2196/1557298317565/Intrepid+Ventures+Bitcoin+White+Paper+Made+Simple.pdf)

### Abstract

A pure P2P electronic cash would allow online payments without going through a financial institution. Digital signatures solve part of the problem, but a third party is still required for preventing double-spending. To solve the double-spending problem we propose using a P2P network that timestamps transactions by hashing them into an ongoing chain of hash-based PoW, creating a record that cannot be changed without redoing the PoW. Thus, the longest chain comes from the largest pool of CPU power and is proof of the sequence of events. As long as a majority CPU power is controlled by nodes that don't cooperate to attack the network, they will generate the longest chain and outpace attackers. The network requires minimal structure. Messages are broadcast on a best effort basis. Nodes can leave an rejoin the network at will, accepting the longest PoW chain as proof of what happened when gone.

### Introduction

Commerce on the Internet relies on financial institutions serving as trusted third parties to process electronic payments. Completely non-reversible transactions are not possible because financial institutions mediate disputes. Problems:

- The cost of mediation increases transaction costs, which prevents small transactions.
- There's a cost for not being able to make non-reversible payments for non-reversible services.
- Merchants have to ask for more information about the customer than they would otherwise need.
- Some percentage of fraud is accepted as unavoidable.

It's needed an electronic payment system, not based on trust but on cryptographic proof, allowing two parties to transact directly without a trusted third party. Non-reversible transactions are would protect sellers from fraud. Routine escrow mechanisms could easily be implemented to protect buyers. We propose a solution to the double-spending problem using a P2P distributed timestamp server to generate computational proof of the order of transactions. The system is secure as long as honest nodes control more CPU power than any cooperating group of attacker nodes.

### Transactions

__Electronic coin__: Chain of digital signatures. Each owner transfers the coin to the next by digitally signing a hash of the previous transaction and the PK of the next owner and adding these to the end of the coin. A payee can verify the signatures to verify the chain of ownership.

However, the payee cannot verify that one of the owners did not double-spend the coin. A common solution is to go through a trusted central authority (mint) that checks every transaction for double spending. The payee have to know that the previous owners didn't sign any earlier transactions, which can only be known by being aware of all transactions (the mint is aware). To accomplish this without a trusted party, transactions must be publicly announces, and participants have to agree somehow on a single story of the order of received transactions. The payee needs proof that at the time of each transaction, the majority of nodes agreed it was the first received.

### Timestamp server

The proposed solution is a timestamp server that takes a hash of a block of items to be timestamped and widely publish the hash. Each timestamp includes the previous timestamp in its hash, forming a chain, with each additional timestamp reinforcing the ones before it.

### Proof-of-Work

To implement a distributed timestamp server on a P2P basis, we need to use a PoW. This PoW involves looking for a value that when hashed, the hash begins with a number of zero bits. The average amount of work required increases exponentially with the number of zeros, but can be easily verified by executing a single hash. We implement the PoW by incrementing a nonce in the block until a hash with the required number of leading zeros is found. Once this work is done, the block cannot be changed without redoing the work. Since later blocks are chained after it, changing the block would included redoing all the subsequent blocks.

The PoW also determines representation in majority decision making. Considering one-IP-address-one-vote, anyone able to allocate many IPs could subvert the majority. PoW is one-CPU-one-vote, so the majority decision is represented by the longest chain, which has used the most PoW effort. If a majority of CPU power is controlled by honest nodes, the honest chain will grow the fastest. An attacker that wants to modify a past block would have to redo the PoW of the block and all subsequent blocks, and surpass the work of the honest nodes.

If blocks are generated too fast, the PoW difficulty will be adjusted.

### Network

Steps to run the network:

1. New transactions are broadcast to all nodes
2. Each node collects new transactions into a block
3. Each node work on finding a difficult PoW for its block
4. When a node finds a PoW, it broadcasts the block to all nodes
5. Nodes accept the block only if all transactions in it are valid and not already spent
6. Nodes accept the block by working on creating the next block using the hash of the accepted block as the previous hash

Nodes always consider the longest chain the correct one and keep working on extending it. If two nodes broadcast different versions of the next block simultaneously, some nodes may receive one of them first, so they work on the first one received but save the other branch in case it becomes longer. When the next PoW is found and one branch becomes longer, the nodes that were working on the other branch switch to the longer one.

New transaction broadcasts don't necessarily need to reach all nodes: If they reach many nodes, they will get into a block before long.

If a node doesn't receive a block, when he receives the next block he will realize that he missed one, so he will request it.

### Incentive

The first transaction in a block is special because it creates a coin owned by the block's creator. This incentivises nodes to support the network, and initially distributes coins into circulation. Nodes are also incentivised with transaction fees: if the output value of a transaction is less than its input value, the difference is a transaction fee. These incentives may encourage nodes to stay honest (a greedy attacker with more CPU power than all the honest nodes my find more profitable to play by the rules than undermining the system and the validity of his own wealth).

### Reclaiming disk space

Once the latest transaction in a coin is buried under enough blocks, the spent transactions before it can be discarded to save disk space. To facilitate this without breaking the block's hash, transaction are hashed in a Merkle tree, with only the root included in the block's hash. Old blocks can be compacted by stubbing off branches of the tree (i.e., interior hashes). A block header with no transaction would have about 80 bytes. If we suppose blocks are generated every 10 minutes, 80 bytes * 6 * 24 * 365 = 4.2 MB/year.

### Simplified payment verification (SPV)

It's possible to verify payments without running a full network node. A user only needs a copy of the block headers of the longest PoW chain, which can get by querying network nodes until he's convinced he has the longest chain, and obtain the Merkle branch linking the transaction to the block it's timestamped in. He can't check the transaction for himself, but by linking it to a place in the chain, he can see that a network node has accepted it, and blocks added after it further confirm the network has accepted it.

The verification is reliable as long as honest nodes control the network. While network nodes can verify transactions for themselves, the simplified method can be fooled by an attacker's fabricated transactions for as long as the attacker can continue to overpower the network. One strategy to protect against this would be to accept alerts from network nodes when they detect an invalid block, prompting the user's software to download the full block and alerted transactions to confirm the inconsistency.

- **FPV wallets** (Full Payment Verification wallets, or heavyweight wallets: It requires a complete copy of the blockchain and can verify transactions.
- **SPV wallet** (Simplified Payment Verification wallet, or lightweight wallet): It doesn't have a full copy of the blockchain and cannot check whether transactions are valid. But it can send and receive BTC, and verify a transaction. 

### Combining and splitting value

Making a separate transaction for every cent in a transfer would be highly inefficient. To allow value to be split and combined, transactions contain multiple inputs and outputs. Normally there will be either a single input (from a larger previous transaction) or multiple inputs (combining smaller amounts), and at most two outputs (one for the payment, and one returning the change back to the sender).

When a transaction depends on several transaction, and those transactions depend on many more, is not a problem here because there's never the need to extract a complete standalone copy of a transaction's history.

### Privacy

The necessity to announce all transactions publicly prevents some privacy. However, privacy can still be maintained by keeping PKs anonymous (so nobody can link a transaction to anyone). Additionally, a new key pair should be used for each transaction to keep them from being linked to a common owner, though some linking is unavoidable with multi-input transactions (which reveal that their inputs were owned by the same owner).  

### Calculations

An attacker that manages to generate an alternate chain faster than the honest chain cannot make arbitrary changes: he cannot create value out of thin air, nor take money that never belonged to him. Nodes won't accept invalid transactions as payment, and honest nodes will never accept a block containing them. An attacker can only try to change one of his own transactions to take back money he recently spent.

There's a race between the honest chain and the attacker's chain. If the probability of an honest node finding the next block is bigger than an attacker finding it, the probability of the attacker catching up drops exponentially as the number of blocks the attacker has to catch up with increases.

An attacker may make a transfer, trying to make the recipient believe he paid him for a while, and then switch it to pay back to himself after some time passed.

### Conclusion

Coins made from digital signatures provide strong control of ownership. To prevent double-spending, we use a P2P network using PoW to record a public history of transactions that an attacker cannot change if honest nodes control most CPU power. Nodes work with little coordination. Nodes don't need to be identified since messages are not delivered to any particular place and only need to be delivered on a best effort basis. Nodes can leave and rejoin the network at will, accepting the PoW chain as proof of what happened while gone. They vote with their CPU power, expressing their acceptance of valid blocks by working on extending them and rejecting invalid blocks by refusing to work on them.

### Key points

- **Digital signatures** prevent fraudulent payments. A payer must sign his payment, so nobody else can pay in his place. Also useful for proving ownership of a certain address without revealing the sk.
- **Double spending problem** is usually solved via intermediaries, but it has some issues (reversible transactions, increased costs...). Satoshi solves this without requiring an intermediary.
- **Blockchain** is a decentralized database that is continually updated with sets of transaction (blocks). 
- To prevent double spending, the network has to agree on the order of transactions. All transactions in a block occur simultaneously.
- **PoW** prevents DoS attacks and spamming (by determining valid blocks), distributes fees and rewards (minting) randomly to miners, gives some time for gathering transactions in a block, and allows the most honest chain to grow faster (if honest nodes control most of the CPU power).
- Fees and block rewards incentivise mining (and disincentivise double-spending), which is necessary for supporting the network. Block rewards is the way of initially distributing coins.


## Extending bitcoin
## Scalability
## Advanced bitcoin
## Future of Bitcoin
## FAQ





## References:

- Harsh Strongman (2022) **Teach yourself crypto**. Retrieved from [teachyourselfcrypto.com](https://teachyourselfcrypto.com/).

- [**History and evolution of money**](https://lifemathmoney.com/the-history-and-evolution-of-money/)
- **Introduction**
  - [How does BTC actually work?](https://www.youtube.com/watch?v=bBC-nXj3Ng4)
  - [Bitcoin - Cryptographic hash function](https://www.youtube.com/watch?v=0WiTaBI82Mc)
  - [How secure is 256 bit security?](https://www.youtube.com/watch?v=S9JGmA5_unY)
  - [Public key cryptography](https://www.youtube.com/watch?v=GSIDS_lvRv4)
  - [What are digital signatures?](https://www.youtube.com/watch?v=s22eJ1eVLTU)
  - [The GNU privacy handbook](https://gnupg.org/gph/en/manual.pdf)
- [**Basic concepts**](https://youtu.be/FYo5E7zT-vM)
- **Decentralized consensus**
    - [Bitcoin blockchain consensus](https://www.youtube.com/watch?v=f1ZJPEKeTEY)
    - [Consensus definition](https://en.bitcoin.it/wiki/Consensus)
    - [Fork definition](https://en.bitcoin.it/wiki/Fork_(disambiguation))
    - [Nakamoto consensus](https://blockonomi.com/nakamoto-consensus/)
- **Nodes**
  - [Role of nodes](https://www.youtube.com/watch?v=fNk7nYxTOyQ)
  - [Types of nodes and forks](https://nodes.com/)
- **Proof of work and consensus**
  - [Byzantine fault tolerance](https://www.youtube.com/watch?v=VWG9xcwjxUg)
  - [Proof of work](https://www.youtube.com/watch?v=9V1bipPkCTU)
  - [A 51% attack](https://www.youtube.com/watch?v=BuTj9raHQOU)
- **Bitcoin wallets**
  - [Bitcoin wallet](https://www.youtube.com/watch?v=A1Pl5hYHXiI)
  - [Wallets: Visual explanation](https://www.youtube.com/watch?v=d8IBpfs9bf4)
- **Bitcoin whitepaper**
  - [Bitcoin white paper](https://bitcoin.org/bitcoin.pdf)
  - [Bitcoin white paper made simple](https://static1.squarespace.com/static/567bb4f069a91a95348fa0b2/t/5cd27c8bb208fcb3a45d2196/1557298317565/Intrepid+Ventures+Bitcoin+White+Paper+Made+Simple.pdf)
- **Extending bitcoin**
  - [BIP approval process](https://www.youtube.com/watch?v=NJqAuZGg1gU)
  - [BIP list (for reference)](https://github.com/bitcoin/bips)
  - [Layer 2 solutions](https://www.cryptovantage.com/news/ask-cryptovantage-what-is-bitcoins-layer-2/)
- **Scalability**
  - Lightning network
    - [Introduction](https://www.youtube.com/watch?v=rrr_zPmEiME)
    - [Understanding the bitcoin lightning network](https://jaspa.codes/site/2021/01/11/lightning-network.html)
    - Understanding the Lightning network [[Part 1](https://bitcoinmagazine.com/technical/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791)] [[Part 2](https://bitcoinmagazine.com/technical/understanding-the-lightning-network-part-creating-the-network-1465326903)] [[Part 3](https://bitcoinmagazine.com/technical/understanding-the-lightning-network-part-completing-the-puzzle-and-closing-the-channel-1466178980)]
  - Segwit
  - Block size increase (Bitcoin Cash, Bitcoin Satoshi Vision)
  - Schnorr signatures
  - Side chains
  - Colored coins
    - [Omni layer](https://www.omnilayer.org/)
- **Advanced bitcoin**
  - Transactions (pre-Segwit) [[Part 1](https://www.youtube.com/watch?v=Em8nJN8IEes&t)] [[Part 2](https://www.youtube.com/watch?v=f9nxuhLSyOg)]
  - Segwit
    - [Transaction malleability](https://www.coindesk.com/bitcoin-bug-guide-transaction-malleability)
    - [What is Segwit](https://www.youtube.com/watch?v=f3CFUbeehc8)
  - [The script language](https://youtu.be/6Fa04MnURhw)
  - [More Segwit](https://medium.com/softblocks/segregated-witness-for-dummies-d00606e8de63)
  - Merkle trees
    - [Merkle roots and Merkle trees](https://www.youtube.com/watch?v=gUwXCt1qkBU)
    - [Merkle proofs](https://www.youtube.com/watch?v=2kPFSoknlUU)
    - [Data corruption and Merkle trees](https://www.youtube.com/watch?v=rsx1nt2bxf8)
    - [How SPV nodes use Merkle trees](https://www.yourdevopsguy.com/merkle-trees-and-bitcoin/)
    - [How SPV nodes communicate with full nodes](https://www.youtube.com/watch?v=WSlvBfLGU5I)
  - Bloom filters
    - [What are bloom filters and why they exist](https://www.youtube.com/watch?v=gBygn3cVP80)
    - [Bloom filters and SPV nodes within the Bitcoin blockchain](https://tara-annison.medium.com/bloom-filters-and-spv-nodes-within-the-bitcoin-blockchain-66c36ea673f2)
    - [Bloom filters and SPV](https://www.yourdevopsguy.com/bloom-filters-and-bitcoin/)
  - [Elliptic curve cryptography](https://www.youtube.com/watch?v=dCvB-mhkT0w)
- **Future of Bitcoin**
  - [Quantum computing risks](https://www.youtube.com/watch?v=wlzJyp3Qm7s)
  - [Schnorr signatures](https://bitcoincore.org/en/2017/03/23/schnorr-signature-aggregation/)
  - [Taproot](https://bitcoinmagazine.com/technical/taproot-coming-what-it-and-how-it-will-benefit-bitcoin)
- **FAQ**
  - [Can you spend unconfirmed receipts?](https://bitcoin.stackexchange.com/questions/69937/accidentrally-spent-from-unconfirmed-transaction)
  - [What happen if your transaction is never confirmed?](https://bitcoin.stackexchange.com/questions/21901/what-happens-if-your-transaction-is-never-confirmed)
  - [Why does each block store a Merkle root?](https://bitcoin.stackexchange.com/questions/48928/why-does-each-block-store-a-merkle-root)
  - [What's the difference between SegWit and Native SegWit address?](https://www.ledger.com/academy/difference-between-segwit-and-native-segwit)
  - [Electrical consumption](https://news.bitcoin.com/bitcoin-energy-consumption-is-far-more-efficient-and-greener-than-todays-banking-system/)
  - [Coins and Tokens](https://www.youtube.com/watch?v=c7TsIb8KyB8)
  - [Incentives](https://www.youtube.com/watch?v=Q8KtQ3uM1tk)
  - [Is Bitcoin ruled by miners?](https://en.bitcoin.it/wiki/Bitcoin_is_not_ruled_by_miners)
  - [What is economic majority?](https://en.bitcoin.it/wiki/Economic_majority)
  - [Common myths about Bitcoin](https://en.bitcoin.it/wiki/Myths)
- **History**
  - [Bitcoin auction: 10.000.000 BTC - Starting bid 50.00 USD](https://bitcointalk.org/index.php?topic=92.0)
  - [The Bitcoin pizza](https://www.cryptowisser.com/the-story-of-the-bitcoin-pizza/)
  - [History of Bitcoin](https://en.wikipedia.org/wiki/History_of_bitcoin)
  - [Mt. Gox](https://www.youtube.com/watch?v=9lJP22qa6Ak)
  - [The long road to SegWit](https://bitcoinmagazine.com/technical/the-long-road-to-segwit-how-bitcoins-biggest-protocol-upgrade-became-reality)
  - [Bitcoin Cash (BCH)](https://en.wikipedia.org/wiki/Bitcoin_Cash)
  - [Bitcoin SV (BSV)](https://www.youtube.com/watch?v=4VWtZpIJPRM)
  - Satoshi Nakamoto