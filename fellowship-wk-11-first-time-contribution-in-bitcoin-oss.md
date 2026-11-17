# The Long Road to My First Bitcoin Open Source Contribution
Everything below is my real experience, the good, the bad, and the ugly.

Over the past 3 months, I had the privilege to be part of Btrust's 2026 [Open Source Fellowship](https://blog.btrust.tech/introducing-the-2026-open-source-fellowship/) program. That program had (still has) an immense impact on my trajectory of becoming a contributor.  
Reflecting on my journey so far is part of the program, so here I am sharing that. But at the same time, the journey did not start there.

## Start at the Beginning
I have been a software developer for a few decades. Without dating myself too readily, I started when PHP was still exciting devs.  
So it is somewhat surprising to me that I only really started noticing Bitcoin somewhere in late 2020 or early 2021. I noticed it, because it had somehow recovered from its crash that started in 2018. And that didn't match what I thought was a dead project.

It took me another year to finally give it the time necessary to study it more. Me being here makes the rest of that obvious. I liked what I saw, liked what I learned about it, and really liked the philosophy behind it. I took my first careful steps in buying a little bit, and the rest, as they say, is history.

## Discovering Decentralization and the Meaning of Permissionless
Obviously, I started buying Bitcoin with the idea of seeing that number on a chart go up. Then through learning about the history and ethos behind it, I came across the concepts that kept me engaged: decentralization and Bitcoin being permissionless.  
The fact that anyone can send value without needing a bank to allow it (something I ran into far too frequently before) was just... wild. And how on earth could that work when there is no central authority? Those questions and searching the answers to them is what kept me engaged.

Quite naturally then, I stopped looking at charts and started looking at where and how I could pay for things with Bitcoin. I still firmly believe in spending and replacing to both support places that accept payments in Bitcoin, as well as the overall network so, one day, if people really need to rely on the permissionlessness when things go seriously south for their local currencies. Regardless of the reason. 

When your currency fails you, it doesn't matter if it's because the government targeted you, or if the entire system is broken, or your behavior just made a bank's alert system notice you for whatever reason and froze your funds until further clarification.  
Bitcoin's permissionless nature does indeed matter then. But I want the merchant network to be there, well-supported, and thriving. And I strongly believe using Bitcoin for payments helps that.

Naturally, I also started at looking into applying my skills to help Bitcoin, the network, succeed. To put it in Jeff Booth's words: Move more of my time into Bitcoin.

## Where to Start Contributing When You Don't Know Where to Begin?
Entering Bitcoin open source is intimidating. Even for a software developer "veteran" of many years. The knowledge is very specific, the stakes are usually very high, and maintainers and reviewers are very diligent.  
Feeling inadequately prepared is just natural. It took me months of learning to understand that feeling probably never goes away. (And I am still working on convincing myself that it is okay. My head knows it, but it usually comes second to irrational feelings of inadequacy.)  
That is when I started looking for bootcamps and programs specifically geared toward gentle introductions to Bitcoin open source specifically. And this is the route along which I discovered Btrust.

My first attempt was taking part in the [BOSS challenge](https://bosschallenge.xyz/). While I managed to qualify, I soon realized I was in too deep and dropped out to study more. Yes, it stung a bit to not complete, but then again, I now had a lot more knowledge about where my gaps were. In fact, I was surprised to have even qualified by completing [Saving Satoshi](https://savingsatoshi.com/).

Armed with more knowledge about gaps, I then entered a Lightning Dev Bootcamp by [Africa Free Routing](https://freerouting.africa/). This event was co-hosted by Btrust and that is where I first got introduced to them. Shortly after completing that, I met a few more Btrust members at a conference.  
What followed was firming up what I've learned before with their [Rust for Bitcoiners](https://pathways.btrust.tech/03/rust-for-bitcoiners) pathway. This is when I noticed concepts coming back to me more easily. The repetition slowly started showing signs of improvement.

At the end of Rust for Bitcoiners, I was then invited to apply for Btrust's Open Source Fellowship. I made the cut and spent the past three months getting in shape for contributions.

## Trying to Contribute!
The first eight weeks of the fellowship is spent on going deeper into Bitcoin technical material, and learning about the open source ecosystem, typical requirements for various projects. The final weeks then are for picking a project and making your first contributions. I chose [Bitcoin Dev Kit](https://github.com/bitcoindevkit) (BDK). I was finally set to contribute...  (_\*narrator\*_: I was not. Not yet anyway.)

It didn't take long to understand that contributing is by no means a case of "pick and issue, understand the problem, fix it, and raise a pull request." Not by a long shot. In fact, for BDK at least, the advent of AI assisted red team efforts had put maintainers under a lot of pressure to separate the real issues from hallucinated ones, and address them in a timely manner. This meant that maintainers were already at capacity. Another factor was that fairly prolific projects like them attract a lot of potential new contributors. I started seeing multiple contribution efforts from my fellowship cohort alone.  
And the nature of having vulnerabilities disclosed is that particular work isn't done in public (or else exploits would be known immediately), so new contributors had very little idea of how far down the priorities list the work they're attempting to contribute to actually sits.

The most impact I, as budding fresh contributor, could have was by trying to review PRs by maintainers and key contributors. With the added difficulty that several of their PRs are too complex for a new contributor like me to even comment on meaningfully.

## Finding an Issue to Call My Own
A program such as the fellowship cannot possibly build a framework matching the nature of all open source projects. But the must try in order to be able to gauge success in some way.  
One of these requirements was being able to show a claimed issues and PRs that were raised against it. Naturally, in an environment BDK finds itself in, that was a long shot to begin with. But also under more normal circumstances, a new contributor cannot expect to have an issue claimed and PR merged in a matter of two weeks. Consider Bitcoin core. PRs frequently take a very long time, and a lot of rightful scrutiny before it moves.

To be clear: This is no know against the program trying to measure success. It has to be done, but the reality is also that it is probably impossible to do holistically without producing a handbook that in itself would take 12 weeks to work through.  
The other side of the coin is equally true though. It does add pressure onto fellows to scrap and scratch and fight for an issue, any issue, to be able to claim and raise a PR. That was a very frustrating aspect of the final weeks: Spending hours upon hours trying to unearth an issue that satisfy multiple criteria.

First, it needs to be "meaty" enough. Something that touches actual code, and makes a meaningful change.  
Then it also needs to have high enough priority to have a chance of attracting eyeballs from key contributors and maintainers.
Furthermore, it needs to be at a level that a new contributor can contribute with their limited exposure to the project by that time, too.
And lastly, get it merged in time before the end of the program to count toward that goal.

As you can tell, this was the hardest part. I did finally find an issue with the help of the maintainer (who came through Btrust and is my mentor). Without his help, though, I'm not so sure if I would have been able to meet that specific goal in the limited time available.

However, and this is very important: That was just dealing with a necessary artificial requirement under time constraints that made finding an issue to raise a PR against so hard.  
Contributing is far more than just that.

## A More Natural Progression
Realistically, while the concept of looking for "Good first issues" sounds great on paper, the reality is that it is unrealistic. I don't know when that stopped, but I haven't come across a well maintained good first issues list any time recently. I think it was popular at some point, heck, even I had maintained such a list on repos I was responsible for (outside Bitcoin in previous work), but despite me managing that list religiously, we did not attract contributions. That might have been the specific project, but then again, the lack of existing maintained lists indicates to me that the approach didn't work or wasn't sustainable.

So what I can do as a new contributor instead is focus on learning what and how the project does things by reviewing PRs. A key lesson during the fellowship was a one of Btrust's members show-casing how he reviewed a PR by reproducing the issue, then applying the commits of a PR individually to inspect changes locally.  
That is an approach that will stick with me and that I have applied myself. And going through reviews one commit at a time teaches me how the author identified, approached, and tested the issue. As a bonus, fairly frequently, there might be some additional follow up work that could end up in a PR to continue the work. But again, for starters, understanding and learning is more important than having a PR. I still believe those come naturally as second order artifacts of starting to understand a project better.

So, without constraints on deliveries, my best advice for anyone trying to break into open source contributions is to learn about the project by reviewing PRs, try to reproduce and understand each commit, and learn how to use tools and techniques to get there. (For the latter, I wrote a short article on how I was taught to [test a pull request locally](https://njump.me/naddr1qvzqqqr4gupzqd0vgmaq2psf32f67rlthe4yfxk8l2yuje3e77sal4nwy7k3zuvgqy88wumn8ghj7mn0wvhxcmmv9uq3wamnwvaz7tmjv4kxz7fwwpexjmtpdshxuet59uqzkcmgv43kk6twvukk7at594c82mrv94ex2ut4v4ehguedd3hkxctvd3uj6amfw35z6emfws4xk7xa).)

So, accept that as a new contributor you will be frustrated at times. Learn to step away, take a breather, and come back stronger. For example, I raised a promising PR closing gaps in tests for methods that were due a refactor only to find out later that a key contributor was actively working on removing that method entirely. It was good code, had to think critically about how to test actual code, and learned a lot. I did not get a merged PR out of it and that is frustrating. But the big win is that I now understand the project that little bit better.  
May the next attempt be more fruitful. Trust me, it is much easier to see it in that light now than it was when I found out the work was not needed after all.

In the end, my own experience tells me this: Be graceful, don't take my own work too seriously. Help where I can, and learn where I cannot help (yet). Do that long enough and my contributions will matter.
