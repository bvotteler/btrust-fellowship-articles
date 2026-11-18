# The Long Road to My First Bitcoin Open Source Contribution
Everything below is my experience. The good, the bad, and the ugly.

Over the past 3 months, I had the privilege to be part of Btrust's 2026 [Open Source Fellowship](https://blog.btrust.tech/introducing-the-2026-open-source-fellowship/) program. The program made a big impact on my trajectory of becoming a contributor.  
Reflecting on my journey so far is part of the program and this article forms part of sharing it. It is worth mentioning, though, that the journey did not start there.

## Start at the Beginning
I have been a software developer for a few decades. Without dating myself too easily, I started when PHP was still something devs got excited about.  
But even so, I only really started noticing Bitcoin around five years ago. I did see it mentioned before that. My best guess being it had to do with it's rise in 2017 and subsequent crash. But hearing a few years later that it was still alive and doing well didn't match what media told me: that it was a dead project.

It took me another year to take the time necessary to study it more. I liked what I saw, liked what I learned about it, and really liked the philosophy behind it. I then took my first tiny steps in buying a little bit.

## Discovering Decentralization and the Meaning of Permissionless
Same as so many others, I started buying Bitcoin with the idea of seeing that number on a chart go up. As I learned more about the history and ethos behind it, I came across the concepts that kept me in this space ever since: decentralization and Bitcoin being permissionless.  
The fact that anyone can send value without needing a bank to allow it (something I ran into before) was just... wild. And how on earth could that work when there is no central authority? Those questions and searching answers to them is what kept me engaged.

Over time, I stopped looking at charts and started looking at where and how I could pay for things with Bitcoin. I firmly believe in spending and replacing to both support merchants that accept Bitcoin, as well as strengthening the network so, one day, if people really need to rely on the permissionlessness for reasons outside of their control, the infrastructure is there to accept them with open arms.

When your currency fails you, it doesn't matter if it's because the government targeted you, if the entire system is broken, or your behavior just made a bank's alert system notice you and freeze your funds. (Of course only for your own safety.)  
That is when Bitcoin's permissionless nature matters most. And I want the merchants accepting it to be there. Well-supported and thriving. Therefore, I strongly believe in using Bitcoin for payments wherever it is accepted.

By extension of that, I also started looking into applying my skills to help Bitcoin, the network, succeed. To put it in Jeff Booth's words: Move more of my time & effort into Bitcoin and out of legacy systems.

## Where to Start Contributing When You Don't Even Know Where to Begin?
Entering Bitcoin open source is intimidating. Even for a developer "veteran" like me. The knowledge is very specific, the stakes are usually very high, and maintainers and reviewers are (rightfully) very diligent.  
I learned that the feeling of being inadequately prepared is the new normal. It took me months of learning to understand and accept that feeling will stay. I am still working on convincing myself that it is okay. My head knows it, but it usually only comes second to feelings of inadequacy regardless of how irrational they can be.  
To help overcome that, I started looking for programs specifically geared toward a gentle introduction to Bitcoin open source. That search led me to discover Btrust eventually, but not without extra steps.

My first attempt was taking part in the [BOSS challenge](https://bosschallenge.xyz/). While I managed to qualify, I soon realized I was in too deep and dropped out to study more. Yes, it stung a bit to not complete, but then again, I now had a lot more knowledge about where my gaps were. With what I know today, I'm impressed and even a bit proud about "past me" for having qualified by completing [Saving Satoshi](https://savingsatoshi.com/).

Armed with more knowledge about gaps, I entered a better starting challenge: a Lightning Dev Bootcamp by [Africa Free Routing](https://freerouting.africa/). This event was co-hosted by Btrust and that is where I was first formally introduced to them and their mission. After completion, I even met a few more Btrust members at a local conference.  
What followed was firming up what I've learned before with Btrust's [Rust for Bitcoiners](https://pathways.btrust.tech/03/rust-for-bitcoiners) pathway. This was the first time concepts started to come back to me more easily. All those "reps" slowly started showing signs.  
At the end of Rust for Bitcoiners, I was delighted to receive an invitation to apply for Btrust's Open Source Fellowship. I jumped at it, made the cut, and spent the past three months getting in shape for contributions to Bitcoin projects.

## Trying to Contribute
The first eight weeks of the fellowship was spent on going deeper into technical material about Bitcoin. Followed by learning about the open source ecosystem, typical requirements, and gaining familiarity with various projects. The final weeks then were for picking a project and making our first contributions.  
I chose [Bitcoin Dev Kit](https://github.com/bitcoindevkit) (BDK). I was finally set to contribute...  (_\*narrator\*_: I was not. Not yet anyway.)

In short order I discovered that contributing is by no means a case of "pick and issue, understand the problem, fix it, and raise a pull request." Not by a long shot.  
Instead for BDK at least, an influx of AI assisted red team efforts had put maintainers under a lot of pressure to triage a wave of reported vulnerabilities and bugs, then prioritize and address them. This meant that maintainers were already at capacity. Another challenge was that fairly prolific projects like BDK attract a lot of budding new contributors.  
Also, the nature of reported vulnerabilities means much of that work isn't done in public (or else exploits would be known immediately), so as new contributors, we had very little insight of how far down the priorities list the work we were attempting to contribute to actually sat.

The most valuable impact I could have was by reviewing PRs raised by maintainers and key contributors. With the added difficulty that several of their PRs were too complex for a new contributor like me to even comment on meaningfully. At times, even though I was told by maintainers and my mentor that type of work was appreciated, it still felt like a participation trophy only.

## Finding an Issue to Call My Own
A program like the fellowship cannot possibly build a framework matching the nature of all open source projects. They have to try set out tasks to be able to gauge success in some way.  
One of these requirements was being able to show a claimed issues and PRs that were raised to address it. So in the situation BDK was operating in, that was a long shot to begin with. The same will apply for other projects in very normal for them circumstances. Consider Bitcoin core, a new contributor cannot realistically expect to have an issue claimed and PR merged in a matter of two weeks. PRs frequently take a very long time, and a lot of scrutiny before it moves. That slow pace is deliberate for Core.

I want to be clear: This is no knock against the fellowship program trying to measure success. It has to be done and it is probably impossible to do that holistically without producing a handbook that in itself would take 12 weeks to work through. It makes sense to try and measure issues worked on and the PRs doing that.  
But it's also important to accept and recognize that it adds pressure for fellows to scrap and scratch and fight for an issue, any issue, to be able to claim and raise a PR. That was a very frustrating aspect of the final weeks: Spending hours upon hours trying to unearth an issue that satisfy multiple criteria.

Such an issue needs to be "meaty" enough. Something that touches actual code and makes a meaningful difference.  
Then it also needs to have high enough priority to have a chance of attracting eyeballs from key contributors and maintainers for reviews.
Furthermore, it needs to be at a level that a new contributor can contribute with their limited exposure to the project by that time.
And lastly, it needs get merged (or close to it) in time before the end of the program to count toward that goal.

Therefore, this task was the hardest part. I did catch a break and finally found an issue with the help of a maintainer (who also is my mentor, fortunate me). Without his help, I doubt I would have met that specific goal in the limited time available.

Having said all that, here a reminder: That pressure was only dealing with a necessary artificial requirement under time constraints that made finding an issue to raise a PR against so hard.  
Contributing is far more than just that, it was only that aspect of having limited time making it such a challenge.

## A More Natural Progression
Looking back, while the concept of looking for "good first issues" sounds great on paper, it did not serve me well to over index on that.  
I haven't come across a well maintained good first issues list any time recently. It seemed popular at some point. I, too, have maintained such lists on repos I was responsible for in my previous work. I remember little uptake, but that might have been the project. The lack of existing maintained lists indicates to me that the approach didn't work or wasn't sustainable for many other projects, either.

My best advice for anyone at that same "first contributions" stage of trying to break into open source is to learn about the project by reviewing PRs, try to reproduce the issue at hand, and work to understand each commit in isolation. For part of reviewing someone else's PR locally, I wrote [an article](https://njump.me/naddr1qvzqqqr4gupzqd0vgmaq2psf32f67rlthe4yfxk8l2yuje3e77sal4nwy7k3zuvgqy88wumn8ghj7mn0wvhxcmmv9uq3wamnwvaz7tmjv4kxz7fwwpexjmtpdshxuet59uqzkcmgv43kk6twvukk7at594c82mrv94ex2ut4v4ehguedd3hkxctvd3uj6amfw35z6emfws4xk7xa) summarizing what Btrust members showed us during the fellowship.

My current approach can therefore be boiled down to: Help where I can, recognize where I cannot (yet). Keep closing gaps by reviewing work. If I keep doing that consistently, over time, meaningful contributions should emerge naturally.
