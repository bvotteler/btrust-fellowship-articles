# Lightning Payments: When Dust Means Trust
Lightning's goal is to enable economical small payments when compared to its base layer while retaining that layer's security properties by settling on-chain.  
As we would expect, that requires some trade-offs. Let's look at one of those aspects: Why spending small amounts (aka. dust) requires trust. Let's start at the base layer.

## Dust Limit on Bitcoin
If an unspent output becomes too small to be economically spendable, ie. the fees would eat up all or too much of the output, then it is considered dust. Another issue is that those outputs, by being unspendable, may remain in the UTXO set forever and, in turn, the data to track it is effectively dead weight that each full node has to carry forward.

In order to combat dust, the reference node implementation, bitcoin-core, introduced a simple rule: If a potential output of a transaction submitted to the mempool is below the dust limit, it will reject it.  
So, how is that dust limit calculated?

In effect, the dust limit for bitcoin-core is calculated as:
`dust = (input_vsize + output_size) × 3 sat/vB`
For more details see [this stackexchange answer](https://bitcoin.stackexchange.com/a/41082) by Murch.

In the code itself, this is represented by using a parameter `-dustrelayfee` argument which [defaults](https://github.com/bitcoin/bitcoin/blob/0e9018e8b65611b0769545e177110e4b7fc51244/src/policy/policy.h#L68) to `3000` since the parameter is kept in `sats/kvB` (Sats per *kilo*-vByte, therefore, `3 sat/vB = 3000 sat/kvB`).  
Take note that this is not calculated from current market fees, but a fixed assumption of fees of about `1 sat/vB` and then the cost should not be more than a third of the value of the UTXO.

## Bitcoin's Incentive: More Fees Over Time
Bitcoin's [security budget](https://www.spark.money/glossary/security-budget) is dependent on fees and subsidies paid to all miners in the network. And with the reduction of subsidies by every halving until stopped entirely, this means that fees will have to make up for the shortfall over time for the security budget to remain at least stable.

This also means that we should expect dust limits to increase over time. Right now, the default sits are `3 sat/kvB`, but each node operator can increase (or decrease) that and future releases may decide to use a higher default over time.

We can therefore say, it is in Bitcoin's best interest if fee rates keep increasing to provide a high enough security budget.

## Lightning's Reality: More Trust Required Over Time
A direct result of Bitcoin's incentive is that with higher fees, the dust limits would get increased over time. This, in turn, leads to more "everyday" spends as a percentage of all transactions on Lightning would fall under the dust limit.  
Great! That's exactly what we want Lightning to do: Make small purchases cheaper and, in this case, even possible. Even if we wanted to, we couldn't spend such small amounts on-chain. Those transactions would be rejected from entering the mempool. So where's the catch?  
The catch comes in a detail of how [LN Penalty](https://bitcoinops.org/en/topics/ln-penalty/) deals with such small amounts. But let's look at amounts above dust first.

When a payment is made, the paying node finds a route to receiving node, and sends the payment along those channels. Each of the nodes forward it to the next node. And in order to get paid, this is secured by [HTLCs](https://docs.lightning.engineering/the-lightning-network/multihop-payments/hash-time-lock-contract-htlc) traveling along the route until all nodes decide they are good and settle into a new state with fresh balances (and drop the HTLC again).  
The key thing is that during that process with above dust amounts, everyone has the ability to enforce a settlement by submitting a transaction with three outputs to be included on-chain: One each paying the balance of each participant of a channel and as third one the in-flight transaction's amount to one node if they can prove they have done "their bit" and the payment was received at the final destination, or to the sending side (after some delay) if the other side cannot prove it.

This is great, as those transactions are secured on the base layer, so funds are safe. However, for dust amounts being sent we can spot an issue: The two outputs holding the balances should be over the dust limit, but the in-flight one now is below dust. Therefore, the transaction securing it cannot use a separate, dust output. Otherwise, the transaction wouldn't be accepted into the mempool and no one's balances is safe anymore.

In that scenario, Lightning nodes use another approach: Trimmed Outputs.  
With trimmed outputs, the ongoing transaction amount is kept in a "cookie jar" of sorts that is the miner's fees. Or in other words, it is simply omitted, and once the in-flight transaction is agreed upon, the dust amount is shifted into one of the two balance outputs. For more details, see [BOLT #3](https://github.com/lightning/bolts/blob/master/03-transactions.md#trimmed-outputs) that defines how that is handled.

In such a scenario, one of the nodes can submit an in-flight transaction state to on-chain, and instead of the node who earned the fees those get sent to a miner. All to say: We now need to trust that nodes will finalize transactions in an honest way, rather than being able to enforce the rules. Hence why sending dust means you have to trust your channel partners.

## What is Being Done
Of course a lot of work is put into that field to address these shortcomings. And without going into detail and to keep this shorter, here are some of the things I am aware of currently being worked on to address the issue of requiring trust.

One of them are [Channel Factories](https://bitcoinops.org/en/topics/channel-factories/). The way they work in a nutshell:  
Instead of two nodes creating a transaction opening a channel on-chain, now a group of many nodes create a shared state transaction. And from that state, any two participants can open channels between each other using some of the balance they have in the overall state. The key difference is that in such a setup, the in-flight transactions are actually settled in Lightning and not on-chain. This removes the dust issues when HTLCs' in-flight amounts can be settled freely.  
The downside? It requires a lot of coordination and good behavior of all nodes. Even if on-chain transactions are available to resolve disputes, they are more costly and complex to set up.

Another in-development solution is using a new type of anchor, a new SegWit v1 script type, Pay to Anchor (P2A) in conjunction with a new relay policy, Topologically Restricted Until Confirmation (TRUC). Bitcoin core started supporting those with their October 2024 release (v28.0). Work is still underway in Lightning, so it is something to look out for in future.  
For more details on P2A, Murch has another detailed explanation of what they are meant to do and solve in his [reply on stackexchange](https://bitcoin.stackexchange.com/a/126119). And [BOLT #2](https://github.com/lightning/bolts/blob/master/03-transactions.md#shared_anchor-output-zero_fee_commitments) specifies its usage in shared anchors.

## Conclusion
While we all can enjoy the benefits of Lightning, the ease and speed of spending small amounts, we also need to keep in mind that those properties come at a cost. As long as we know there is a cost and in what form it can hurt us, we can make better decisions in our everyday use of the Lightning network.  
We should not delude ourselves, or worse, others by discarding the reality that transacting on Lightning isn't always trustless. But at the same time, requiring some trust is not necessarily a terrible thing, either. Far from it. Human societies have always needed trust to foster cooperation.

So be aware and continue to spend well. Choose on-chain when trustlessness matters most and Lightning when the stakes are not as high.
