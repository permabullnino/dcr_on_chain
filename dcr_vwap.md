Decred On-Chain: The Ticket Pool VWAP

Introduction / Roadmap

In my previous piece "Decred On-Chain: A Look at Block Subsidies", we explored the ultimate Network-Based indicator - block rewards, and their relationship to network valuation from the point of view of the network itself, miners, stakers, and the DCR treasury. Within this article we will begin to explore and uncover the magic behind the ultimate Decred User-Based indicator - ticket data, and show how it provides a means for effectively gauging the HODL behavior of users within the Decred Network. This article aims to be a foundational piece in understanding ticket data for future pieces, explain why it's worthwhile analyzing, and hopefully provide some color for Decred-curious on-chain analysts within the cryptocurrency space. Below are the topics that will be covered within:

(1) Decred Tickets: What they are, functions they serve, and ticket parameters [MAYBE MOVE TICKET PARAMS TO LATER SECTION]
(2) Analysis of User-Based Indicators in Crypto-Networks
(3) How Decred Tickets Break the Mold for User-Based Indicators
(4) Definitions of "HODLing" in Different Crypto-Networks
(5) Introducing the Ticket Pool VWAP
(6) Analysis of 14, 28, and 140 Day DCRUSD Ticket Pool VWAP
(7) Analysis of 14, 28, and 140 Day DCRBTC Ticket Pool VWAP
(8) Lifetime DCRUSD VWAP, Lifetime DCRBTC VWAP, and Cumulative Cap
(9) Closing Thoughts

Decred Tickets: What They Are, Functions They Serve and Ticket Parameters

Tickets are the semi-scarce asset of Decred's Proof of Stake mechanism. Just like Proof of Work, which is semi-scarce as a function of (1) difficulty retargeting based on demand for hash and (2) profitability in acquiring additional units of hash - tickets are semi-scarce as a function of (1) ticket price regularly retargeting based on demand for tickets and (2) the scarcity of available DCR on the market to purchase tickets. In the case of Proof of Work, people compete for hash in order to receive block rewards. Decred tickets are similar, as stakers compete for tickets in order to (1) receive block rewards and (2) participate in the network's governance. This combination of scarcity, incentive to compete for the scarce object, and making the pricing of the scarce object determined by purely market driven forces are what make Decred's Proof of Stake / Ticketing mechanism a reliable second authentication layer as it relates to enforcing digital scarcity, and ultimately a grand innovation in applying the principles which make Proof of Work special in a stake-based scheme.

[INSERT TABLE HERE]

Security for cryptocurrencies depend on the foundations listed in the table above - incentivizing people to contribute to the network is mission critical for the longevity of any crypto-network. These incentives to contribute are upheld not only by competing over scarce objects, but also by making the game for competing over these scarce objects *provably* fair. Fairness in distributed systems such as cryptocurrencies are best managed by the market itself, so fairness can be proven via (1) transparency of data, (2) data completeness, and (3) established / widely accepted quantitative measures.

Proof of Work offers transparency by allowing users to check the validity of hashes that supposedly fall below the network difficulty target. Futhermore, Proof of Work offers high data completeness as it's impossible for mining not to leave an on-chain footprint. Lastly - difficulty retargetings establish the fair balance between supply and demand, which can be checked on by looking at the frequency of which blocks are being discovered. All three things considered - Proof of Work is *provably* fair.

Decred's Proof of Stake Tickets offers transparency by allowing users to check the validity of any given ticket being chosen to vote - which is a fucntion of the previous block's hash. Tickets are a consensus-critical part of Decred, so all ticket purchases and votes occur on-chain, so there is no missing material data surrounding tickets for network stakeholders. And to finish things off - Decred tickets have ticket price retargetings which aim to establish a certain amount of ticket buying volume, which can be checked to determine if the retargeting is properly regulating supply and demand.

Both PoW and Decred's PoS Tickets are built on the foundations of randomness, which is also incredibly important. If one party could game the system and win the PoW/PoS competitions consistently while not putting forth the appropriate amount of work/stake, then by definition these systems wouldn't be fair. PoW imposes this fairness by making block discovery a brute force process - forcing miners to plug nonces relentlessly until they find a hash below the network difficulty target. Decred's PoS leverages the randomness from PoW to its advantage, by making ticket selection pseudo-randomly derived from the previous block's hash.

[INSERT TABLE HERE]

Fairness matters - analyzing competition over scarce resources in these crypto-systems is substantially less interesting and predictive of user behavior if they aren't fair. Proof of stake systems are *generally* stamped as being "unfair", but that is not the case with Decred's ticketing system.

---

We have covered that tickets are scarce resources that are fairly competed over. However, it's also important to also understand that tickets are incredibly useful, wearing multiple hats within the network itself. More emphatically speaking, tickets drive the vast majority of operations that users leverage Decred for, including:

(1) A means for users to accumulate as much of the 21 million DCR supply as possible
(2) An additional authentication layer for newly discovered blocks
(3) On-chain voting to push consensus changes
(4) Off-chain voting to allocate treasury funds
(5) Provide fungibility
(6) Time-locked, trustless, custody of funds
(7) Provide network participants with high signal data 

When users lock their DCR in tickets, they're gaining access to everything listed above, and opting out of them when foregoing ticket purchases. 

---

Thus far we have established that tickets are a scarce resource, that are competed for fairly, and provide a great deal of utility for network participants / the network itself. Now it's time to discuss the specific parameters of the ticketing system. These specifics build the backbone of ticket scarcity, competitive fairness, and utility that they provide. Understanding the specifics not only help us lock down these foundational bits, but also set the stage for us to compare ticket data to other User-Based indicators in crypto. After this comparison we can leverage this information to better analyze the TVWAP (Ticket Pool VWAP). The parameters of the Decred ticket system are as follows:

(1) Target Ticket Pool Size: 40,960 tickets
(2) Ticket Votes per Block: 5 - please note tickets get released from ticket pool after voting and need to be repurchased at the most recent ticket price
(3) Block Times: ~5 minutes on average
(4) Difficulty / Ticket Price Adjustment: every 144 blocks - this 144 block period will be referred to as a "ticket window" herein
(5) Ticket Voting: Pseudo-random

We can take these base parameters and point out a few extra noteworthy aspects of the Decred ticket system:

(1) Ticket Votes per Ticket Window: 720 votes (5 votes per block * 144 blocks per ticket window)
(2) Ticket Window Duration: ~12 hours (144 blocks per ticket window * 5 minutes per block)

Before moving forward, it's worth taking a second to remind those who are less familiar with Decred tickets that the goal of the ticket difficulty retargeting algorithm is to match supply and demand reliably. As such - if 720 tickets are getting released from the ticket pool during a ticket window, then the goal is to replace those tickets with another 720 tickets on average:

(1) Ticket Windows to Fill Ticket Pool: 56 (40,960 target ticket pool size / ~720 tickets purchased per ticket window)
(2) Days to Fill Ticket Pool: ~28 (56 ticket windows to fill pool / 2 ticket window periods per day)
(3) Ticket Expiration: ~142 days (tickets that still haven't voted will expire, DCR will become spendable)

---
Analysis of User-Based Indicators in Crypto-Networks

As a quick refresher, User-Based indicators are on-chain footprints that are left by users themselves. By analyzing the data flows driven by users, we can better understand their behavior and how it changes with a network's growth over time. There are a variety of ways users can leave an on-chain footprint, but generally speaking there are 4:

(1) Mining (Example: Difficulty Ribbon)
(2) Throughput (Examples: NVT Ratio, Network Momentum)
(3) Coin Age (Examples: HODL Waves, Realized Price)
(4) Decred Tickets (Example: Ticket Pool VWAP)

Each indicator category possesses its own respective strengths and weaknesses as far as data quality is concerned. Specifically speaking, for purposes of this article we care about data quality as it relates to analyzing holding behavior of users. In simple terms, these categories for analyzing holding behavior can be compared across 3 standards:

(1) Completeness: Does indicator capture all relevant data, or can some of the data the indicator relies on occur off-chain?
(2) Intent to Hold: Is the intent to hold implied based on the data, or is the indicator very explicit about intentions of users?
(3) Dynamic: Does data driven by indicator provide reliable signals promptly? Or does it lag?

Below we will discuss mining, throughput, and coin age as user based indicators by evaluating how well they satisfy the completeness, intent to hold, and dynamic standards needed for analyzing users holding behavior.

Mining

[INSERT TABLE HERE]

(1) Completeness: Mining data doesn't suffer from completeness issues, because by definition it needs to emerge on-chain in order to add blocks to the network's transactional history. 
(2) Intent to Hold: Miners are known as the largest compulsory sellers of any cryptocurrency, as they have both fixed and variable costs to cover from their capital-intensive mining operations. There are certain points in market cycles where miners become more willing holders, but these points vary case-by-case. As such, the "intent to hold" is not by any means explicit as far as mining data is concerned.
(3) Dynamic: Mining data is relatively dynamic, over market cycles hashrate has proven to be a reliable manner to identify market bottoms which is evident in squeezes in network hashrate over a multi-week or multi-month period. 

Throughput

[INSERT TABLE HERE]

(1) Completeness: Throughput data is not complete, and will probably become less complete as time goes on - off-chain solutions like Lightning Network will allow users to transact without leaving an on-chain footprint. Further, users can also transact / allow coins to change hands using centralized solutions such as cryptocurrency exchanges like Coinbase, Kraken, etc.
(2) Intent to Hold: Generally speaking we do not know whether transactions on-chain represent sends from an exchange to a personal wallet, a send from one personal wallet to another, or a send from a personal wallet to an exchange to sell. Overall, it's very difficult to figure out intent when it comes to a standard on-chain transaction.
(3) Dynamic:Transactional throughput has proven to be relatively dynamic, with trends of anemic on-chain throughput during bear markets and elevated levels of throughput during accumulation periods and bull markets. 

Coin Age

[INSERT TABLE HERE]

(1) Completeness: Just like Throughput, Coin Age does not guarantee data completeness. Coins can change hands via the various off-chain outlets available (lightning, exchanges, etc.).
(2) Intent to Hold: Age resets for a set of UTXOs when they move on-chain. When these UTXOs aren't moving, they are by definition being held. Although data completeness concerns still remain, this understanding of intent is substantially stronger than in the cases of Mining and Throughput.
(3) Dynamic: Coin age has proven to be a dynamic means to track holding behavior of network participants over time, with slower moving but high conviction tools such as HODL Waves, and faster-responding tools like Realize Price, by assigning a price to coins based on when they last moved.

[FINAL TABLE SHOWING ALL 3 INDICATORS]

---

How Decred Tickets Break the Mold for User-Based Indicators

The Decred tickets system is special in that its design uniquely positions it for satisfying the completeness, intent to hold, and dynamic standards better than other indicators available in the cryptocurrency space. Below are the explanations for how, and why:

(1) Completeness: As we've already stated before - all material data related to tickets appears on-chain, and we can expect that this will remain the case as tickets are consensus and governance critical. Data incompleteness in either of these arenas could potentially erode assurances surrounding digital scarcity and sound governance, respectively. 
(2) Intent to Hold: By locking up DCR in tickets you are relinquishing spending capabilities in exchange for stake in the network. This tradeoff is holding in the purest sense, by committing skin in the game and only to be unlocked at a pseudo-random interval. There's zero ambiguity surrounding intent here - purchasing tickets = holding behavior.
(3) Dynamic: One of the most overlooked aspects of the Decred ticket system is that users are engaging in what I like to call "active holding". Unlike other networks where holding simply equates to not moving coins for very long periods of time, Decred tickets force users out of holding (i.e. tickets voting) and require them to recommit to holding (i.e. purchasing a ticket at the most recent ticket price). This makes the Decred ticket data very dynamic, as it gives users the opportunity to opt out of holding or requires them to commit an on-chain footprint to prove their willingness to hold. With approximately ~190,000 DCR moving into tickets on a daily basis, this not only gives us a dynamic dataset but also a very large one.

[TABLE SHOWING ALL 4 INDICATORS]

---

Definitions of "HODLing" in Different Crypto-Networks

In the cryptoverse we refer to diehard advocates that do not have any intent to sell in the near future as "HODLers". This general definition applies to any network and its respective native asset, however - specificity surrounding how HODLers going about holding is valuable to understand, and a question worth addressing. Each network with its own design / goals will dictate how the native asset is held, and it's important to make this distinction between (1) different networks and (2) different types of activity within a network itself so we can ensure we are making fair comparisons and being as precise as possible when evaluating data. Below we have a quick comparison of Bitcoin and Decred, with (1) their respective network design / goals and (2) HODL definitions:

Bitcoin Design / Goals: Proof of Work used to provide assurance over transactional history validity, and informal governance structure to coordinate network-wide initiatives. Ultimate goal = store of value.
Bitcoin HODL: Not moving bitcoins for long periods of time.

Decred Design / Goals: Hybrid Proof of Work + Proof of Stake used to provide assurance over transactional history validity, and formal governance structure to coordinate network-wide initiatives. Ultimate goal = store of value + digital state.
Decred HODL: Locking DCR up in tickets.

HODLing Decred is different from Bitcoin HODLing. In Decred, HODLers buy into the social contract that governing the network is valuable, and that rights over governing are worth competing over. As such, if you are indeed a HODLer - you will be locking up your DCR in tickets. This is significant as it allows us to weed out all other transactions when trying to focus on HODLers, and we can assume that any standard Decred transaction (i.e. any non-ticket related transaction) represents marginal buyers and sellers. 

---

Introducing the Ticket Pool VWAP

At this point we've built a foundational understanding of Decred tickets, what makes them special, and how they represent the collective pulse of HODLers within the Decred network. In the remainder of this piece we will focus on the Ticket Pool Volume Weighted Average Price over a variety of time frames, discuss how it performs versus the market price, and what the differences imply about HODLers and their relationship to the network valuation over time.

The calculation for the TVWAP is simply the USD or BTC value locked into tickets over a selected timeframe divided by the the amount of DCR that have gone into tickets over that same period of time, as shown below:

[SHOW TVWAP CALCULATION]

The TVWAP is significant and important to be aware of at all times because it transaparently gives you an approximation of the cost basis of HODLers within Decred the network, or more specifically the prices they forewent liquidity to recommit to HODLing. Opportunity costs matter in all walks of life, and the TVWAP hones in on this. The success / failure on locking money in tickets instead of doing something else with those DCR can be measured in the profit / loss from the ticket entry point, which we can show using (1) a standard line chart with actual price vs TVWAP prices, or (2) the ratio of the actual price vs the different VWAP prices.

[SHOW TVWAP RATIO CALC]

Our chosen timeframes for this study are the 14 day , 28 day, and 142 day TVWAPs. The rationale for these timeframes are as follows:

(1) 14 day: This timeframe has been chosen in order to provide a sensitive TVWAP that will be able to catch as many bottoms as possible. It also represents the amount of days it takes to fill 50% of the ticket pool.
(2) 28 day: This timeframe is significant because it represents the amount of days it takes to fill up the ticket pool and also reflects the average vote time for a ticket.
(3) 142 day: This timeframe is significant because it represents the amount of days it takes for a ticket to expire, or explained differently - for the ticket pool to move fully through every ticket purchased, whether it be via voting or expiration.

In the next two sections we will perform an analysis of these TVWAPs for DCRUSD and DCRBTC.

---

Analysis of 14, 28, and 140 Day DCRUSD Ticket Pool VWAP

Each TVWAP timeframe in this section will include a price chart overlaid on the TVWAP Ratio, that way readers can see how the timing of actual price bottoms compares to the TVWAP ratio. A brief analysis of each chart will follow, until we reach the 142 day DCRUSD TVWAP ratio - which will have instead dive into a comparative analysis versus the Decred Realized Cap to help us better track trend changes over time.

14-Day TVWAP:

[SHOW 14 DAY CHART W/ TVWAP RATIO]

It's worthwhile noting that the ratio section at the bottom of the chart has two lines with (1) the yellow dotted line as the raw TVWAP ratio value and (2) the light blue solid line as the 7-day smoothed version of the raw TVWAP value. The red box represents the meat of the historical sell zone and the green box shows our historical buy zone. These zones respectively can be viewed as places where HODLers might become sellers, or where HODLers are so underwater that they're going to stick to the plan, wait for a reversal, or even add to their DCR hodlings. The historical zones for reversals are as follows:

Sell zone: 1.15 - 1.35 TVWAP Ratio
Buy zone: 0.90 - 0.75 TVWAP Ratio

Note that there's approximately a 27% gap between the bottom of the sell zone and the top of the buy zone. Furthermore - note that DCRUSD to date hasn't had a full, longer term trend reversal without the 7-day smoothed ratio moving into the sell or buy zones. However, it is worth mentioning that the 14-day TVWAP isn't the ideal timeframe to use for this - the 28-day and 142-day timeframes are more appropriate.

28-Day TVWAP:

[SHOW 28 DAY CHART W/ TVWAP RATIO]

Sell zone: 1.35 - 1.50 TWAP Ratio
Buy zone: 0.90 - 0.70 TVWAP Ratio

Quite naturally, the 28-day TVWAP Ratio tops and bottoms less frequently. This lack of frequency brings added significance for when it reaches our sell / buy zones, and can give us a higher conviction sell / buy signal. Another way to phrase this is that the people who filled up the ticket pool over the last 28 days are either in heavy profits or losses when the sell / buy zones are hit. Upon further inspection readers might notice that the 28-day TVWAP bottoms seem much more consistent than the tops, which would be a fair assessment. With more time my expectation is that we'll see the sell zone become better-defined. However, at a minimum we can use the bottom zone for a gauge on areas for maximum HODLer pain, which is usually where we see price action reverse. 

142-Day TVWAP:

There are three items that were previously explained relevant to this analysis:

(1) It takes 142 days to run through the entire ticket pool
(2) Ticket buying is a high-signal way to identify HODLers transacting on the Decred network
(3) All non-ticket transactions represent accumulators or capitulators

The Realized Cap of any cryptocurrency represents the cumulative value of all coins on the network, but with their individual value assigned by when the coins were last moved. Decred has two ways in which coins move - (1) tickets and (2) standard transactions. The Decred Realized Cap captures the combination of these two. If the Realized Cap is supposed to capture the value of every most recent coin movement, then in theory it should most closely resemble the 142-day TVWAP Cap of all the TVWAPs, as that's the amount of days it takes to fully move through every single ticket in the ticket pool. The spread between the Realized Cap and 142-Day Cap should be representative of a accumulation or capitulation premium / discount as a result of the standard transactions included in the Realized Cap, which should give hints for the health of a current trend or direction of an upcoming trend. The chart comparing the Realized Cap, 142-Day Cap, and Actual Market Cap are shown below:

[SHOW CHART]

The results of this comparison line up nicely with expectations - while Realized Cap sits above the 142-Day Cap price action remains bullish, indicative of an accumulation premium for Decred, and viceversa for when Realized Cap is lower than the 142-Day Cap.

---

Analysis of 14, 28, and 142 Day DCRBTC Ticket Pool VWAP

This section will follow a similar approach to the previous section - the 14-day and 28-day charts will include their respective TVWAP ratios along with the line chart of the Decred network's value denominated in BTC terms. The 142-day chart will include network value vs the 142-day BTC value, and accompanied with volume bars on the bottom for total DCR moved on-chain (ticket buying + standard transactions). This combination will give us perspective on HODLers, accumulators, and capitulators from a bird's eye view. 

14-Day TVWAP:

[SHOW 14-DAY CHART W/ TVWAP RATIO]

Sell zone: 1.15 - 1.30 TVWAP Ratio
Buy zone: 0.90 - 0.75 TVWAP Ratio

28-Day TVWAP:

[SHOW 28-DAY CHART W/ TVWAP RATIO]

Sell zone: 1.20 - 1.45 TVWAP Ratio
Buy zone: 0.80 - 0.65 TVWAP Ratio

142-Day TVWAP:

[SHOW CHART]

ALTBTC charts are more useful for identifying accumulation / capitulation behavior in general. The basic rationale is that ALTUSD pairs can get dragged up / down by Bitcoin's price movements, so ALTBTC can help remove that noise to zoom in on the true demand for the altcoin itself. This approach is no different for DCRBTC - and the accumulation / capitulation we aim to identify shows itself in the 142-day chart. 

Zoned off using green boxes are the nodes of high-volume DCR moved on-chain - which are our obvious zones of interest for accumulation / capitulation behavior. What's particularly interesting about these zones is that they all almost exclusively occur while the Decred network value sits below the 142-Day Cap, signalling that all big accumulation occurs when HODLers are underwater ("buying the blood") and all big capitulation occurs when these same HODLers are feeling the pain of Mr. Market. A few additional notes include:

(1) The 142-Day Cap seems to serve as the bull / bear line for DCRBTC - notice how for Decred's entire bear market (since July 2018) the Decred market cap was unable to cleanly breach the 142-Day Cap.
(2) Periods where market cap sits above the 142-Day Cap are characterisically quiet on-chain, with a steady flow of coins but no obvious large movements. 

---

Cumulative Cap, Lifetime Ticket Pool VWAP, Lifetime DCR Moved On-Chain VWAP, and Lifetime Average Cap

This section focuses on the lifetime values moved on-chain, how they compare to their non-weighted equivalents, and how these help us analyze the big picture of the Decred markets. The definition of these lifetime values, a brief explanation of their significance, and their formulas are included below:

Cumulative Cap

Definition: The cumulative value that has gone into tickets over Decred's lifetime.
Significance: Decred tickets are opt-in, which means that users have two decisions: (1) to buy tickets and (2) to not buy tickets. This means that there's no sell side of tickets, and that the cumulative value locked into tickets can be a gauge to meausre the net demand to HODL DCR.
Formula: [SHOW FORMULA]

Lifetime Ticket Pool VWAP (LTVWAP)

Definition: The weighted average DCRUSD or DCRBTC value that has gone into tickets over Decred's entire lifetime.
Significance: This is the point where on average a Decred network participant committed to HODLing. As such, the LTVWAP can be viewed as a representative break even price for HODLers
Formula: [SHOW FORMULA]

Lifetime DCR Moved On-Chain VWAP (LOVWAP)

Definition: The weighted average DCRUSD or DCRBTC value that has moved on-chain (tickets & standard transactions) over Decred's entire lifetime.
Significance: This also represents a breakeven price of sorts, but is more inclusive as it includes accumulators and capitulators.
Formula: [SHOW FORMULA]

Lifetime Average Cap

Definition: The non-weighted average price Decred has traded at throughout its lifetime.
Significance: This is included within as a means to compare the difference between the on-chain / volume-weighted tools. 
Formula: [SHOW FORMULA]

Below we have the DCRUSD & DCRBTC charts with all the above included versus Decred's Market Cap:

[SHOW DCRUSD CHART]

Note 1: The Decred Market Cap followed the Cumulative Cap closely from network launch until the the bull market top in early 2018.
Note 2: Throughout Decred's lifetime the LTVWAP, the LOVWAP, and Lifetime Average Cap have overall represented a zone of confluence when Market Cap approaches it from the upside or downside. As the "Break Even Zone" for Decred participants it is obvious in retrospect that this is where price stalled in late 2018, and so far marked the DCRUSD top for 2019.
Note 3: The Decred Market Cap has put in significant bottoms on three different occasions when Market Cap is at 35% of the Lifetime Ticket Pool VWAP.

[SHOW DCRBTC CHART]

Note 1: The Decred Market Cap followed the Cumulative Cap through mid 2017, which was the end of the notorious Alt Season.
Note 2: What applied to the DCRUSD chart likewise applies to DCRBTC - the LTVWAP, the LOVWAP, and Lifetime Average Cap are a large confluence zone of buy / sell activity. Like we've mentioned before - this makes a lot of sense as the "Break Even Zone" for network participants.
Note 3: DCRBTC has had two significant bottoms - one in early 2017 and one in late 2019. These bottoms were not at an equal % down from the LTVWAP, but have been close enough around ~28% (shown with the purple line)

Now that we have the HODLer Break Even Price (LTVWAP) and the HODLer, Accumulator, & Capitulator Break Even Price (LOVWAP), we can merge them into the block rewards paid to date lines (covered in this article) to create an overall lifetime network participant break even  chart for DCRUSD & DCRBTC:

[SHOW DCRUSD CHART]

[SHOW DCRBTC CHART]

---

Closing Thoughts

Within we have covered what makes Decred tickets a unique User-based indicator, how it helps us filter out noise between HODLers, Accumulators, and Capitulators, and the significance of the volume-weighted average value that has gone into tickets over various timeframes. Before closing - please remember that Decred is still a young network, and that we're in the early stages of evaluating a blockchain that could be around for a very long time. This passing of time can prove to change / prove incorrect certain data that we've seen to date. However, hopefully this piece helps us all have the frameworks in place to dive deeper and appropriately change assumptions if the time comes. Until then - signing out...

Permabull Nino
