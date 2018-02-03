September 2017
==============

Tech
----

### The digital path

Author: Mark S. Miller and Marc Stiegler

[Chapter](https://www.cypherpunks.to/erights/talks/pisa/paper/digital-path.pdf)

- Wow, these guys were onto the issues of capital and land titles in developing countries (and solving them with "smart contracts") way before blockchains got started
- Wealth is based on high-trust between members as well as widely trusted intermediaries enabling cooperation at a distance ("trust hubs")
    - Trust intermediaries essentially allow n^2 network scaling vs a forest graph development
    - Especially trustworthy systems of title transfer: credible title claims enable collateral and therefore further leverage using collateral
- Local communities will usually work out their own law if a more widespread option (e.g. national) is not available; difficulties lie in bridging new national systems with these traditional local systems
- Could those without the needed trust intermediaries piggy back on known intermediaries via digital means?
- Escrows create an "inescapable arrangement", as can reputation (to protect and predict good participation)
- On smart-contracts as board games: "We assume that each player trusts their own computer (a dangerous assumption...)" -- interesting to note, Ethereum makes this non-dangerous
- Digital means cannot be *coercive*, unlike governmental means; they cannot force physical action from people by themselves
    - Diminish potential losses: insurance, reputation via ratings (credit score for local laws)
- First notion of *split* contracts? A contract split between automated and non-automated parts.
    - Automated: contract automated by overridable by real humans
    - Layered: some underlying logic is automated but the "whole" is governed by humans
- "Regulatory capture": consumers have escaped geographic and jurisdiction boundaries imposed by their states, but producers have not
- **"Might a decent architecture for distributed smart contracting treat regulation as damage and route around it"** -- Wow, WTF just happened here `<mindblown>`
- Western companies: legitimacy is linked to legality; anything that is legal is considered legit (resulting in loss of flexibilty for stability and performance?)

### The Hitchhiker's Guide to Smart Contracts in Ethereum

[Article](https://blog.zeppelin.solutions/the-hitchhikers-guide-to-smart-contracts-in-ethereum-848f08001f05)

- Every executed operation is executed by every node; giant decentralized global computer
- Use [`testrpc`](https://github.com/ethereumjs/testrpc) as a fast local dev node
- Use [`truffle`](https://github.com/trufflesuite/truffle) as a dev/boilerplate framework
    - It has a console for testing function calls and reading public state!
- Contracts:
    - Similar to classes; contain their own state and methods
    - Read-only (`constant`) methods: no state changes
    - Transactional methods: perform state changes, require gas
- Security basics:
    - Reentrancy: don't perform external calls in contracts, or if you must, make sure they're last
    - Sending can fail: make sure you check the fail case
    - Loop iterations cost gas: especially arrays, but if iterating over a state that grows, be careful about increasing gas costs
    - Call stack depth limit: prefer no recursion
    - Timestamp dependency: timestamps are inaccurate and can be manipulated by miners; exception are trusted 3rd party oracles

### The Meaning of Decentralization

[Article](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)

- Three axis of decentralization (interesting):
    - Architectural (de)centralization: physical hardware
    - Political (de)centralization: individuals or organizations
    - Logical (de)centralization: interface and data structures -- if you cut the system in half, are the two halves still independently operable?
    - E.g. blockchain is architecturally and politically decentralized, but logically centralized (consensus on state)
    - Architectural usually leads to political centralization
- Reasons for decentralization (and their pitfalls):
    - Fault tolerance -- don't run on a single hardware / software architecture, scrutinize upgrades, incentives should be decentralized (multiple orgs)
    - Attack resistance -- asymmetric attack/defense costs (usually costs much more to defend than attack), centralized sometimes more resistant to attack
    - Collusion resistance -- powerful players will always get around to colluding for their best interests (mitigate it by trying to build protocols that resist it, lessen ability to coordinate, or try to flag harmful coordination and eliminate it)

### Minimum Viable Blockchain

[Article](https://www.igvita.com/2014/05/05/minimum-viable-block-chain/)

- Triple-entry bookkeeping: having a notary record the transaction
    - Notary can authenticate two parties, and has a tamper-proof record of the transaction taking (or not taking) place
    - Source of failure is then the notary
    - DSAs enable triple-entry bookkeeping and eliminate notaries (but a fail point: key management and whether the party is legitimately in control of the keys used)
- P2P systems are usually forced to operate under the assumption of weaker consistency:
    - Some participants will be out of sync
    - Eventually participants will converge on a global ordering of events
    - Conflicts must be predictably resolved
    - Invariants (ie. a set of rules) must be enforcable
    - System should be protected from Sybil attacks
- **Voting systems are easily subverted if forging identities (and thereafter, voting with the identity) is easy and cheap**
    - Proof-of-work: proof-of-work step should be expensive for sender, cheap to verify by others -- this asymmetry makes it harder to vote

### Multithreading Magic

[Article](http://zeromq.org/whitepapers:multithreading-magic)

- All current languages (circa 2010) were completely shit at concurrency on their own; many still are today (2017)
- "Just switch to Erlang"(TM)
- Extra rules to live by in concurrency:
    - "Forgotten synchronization": avoid race conditions for shared data
    - "Incorect granularity": proper usage of critical sections is *difficult*
    - "Read and write tearing": what operations are atomic? what guarantees come with the system / language's memory model?
    - "Lock-free reordering": lock-free code can be problematic when the processor rearranges execution; learn about memory barriers
    - "Lock convoys": locks are unscalable, too many threads waiting on one leads to performance issues
    - "Two-step dance": avoid thread thrashing between waking and waiting
    - "Priority inversion": avoid changing thread priorities, period
- Costs of the above:
    - Super expensive (10-100x compared to single thread)
    - Usually applications only use a handful of threads
    - Most threads are still blocking each other, so not much useful work is actually getting done
    - Locking just doesn't scale (diminishing returns on thread number)
    - Further increases in performance is just arcane black magic at this point
- Key to ideal concurrency: pass information as messages (into queues) rather than share state
    - Code becomes thread-naive; no shared data = all data is private (i.e. no locks, critical sections, etc); threads can run at full speed
    - Trivial to scale when everything is broken down into a task; just create more instances (sounds a lot like the microservices fad, but this is *really* important)
    - No blocking (except for waiting for work via a queue)

### The Value of Cryptocurrency

[Article](https://medium.com/@RafeFurst/the-value-of-cryptocurrency-675e7c790979)

- Sources of value for money:
    - Production: how much does it cost (real and opportunity)
        - Fiat currencies have very little production value, since they're only backed by trust (some would argue this isn't cheap)
        - Bitcoin costs extremely large amounts of resources to mine
            - These resources could be used for other systems (opportunity costs), but the market is still demanding it (because it's an extremely cheap and simple economic model?)
    - Scarcity: how much is available
        - Fiat can be produced infinitely
        - Bitcoin has a cap
    - Utility: can it be used?
        - Cryptocurrencies have a lot more "uses" than just stores of value and tools of transfer (but how valuable are these "uses"?)

### Spanner, TrueTime & The CAP Theorem

[Publication](https://research.google.com/pubs/pub45855.html)

- Assigns globally consistent real-time timestamps --> how?
    - TrueTime, a bunch of globally synced atomic clocks
- CAP: although we usually say that we have to give up A or C for P, this is only theoretically true in cases where we are experiencing a partition
    - Can we engineer the system so partitions are extremely rare? **If it doesn't partition, we can get all three!**
- Spanner is technically a CP product, but is CA in the case of no partitions
- If both the user and Spanner are down ("fate sharing"), it doesn't matter if Spanner is unavailable; the only data point to use is if a user actually notices it's down
- How much of Spanner's downtime can actually be attributed to partitioning rather than some other fault?
    - Hint: not very much
- At Google, availability is too high for some services (e.g. Spanner, Chubby) that SREs have to artificially introduce faults so they can understand how things can fail
- Key to high availability is Google's WAN and operational robustness (much better than the public Internet's)
    - A bigger risk is actually misconfiguration or software upgrades that simultaneously break multiple paths
        - Limit the impact of an update at first so not all paths are affected simultaneously
    - "Unplanned failures are rare in a Google data center"; damn AWS you better step up your game
- 2PC is bad for availability because all members need to be up, but if each member is actually a quorum group (e.g. Paxos), some of the availability restrictions are alleviated
- Spanner keeps snapshots of data at a particular time, allowing all read-only transactions to be lock-free: every read is associated with a particular state committed at or before the selected time (current reads just use the current time)
    - Reads are also more resilient to partitions, assuming your partition includes all the available data for the requested time
    - Allows for consistent data analysis for any given time
- Synced clocks makes consistency a lot easier to deal with in distributed systems; less chatter for ordering
    - TrueTime is not 100% accurate (nothing will be) so it gives an interval for confidence; if two intervals don't overlap, they definitely won't conflict
        - Provides linearizability (external consistency); serializability comes with 2PC
    - Spanner waits out the error limit to ensure the commit time won't conflict
    - In multiple system workflows, synced time also allows you to know if later pipelines should wait (to be consistent) or go ahead (to be available)

### Software Engineering at Google

[Publication](https://arxiv.org/pdf/1702.01715.pdf)

- Do take note that what works for Google doesn't necessary work for you; they have the scale, team, culture, etc. to make these things work for them. Don't cargo cult.
- Most code is stored within a single, gigantic monorepo accessible to everyone (86 TB repo, 2B loc)
    - Anyone can see, build, experiment, and PR; encouraged to fix anything that is broken and they know how to fix
    - No to little branching; faster integration and minimizes merging work
    - Each subdirectory has at least two owners (or inherits them) who have write approval
    - Building and testing any software in the repo is extremely simple and fast
        - Highly optimized (caches, determinism, etc) and distributed over Google's cluster (upwards of thousands of machines per build)
- Code review tools
    - Presubmit checks and tests
    - If a bug is later discovered, the change introducing the code is commented on so the original authors are aware
    - **Size labels:**
        - 30-99: medium
        - 300-999: large
        - 999+: "freakin huge"
        - These labels can change for "special" days (e.g. pirate day)
- Testing:
    - All production code is expected to have unit tests
    - Load testing is done prior to deployment (e.g. errors, performance, etc)
- Languages:
    - Highly encouraged to use one of four approved languages (adhering to their style guides): C++, Java, Python, Go (and probably JS if it's browser related)
    - Experienced engineers will train others on readability, and non-trivial new code must be approved by someone who's passed readability training in that language
    - Interop is via Protobufs when possible
    - All languages have the same development process
- Releases:
    - Usually done frequently, weekly or fortnightly if not daily
    - Integration testing on staging is always done, either by the dev team, internal users, or sampled requests from live servers
- Lauch:
    - User-visible changes or design changes require approvals from people outside the engineering team that implemented it
        - Checks for legal, privacy, security, reliability, business requirements
- Post-mortems:
    - Any significant outage or reliability issue results in a post-mortem document detailing timeline, impact, root causes, what actions worked and didn't
    - Focus on the problem, and how to avoid or fix them in the future
- "Most software at Google gets rewritten every few years"
    - Rewriting old code that reflects outdated requirements and years of added complexity often results in leaner, simpler, and more robust code
    - Transfer knowledge and ownership to newer members
- OKRs (Objectives and Key Results)
    - Individuals and teams explicitly document their goals and frequently assess their progress towards these goals
        - Objective and measurable
    - Should be set high; target score is 65% completion; adjustments following data are made each quarter
    - Not used directly in individual performance appraisals
- Roles
    - Engineering Manager: always manages people, defers to Tech Lead for final say in technical decisions, responsible for selecting Tech Leads and team performance
    - Research Scientist: demonstrated research ability and ability to write code (most PhDs still fall into SWEs)
    - SWE: engineer
    - SRE: maintenance of operational systems
    - Product Manager: management of product, coordinate and prioritize work as customers (4:1 with SWE)
    - Program Manager: project and process management (30:1 with SWE)
    - Managing people is not a requirement for promotion, even at the highest levels; leadership can come in many ways
    - Transfers usually available after 12 months experience, and encouraged to do SRE rotation
- Performance
    - Money-bonus as well as purely social recognition awards are available

### How Complex Systems Fail

[Publication](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf)

1. Complex systems are inherently dangerous: they all pose risks (but we should be able to control their frequency and create defenses)
1. Complex systems are defended against failure: technical, human, organizational, institutional, and regulatory measures
1. Catastrophe usually requires multiple simultaneous failures: usually small, unnoticed failures joining together
1. Chance of failure is always changing in complex systems: technology, organization, efforts to reduce chances of failure
1. Complex systems are broken: they're only up because of the redundancies and human effort, and these are often replaced
1. Catastrophe is always just around the corner
1. There is never a single "root cause": there will always be many simultaneous contributors (but perhaps only a few "root" causes that allowed for these contributors to manifest at the same time)
1. Human performance is always easy to blame in hindsight: when you're in the situation, it's usually not so obvious what or if something went wrong
1. Humans are responsible for producing products and defending against failure: normally biased on maximizing production until something goes wrong, then blame is based on maximizing defense
1. All human actions are gambles: accidents are never inevitable, and usually humans actions causing failure are not deliberate (or disregarding); remember that actions leading to production are also gambles
1. Organizational pressures are often ambiguous: human actors are often influenced by targets or adverse pressures, especially when violating rules or skipping procedure
1. Humans adapt systems to maximize production and minize accidents moment by moment
1. Human expertise constantly changes: often a mix of scarce expertise available for demanding tasks and need to develop future expertise is present
1. Change leads to new forms of failure: we often trade off low-impact high-frequency failures for high-impact low-frequency failures by adopting newer technology
1. Trying to fix a "cause" limits effectiveness of existing defenses against future events: "end-of-the-chain" measures hide the real problems, and the chance of the exact same failure happening may be rare due to constant changes in the failure mixture
1. Safety comes with the whole, not the components: safety (as a whole) can't be compartmentalized, purchased, or manufactured
1. People create safety: only people keep systems within their tolerance boundaries
1. Becoming failure-free requires failure: only intimate contact with failure provides experience one can use to avoid future failure

### Deep Learning

[Publication](http://www.nature.com/nature/journal/v521/n7553/full/nature14539.html)

- Prior to deep learning algorithms, ML techniques were limited by their ability to process information in a raw form
    - Figuring out how to reduce the raw input into a form usable by a classifier was super difficult and required deep domain expertise
- Representation learning: allows a machine to automatically discover usable representations of the raw data
    - **Deep learning: kind of like recursive representation learning; (endlessly) composable transform functions on raw data to amplify and disregard certain details**
        - None of this is engineered; they're learned through a general purpose procedure!
- Backpropagation: despite only knowing the error from the outcome, backpropagation properties mean that every layer can be adjusted ("learned") to fit the data
- Stochastic gradient descent: split your training data into small samples and iteratively adjust weights (sounds a lot like the *lean* "fail fast and adjust cheaply")
- Convolutional neural networks: designed to process data that comes in multiple arrays
    - Kind of like a MapReduce (convolution -> pool) operation at each layer?
- Recurrent neural networks: better for sequential inputs
    - Kind of like a state machine processing inputs
    - Good for figuring out what the next word might be, or the "thought" in a sentence (really analagous to the sentence's "state")
    - E.g. English to French translation: RNN interprets thought of English and feeds it to a French network who then uses it as input to sequentially generate words (Holy Shit!)
- ConvNet -> RNN example: ConvNet to encode raw picture into a form usable by an RNN to produce a sentence
- Now we're building neural nets with memory (e.g. neural Turing machines), enabling them to hold state and answer questions on that state
- Future: combining deep learning and reinforcement learning (e.g. image recognition but with the ability to focus on particular parts, NLP but with ability to focus on specific parts of a document for state building, etc)
    - Combine representation learning with complex reasoning

### Fallacies of Distributed Computing Explained

[Publication](http://www.rgoarchitects.com/Files/fallacies.pdf)

- Also see [original](http://nighthacks.com/jag/res/Fallacies.html)

1. The network is reliable
    - Literally anything and everything will fail, especially things not under your control
    - Trade-off redundancy for risks of failure in hardware and communication protocols (messages lost, unordered, etc)
1. Latency is zero
    - Unfortunately, we can't teleport atoms (yet?)
    - More inherently difficult than bandwidth to increase and make reliable
    - Calling remote services is expensive!
    - Stress test applications for latency
1. Bandwidth is infinite
    - As bandwidth grows, we usually find ways to use more of it
        - Be mindful of how much you're expecting the underlying network to handle
    - Packet loss across WANs can be very large and be the bottleneck for performance, where the only solution is to increase packet sizes
1. The network is secure
    - Security from Day 1 during architecture and use threat modelling
1. Topology doesn't change
    - Network topology is usually out of your control; don't depend on constant routes without a Plan
1. There is one administrator
    - Administrators (of your network) will probably not be under your control; you'll have to think about coordination
1. Transport cost is zero
    - Serialization / marshalling across a network costs performance
    - Using a network has inherent costs
1. The network is homogeneous
    - Users will not be running the exact same machines as you are; think about portability (and standardized protocols) from Day 1

### What are Bloom filters?

[Article](https://blog.medium.com/what-are-bloom-filters-1ec2a50c68ff)

- Data structure that's good at answering "is this item in the set?" (approximately; false positives can occur)
    - O(c) for adding items and asking presence
    - Uses multiple hash algorithms on the same data to create multiple identifiers that must be checked for existence
        - False positives occur when there's too many items relative to buckets and an item hashes to ids that have already been used by other items
- Can't remove items from the set

Life
----

### Batesian Mimicry: Why Copycats are Successful

[Article](https://www.farnamstreetblog.com/2016/12/batesian-mimicry/)

- The more impressive something is, the more effective the copycat
- Law of nature: success will be copied, but remember that the copy is just a fake!
- The only person who can tell who's the real deal is the one being copied

### Second Level Thinking

[Article](https://www.farnamstreetblog.com/2016/04/second-level-thinking/)

- First order thinking: having an opinion
- Second order thinking: why? To what extent? Possible outcomes? What happens next? How could I be wrong?
- Only way to be successful: you have to be **different** and **correct**
- Don't be unwilling to be wrong out of fear of your ego! "You never look like a fool if you look like everyone else."

### Activation Energy

[Article](https://www.farnamstreetblog.com/2017/06/activation-energy/)

- Activation energy: minimum required energy needed before something will happen (to overcome inertia)
- Catalysts: speed up a reaction by lowering the necessary activation energy
- The bigger the change, usually the higher the activation energy

### Occam's Razor

[Article](https://www.farnamstreetblog.com/2017/05/mental-model-occams-razor/)

- Among competing hypotheses, the one with the fewest assumptions should be selected (i.e. the simplest solution is correct)
- Don't use it to mask up confirmation bias in considering what's "fewest assumptions" and "simplest"

### Attrition Warfare: When Even Winners Lose

[Article](https://www.farnamstreetblog.com/2017/07/attrition-warfare/)

- "When you do as everyone else does, don't be surprised when you get what everyone else gets." -- Peter Kaufman
- Clever, decisive victories are usually much more useful than winning via attrition
- Moral is key in attrition warfare
- Attrition warfare usually leads to sunk-cost fallacies that sustain the war longer than it should
- Realize you're in a war of attrition, and you can opt out
- Use asymmetric weaponry; don't do what everyone else is doing

### The Trojan Horse: How Marketers, Retailers, and Artists Conceal Their True Intents

[Article](https://www.farnamstreetblog.com/2017/07/trojan-horse/)

- Marketers hide their secrets in gifts; offer something free, and then upsell
- Lower defenses for challenging ideas by packaging it in a form that appeals to them (e.g. art, music, etc)
- Good uses of the Trojan Horse are ones that are not yet recognizable
- **"A good heuristic when things seem too good to be true is to just forget about them."**
- Good example: making income from non-obvious revenue streams (e.g. those not in the direct line of business; cinemas off of concessions)
- Permission marketing: delivering messages to people who actually want them; a recipient paying attention is something to be prized!
- Getting someone to like you: try asking for a favour from them (Ben Franklin effect)
- Use selective honesty -- open-hearted gestures bring down suspicions
- **"When confronted by something difficult or thorny, do not be distracted or discouraged by its formidable outer appearance; think your way into the soft core, the center from which the problem blossoms"** -- Robert Greene

### Proximate vs Root Causes: Why You Should Keep Digging to Find the Answer

[Article](https://www.farnamstreetblog.com/2017/05/proximate-vs-root-causes/)

- Look beyond the superficial, easily perceived causes, and get to the underlying foundations
- Look at predisposing factors; relevant factors to the root cause (e.g. location, severity, time, factors preventing being more severe, etc)
- Root cause: the most basic reason for an undesirable condition or problem which, if eliminated or corrected, would have prevented it
- Don't allow yourself to swim in self blame or negative thought spirals; focus on the future not the past
- Socratic questioning:
    1. Clarify thinking and explaining origins of ideas
    1. Challenging assumptions
    1. Looking for evidence
    1. Considering alternative perspectives
    1. Examining consequences and implications
    1. Questioning the original questions
- Use with other models (e.g. Hanlon's Razor, Occam's Razor, etc) for great effect

### The Map is Not the Territory

[Article](https://www.farnamstreetblog.com/2015/11/map-and-territory/)

- A description/abstraction (map) can not substitute for the real thing
- Remind yourself that a map has limits! It may be wrong in some ways; it may oversimplify some things; you may interpret it mistakenly!
- Remind yourself not to over-apply powerful models or abstractions!
- Don't let past experiences blind you in new situations; reasses, reasses, and determine what the new conditions are before allowing yourself to apply what you've learned before
- **"A model might show you some risks, but not the risks of using it"** -- Nassim Taleb
    - Understand that the parameters that go into making a model may be misinformed, or using data that doesn't do a good job of predicting the future
    - Frequently, we're blind to the fact that models using historical data can't say anything about what they haven't seen yet; in a lot of cases, we just haven't seen something yet (e.g. we can only expect the previous worst case until a new worst case happens)
    - Notice when we try to spin myths about the future by using backwards-looking, trend-fitting models
- When using models, think about what you're trying to do: optimize or survive?
    - If you're looking for survival, make sure the tails of a statistical model don't kill you. Assume worse than the worst.
- **Respect the limitations of any abstraction or model you're using**

### Thought Experiment: How Einstein Solved Difficult Problems

[Article](https://www.farnamstreetblog.com/2017/06/thought-experiment-how-einstein-solved-difficult-problems/)

- Thought experiments are a structured manifestation of our natural curiosity about the world
- Complex information is best digested as a narrative or analogy
- Types of thought experiments:
    - Prefactual (on future outcomes)
    - Counterfactual (contradicting known facts)
    - Semi-factual (how would things change if the past was different?)
    - Prediction (future outcomes based on existing data)
    - Hindcasting (knowing an outcome, what could have predicted it?)
    - Retrodiction (going backwards to find the root cause)
    - Backcasting (how to get to a future outcome)
- Our brains work differently depending on the context; e.g. push a button -> brain uses rational areas, push a person -> brain uses emotional areas


### Reciprocation Bias

[Article](https://www.farnamstreetblog.com/2017/09/reciprocation-bias/)

- Reciprocation doesn't just happen on good events, they also happen on bad events (leading to positive feedback cycles of negativity)
- Avoid reciprocating hositility by delaying your reaction
- Reverse negativity by doing something positive (especially if it feels undeserved!)
- Advance relationships by displaying generosity
- Relationships: provide what is needed, when it is needed (rather than unnecessary generosity)
- Sales: focus on the experience, not the exchange of goods and their price
- Notice the tendency when you are (or a delegate is) in an exchange as an agent for someone else; you may be benefitting at the expense of the whole
- **Something more subtle than exchanging gifts: the person who acts in a certain way toward us is entitled to a similar return action**
    - If you give a concession (e.g. smaller item to sell), they might give one back (buy the smaller thing)

### A Primer on Critical Mass

[Article](https://www.farnamstreetblog.com/2017/07/critical-mass/)

- "When enough people (a critical mass) think about and truly consider the plausibility of a concept, it becomes reality." -- Joseph Duda
- F\*\*\* you money: "it shields you from prostituting your mind and frees you from outside authority — any outside authority" -- Nassim Taleb
- Be careful in group settings; usually the strong have power over the weaker
- Most technology exhibits a network effect: the more people have them, the more useful it is
- "The more people who believe a story, the more believable it seems." -- Groupthought?
- Types of people for creating critical mass:
    - Connectors: highly socialable and connected to people with influence
    - Maven: the expert (for sharing reliable information)
    - Salesmen: negotiators and masters of persuasion
- Stickiness: how fast do users drop off?
- **Only about 10% of a population is needed before a switch from minority to majority -- get to this point to get to growth!**

### Peter Bevelin on Seeking Wisdom, Mental Models, Learning, and a Lot More

[Article](https://www.farnamstreetblog.com/2016/10/peter-bevelin-seeking-wisdom-mental-models/)

- Decision making is not about making brilliant decisions, but avoiding terrible ones (don't be stupid!)
- Make it easy for yourself to avoid harm (e.g. heuristics, filters, etc); focus on simple, and have a foundation
    - Filter: you haven't understood something if you can't describe it simply
- "A reward that feels controlling and makes us feel that we are only doing it because we’re paid to do it, decreases the appeal"
- "Intuition is nothing more and nothing less than recognition" -- Herbert Simon
- Missing events, or negative evidence, that normally should be present for a hypothesis to be right, should be red flags!
- Focus on simplifying and clarifying, distilling everything down into just the key factors and everything else (to ignore)
- "There is a certain natural tendency to overlook anything that [is] simple and important"
- "A majority of life's errors are caused by forgetting what one is really trying to do" -- Charlie Munger
- Don't anchor on predictions, focus on prevention (of fatal mistakes), robustness, ad adaptability
    - On predictors: "often these are the people who live in a world where their actions have no consequences and where their ideas and theories don’t have to agree with reality"

### Compress to Impress

[Article](http://www.eugenewei.com/blog/2017/5/11/jpeg-your-ideas)

- Ideas and messages travelling through degrees of people will distort them; make your messages concise, memorable, and catchy to keep them undistorted, and then keep repeating them
    - Key of communication: maintain maximam recall in others
    - Is everybody able to recall the current top priority of the business at any given time?
- **Genius: state the complex simply**: find the most elegant and stable output from a complex universe of inputs
    - Consume unfiltered (no lossy, no lazy thinking), output concisely
- "At scale, maintaining strategic alignment feels like an organizational design problem, but... organizational design is centered around how it impacts information flow"
- **"People fret about what others say about them when they're not in the room, but Jeff was solving the issue of getting people to say what he'd say when he wasn't in the room"**

### Social Engineering 101

[Article](http://hintjens.com/blog:21)

- "Software is all about the people"
- Kinds of relationships:
    - Those that you cannot make work
    - Those that will always be good
    - Those that you can profitably invest in; based on the economics of mutual needs, as revealed over time
- Social interactions is all about ethics: the balance of relative power between parties
    - **If you wouldn't switch sides in a deal, it's unethical** (interesting way to look at fairness and ethics)
- Engineering a social session: define a clear goal, set your mind to degrees of happiness, charm, determination, and patience
    - (Obviously) avoid incoherence, stress, unpleastantness, uncertainty, or impatience
    - Realize and turn off negative emotional responses so you're just left with joy to express
    - Create an experience that the other party *wants* to be in!
- *Suggest* (rather than demand) that the other party is able to solve a clear problem of yours -> this clarity drops our guard and gives us joy
- Charm: enjoy what you're talking about, and speak directly to the person
- Determination: a "no" is just one closed path; explore all possible routes from the problem to the goal (don't give up at the first no!)
- Patience is contagious; you'll make time to solve your problem if you care about it (and the other side will see that)
- Confidence is also contagious; if you know you're going to succeed, the other side will be infected
- People love to say "no": it gives them a feeling of power; don't give them any potential barriers to deny you
- Fashion: expressing yourself through your appearance is just narcissism, shift styles as needed to fit in so that the other party puts you as "us" rather than "them"
- Service jobs suck: most people are by default in a mix of boredom, loneliness, jealousy, or hate; lift up their day and make it to your advantage
- Gender differences: women open up to smiles and confidence, men open up to confidence and touch
    - Approaching male groups: find alpha, randomly chat without emotion (especially fear), firmly shake hands, shoulder slap, address rest of group
- **"You won't ever do better than you aim for"**

### The Cretan Method

[Article](http://hintjens.com/blog:81)

- As we remove all the provably wrong, we approach truth (but can never actually achieve truth)
- **Learn to differentiate between scientific theories and *magical* theories (those that cannot be proven right or wrong; they are "Not even wrong")**
    - Scientific theories can be falsified and improved; magical ones just float as opinions (an infectous mental disease)
- Emotional restraint is more effective and less risky than physical restraint for humans; try to notice when someone is trying to prey on your theory process by injecting magical theories
- Children's minds are uncluttered with magical theories about the world (and society)
    - **Seek childlike intuition**
- Pain is a valid data point; you don't like it for a reason (and do something about it, don't just accept it!)
    - Note that all theories are broken sometimes, and other things may be more important than minor pain
    - A magic theory will only cause pain when you try to use it seriously
- A good theory works smoothly and almost silently; a poor theory causes friction (irritation, cost, delay, stress)
- **Improve your theories, or discard them**
- Asymmetrical relationships: abusive relations have significant debt on one side (but we often justify them to ourselves via emotional attachment)
    - Promising future payoffs cheats this relationship; one party will likely invest based on this promise true or not and is likely to view the relationship advancing when it really is not
    - Challenging those stuck results in confrontation; the invested party is stuck in sunk cost bias
    - Only two ways out: either the party being cheated has nothing left to give (and gets discarded), or that party realizes the truth or blows up after not being able to justify a demand
    - We try to discount the future, but if one party simply adds ridiculous amounts of power or money, it'll still be enticing
    - **Same with theories: "theories that are excessively complex, and promise future payoffs, are a form of advance fee fraud"**; don't get misled into heavily investing into something that only promises "power" (note that it's mostly fake or mythical power)
- One view of emotions: they're social communication tools, designed to let us manipulate others' behaviour
    - We often express our own pain as anger towards others
    - **"Emotion is valid as data, yet invalid as a process"**
    - You might be able to discern the level of magic vs science in a project by the level of emotional responses
- **Process of improvement (group exercise):**
    - Observe friction in a social setting
    - Discover or guess the underlying theories
    - Identify the flaws in those theories
    - Improve the theories, or discard
    - Test your improved theories
    - Repeat until it gets boring
- "Smart people often use their intelligence to compensate for friction" (by rationalizing rather than acting to remove annoyances)
- "There is no social friction in solitary"
- Thinking / learning process:
    - *Learn* (from others)
    - Test the new knowledge by *playing* with it
    - Apply it to real problems through *work*
    - *Teach* the knowledge to others
- We've broken this thinking process to separate stages in modern society: play as children, learn when young, work as adults, and die (teaching is left as work as well)
    - This separation favours magical theories; during our learning phase, we never get to test what we're learning on practical problems (so lazy thinking is more acceptable)
        - **Society is saturated with magical theories**
    - Somehow, we've become socially addicted to non-confrontation; it's usually not socially acceptable to negate someone's views in public (unless it's obviously up for debate)
    - Society disowns anyone who tries to go against this four-stage process to define their own life, although those who succeed as re-christened as demi-gods
- Power of the monologue: "send your audience into a sleep state where they will accept anything" (magical theories)
- **The best pattern for learning and teaching is the dialogue**; present your theory, ask for others to negate it, and gain an improved theory after
- Over-complex is actually over-engineered; it takes real work to turn complexity into simplicity
    - Complexity grows as you throw more problems at a theory; untamed complexity is a problem to solve (via abstraction with a grander theory)
- **"Lies tend to hide in complexity"**; the simpler something is, the easier it is to negate it
    - **Simplicity always beats complexity**
- "We all pretend we know what we're doing. This industry is always confident, especially when it has no clue" -> hits home real hard man
- Grounding: remove negative emotions by negating their root theories (what they're trying to convince in you by manifesting in you)
    - Self-pity: cry for adult affection; theory: I'm a needy child who's spoiled
    - Jealousy: cry for attention in contention to another person; theory: bully this person into spending time
    - Anger: determination to fight; theory: showing anger will force the other person
    - Fear: showing stress at looming danger; theory: someone will come save me if I show fear
    - Sadness: show stress at losing something; theory: someone will come make things right
    - Shame: showing stress at being diminished in front of others; theory: we'll be secluded from others
    - Guilt: showing fear of shame; theory: maybe we'll be forgiven if we show how bad we feel
    - Loneliness: showing hunger to belong; theory: people want us because we look sad (lol)
        - E.g. this only works for babies; showing a smile is a lot better for being acceptance than being sad

### General and Surprising

[Article](http://paulgraham.com/sun.html)

- Surprising and general insights are hard to come by (they're *big* revelations)
- You can try to make something surprising more general (generalizing gossip to insight)
- Or you can try to make something general more surprising / novel
- Most of the time, you only need a small delta from where you started to get useful insights

### The Difference Between Open-Minded and Close-Minded People

[Article](https://www.farnamstreetblog.com/2017/09/open-closed-minded/)

- Don't fool yourself into thinking you're open-minded (nobody is, all the time)
- Don't be afraid to be wrong; it's a learning opportunity and a chance to refine yourself
    - Ask questions, expand ideas, and probe reasoning for disagreement rather than reaffirming your views
    - Don't assume misunderstanding when they're actually in disagreement
- Get the best outcome, not what you think is "right"
- "Open-minded people know when to make statements and when to ask questions"
- Don't let one idea take hold of your mind; be open to weighing opposing ideas at the same time
- Choose when to be open minded; some things (e.g. illegal or physically impossible) should be easy to close out

Random
------

### Amazon 2016 Letter to Shareholders

[Article](https://www.amazon.com/p/feature/z6o9g6sysxur57t)

- Jeff even works in a building called "Day 1", and moved the name when he moved buildings. **Wow**
- Day 2: statis -> irrelevance -> painful decline -> death
- Many large, established companies are busying harvesting Day 2; stay vigilent and stay on Day 1 if you don't want the death sprial to begin
- Staying on Day 1:
    - Customer obsession (customers are always dissatisfied, no matter what they report, and it's your job to find out how to make them *less* dissatisfied)
    - Skeptical view of proxies (anything that masks the end result, e.g. process; do we own the process or does it own us?)
    - Eager adoption of external trends (otherwise, they'll make you be on Day 2)
    - High velocity decision making (if the decision is reversible, who cares if you're wrong and you notice it quickly enough?)
        - **Disagree and commit: don't wait to convince; even if we disagree, commit to a single action and test it together**
        - **Recognize misalignment, and escalate immediately**
- Product owner: understand the customer, have a vision, love your offering
