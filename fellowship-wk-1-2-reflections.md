# Fellowship Lessons I: From Whitepaper to SegWit to Taproot and Implications on Privacy
The goal of this article is to give a glimpse into what the first 2 weeks of the [Btrust](https://www.btrust.tech/) Open Source Fellowship looks like.
It is my first-hand account of going through it in late 2026.

## What is the Open Source Fellowship?
Btrust's Open Source Fellowship follows is an accelerated program to get top graduates from Btrust's pathways to deepen their understanding of Bitcoin and, eventually, work on real Bitcoin open-source projects.  
The duration of the fellowship program is 12 weeks at the time of writing.

In my case, I qualified by graduating in the 2026 cohort for the [Rust for Bitcoiners](https://pathways.btrust.tech/03/rust-for-bitcoiners) pathway. This was only one of several pathways. If you are interested in becoming a Bitcoin open source dev, I can only encourage you to explore the options the [Btrust Builders program](https://www.btrust.tech/builders) has on offer.

## The First Weeks: Studying The Basics
Weeks 1 & 2 are dominated by reading. And a lot of it.  
This is to deepen our knowledge in the fundamentals of Bitcoin going as far back as the whitepaper, some of the history of Bitcoin development, the various types of nodes, and basics around the security model. This is further fleshed out with studying the innovations SegWit brought to Bitcoin (both in fixing TXID malleability and also better upgrade options in future), and learning about mining and network propagation. Finally, towards the tail end of the first 2 weeks, we learn about Taproot, Tapscript, Schnorr signatures and wallets.

## The Structure
The material itself is, quite fittingly, [entirely open source](https://github.com/chaincodelabs/seminars) and provided by Chaincode Labs. The fellowship provides the setting around it where we are grouped together with like-minded Bitcoin devs-in-training so we can share the experience of learning the material together.

So, instead of only studying the material in isolation, we are encouraged to take down notes and questions to then discuss those among each other both in 1-on-1 discussions as well as in small groups.  
Getting someone else's perspective on a tricky question helped shape my understanding a lot as early as during the first few days already.

## Implications for Privacy
Bitcoin evolved from the initial reference implementation in many ways. From the perspective of privacy, which is one of my key interests in the Bitcoin space, some of the changes were pivotal in nature.

At first, there was a fairly widespread belief that given Bitcoin's pseudonymous nature, privacy is all but guaranteed. As the public discourse surrounding the infamous dark net market, [Silk Road](https://en.wikipedia.org/wiki/Silk_Road_(marketplace)), heated up, the popular narrative was that payments were untraceable. That, of course, was a mistaken impression.  
Given the public nature of the blockchain and, therefore, the transactions that were included, the very nature of the UTXO (unspent transaction output) model demanded that a link can be established between them.

Even the [whitepaper](https://bitcoin.org/bitcoin.pdf) said as much in section 10:
> [..] a new key pair should be used for each transaction to keep them
from being linked to a common owner. Some linking is still unavoidable with multi-input
transactions, which necessarily reveal that their inputs were owned by the same owner. The risk
is that if the owner of a key is revealed, linking could reveal other transactions that belonged to
the same owner.

Therefore, breaking or obfuscating those links between inputs associated with an owner and their outputs to increase privacy would be key. At the very least, there would have to be ways to introduce uncertainty in associations made.

### Pre-SegWit
Before SegWit, the main way to achieve obfuscation was using [CoinJoins](https://en.bitcoin.it/wiki/CoinJoin) and [PayJoins](https://en.bitcoin.it/wiki/PayJoin). In a nutshell, both use multiple owner's UTXOs to construct a single transaction using those as inputs and sending them to multiple new outputs. This breaks the heuristic of "all keys required to sign all inputs belong to the same person/entity."  
But both options suffered from issues for wallets trying to know about those transactions: [transaction malleability](https://en.bitcoin.it/wiki/Transaction_malleability). Since wallets would keep a lookout for a specific transaction ID (txid), and anyone could modify a signature so it stays valid, but that change results in a different, calculated txid, this meant there were angles of attack to make someone lose track of a transaction output.

It is worth pointing out that while changing the signature through mathematical calculations was possible, it was not possible to change where the amounts came from or where it went to. It only affected the result of the calculated txid.

### SegWit Fixes Transaction Malleability
With the introduction of [SegWit](https://en.bitcoin.it/wiki/Segregated_Witness) (Segregated Witness), the signatures were moved into another area of the block, more importantly, they were removed from the set of fields that were used to calculate the transaction ID.  
And while SegWit didn't provide any direct privacy benefits, it did among other things such as making Lightning possible, it also stabilized the use of CoinJoins and PayJoins. Neither is a perfect panacea for privacy concerns, but they do represent a big step forward. So I will include that as a small, but crucial victory for better privacy.

Another crucial feature of SegWit was that it introduced "script versions" as a field. That seems innocuous at first, but has one out-sized beneficial effect: Future upgrades to newer versions could utilize that field and make it easier to introduce changes with fewer risks of [hard forks](https://en.bitcoin.it/wiki/Hardfork).  
And this version field was then used to eventually introduce...

### Taproot & Schnorr Signatures
Taproot was introduced as the next "version" utilizing the script version field SegWit introduced.  
From a privacy perspective, the introduction of Schnorr Signatures as part of that was a big win. In shorter terms, Schnorr signatures, unlike the existing elliptic curve signatures (ECDSA), have a mechanism called "key aggregation" where a set of disparate keys are condensed into another key that, for an outside observer, looks exactly the same a single key.

Not being able to discern a multi signature transaction from a single signature one might not seem like a big deal, but there are more applications that the technique allows. More generally, any information that is not provided is a good thing when it comes to privacy. For a more detailed explanation about Schnorr Signatures, I encourage you to read the excellent article by Lucas Nuzzi: [Schnorr Signatures & The Inevitability of Privacy in Bitcoin](https://medium.com/digitalassetresearch/schnorr-signatures-the-inevitability-of-privacy-in-bitcoin-b2f45a1f7287).  
And of course Taproot does not only provide a new signature, but also new ways to enable multiple spend options with different scripts in a more compact way than SegWit can do. For more on that, take a look at the "complex spending with Taproot" section in the [Bitcoin Optech Newsletter #46](https://bitcoinops.org/en/newsletters/2019/05/14/#overview-of-the-taproot--tapscript-proposed-bips).

## My Thoughts & Conclusion
So far, this program has been a challenge in deepening my understanding of Bitcoin that I accumulated over the past few years of casual study. It really takes it to the next level by providing some structure, fellows around me at similar knowledge levels and technical abilities.  
It's an eye-opener to chat through my perceptions of some technical text, forcing me to think more clearly to be able to articulate those thoughts. And in the same session, I get to hear how another fellow sees the very same text and comes away with some unique thoughts on a facet I hadn't even paid much attention to.

That range of perspectives from people who are continuing to study Bitcoin just as I am provided a lot of food for thought to revisit ideas I had formed over time.  
So, while I may stress the "a lot" bit when reading, well, *a lot*, it is well worth it because the program itself makes sure we also talk and think about it... yes, you guessed it: *A lot*. And I am looking forward in exploring more options of preserving privacy with existing and new ideas in the ecosystem.
