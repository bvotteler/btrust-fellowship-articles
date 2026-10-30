# Privacy Limits of Silent Payments

## Introduction
Silent Payments can be public without making every donation public knowledge. At times, the hype forgets to mention the limits of that privacy.  
In this article, I will try to explain why the privacy doesn’t automatically follow the received sats when they’re spent.

I assume basic knowledge of how Silent Payments work. See [this article](https://silentpayments.xyz/docs/explained/), or [Satsie's zine](https://satsie.dev/zines/silentpayments.html) for a brief overview or as refresher.

## Why Silent Payments
The [motivation for BIP 352](https://github.com/bitcoin/bips/blob/master/bip-0352.mediawiki#motivation) says in its opening sentence:
> Using a new address for each Bitcoin transaction is a crucial aspect of maintaining privacy.

It provides just that and [a few additional goals](https://github.com/bitcoin/bips/blob/master/bip-0352.mediawiki#goals) while avoiding existing procedures of having to interact with the receiving party to obtain a new address, in order to protect the receiver's privacy.  
Even better, it also protects a sender's privacy, because a Silent Payment address can be used by anyone without leaving a trace of having requested an address from the receiver.

So, if Bob (the receiver) published a Silent Payment address, let's say to receive donations, Alice and any other senders with knowledge of the address can send donations and none of them can see which other addresses donated.
(At least not immediately. But we'll get to that in a bit.)

With Silent Payments, all Alice knows is that she sent her donation to an address that looks like any other taproot address no less. And that Bob controls the private key to spend it.  
So far, that is a big improvement over having a static address where donors cannot only see immediately how much Bob received, but also from how many addresses.

## More Benefits
Since the UTXO looks like any other taproot address, chain analysis won't be able to tell that this is a Silent Payment, either.  
It hides among all other taproot payments that use the same types of inputs that are allowed for Silent Payments. In a nutshell, those are inputs controlled by a single key and cannot be signed with different keys depending on conditions or output paths. The good news is, that encapsulates the majority of taproot transactions.

## Dangers of Chain Analysis Still Apply
Despite the initial privacy gains, Bob still needs to be vigilant when spending UTXOs from Silent Payments. The dangers of chain analysis still apply going forward.

As soon as Bob uses these outputs in a spend, such as consolidating the donations into one output, Alice could infer links between her donation and that of other donors when her output is used as one of several inputs.  
Any other derived piece of intelligence can be gained as with standard taproot outputs going forward.
From that point onward, anyone knowing that Bob controlled one key could make the same observations and come to assumptions about key control for other addresses involved in future transactions.

## Conclusion
The key takeaway is that Silent Payments do not "solve privacy", at least not holistically. Knowing the limits is half the battle if Bob's goal is maintaining an adequate level of privacy.

If your privacy preservation is important to you, you would still use a mix of privacy techniques going forward. CoinJoins, PayJoins, chain hopping, using Lightning, or what else have you.  
All come with their respective caveats, so a mix is advised.

Privacy in Bitcoin is a very deep rabbit hole. I am still exploring and learning more as I go along.  
To start learning more about available privacy tools, Kruw has an [excellent starting point](https://kruw.io/guide.html) on CoinJoins. For PayJoins, [payjoin.org](https://payjoin.org/docs/why-payjoin/privacy) has good resources. And to learn about privacy in Lightning, Spark has a [thorough resource](https://www.spark.money/research/lightning-network-privacy-analysis).

