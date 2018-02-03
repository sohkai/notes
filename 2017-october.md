October 2017
============

Tech
----

### Onward with Ethereum Smart Contract Security

[Article](https://blog.zeppelin.solutions/onward-with-ethereum-smart-contract-security-97a827e47702)

- Fail as early and loudly as possible
    - (Particularly in Solidity) hidden errors can kill you; prefer to throw or avoid default states if you can
    - Separate preconditions and make each fail (for good errors)
    - Think about ways for your contract to safely recover
- Favour pull over push payments
    - Never trust that a `send()` will execute without error (**whenever you call a contract, especially one you don't have control over, expect it to fail!**)
    - Prefer not to call `send()` while already executing a function
    - Separate payments into a different function, where others call to receive (pull) a transfer
- Structure your functions as:
    1. Check preconditions
    1. Make changes to state
    1. Interact with other contracts (if they fail unexpectedly, your state will be rolled back so you can try again later)
- Be aware of platform limits
    - Avoid implicit types (`var`) unless you know **exactly** what values a variable can take (even then, it's probably not good for others)
    - Be careful of gas, especially in loops (avoid calling potentially expensive functions)
    - Be aware that an attacker may put your contract above the call stack, causing any further `send()`s to silently fail
- Write tests (duh)
- Fault tolerance and automatic bug bounties
    - Wrap contracts around a `Bounty` that researchers can claim if they've proven some invariants in the contract (or a duplicate) are broken
    - Add pause or halt button to the contract
- Limit the amount of funds deposited
    - You can make it so that the contract doesn't accept more deposits than a set number
- Write simple and modular code (duh)
    - Especially important for solidity, you should understand every state your contract could possibly be in
    - Events should start with "Log"
- Don't write all your code from scratch (duh)

### Ethereum Contract Security Techniques and Tips

[Repo](https://github.com/ConsenSys/smart-contract-best-practices)

- Cost of failure is high, change is difficult (see hardware or financial technology)
    - Prepare for failure: pause when broken, limit amount of money at risk, future upgrade path
    - Rollout carefully and provide incentives as soon as possible to test and break contract
    - Keep it simple
    - Stay up to date
    - Know and be careful of blockchain properties: use extreme care with external contract calls, your public functions can be called by anyone, all data is public, limit gas costs
- Notice the balance you'll have to make between *software engineering* and *security* biases; consider the time frames as well (short-lived may be more inclined towards *security*)
    - Rigid versus Upgradeable: upgradability adds complexity and more attack surfaces
    - Monolithic versus Modular: modular adds more complexity and hides knowledge
    - Duplication versus Reuse: to be safe, you might have to duplicate code that you don't have control over
- Best practices
    - External calls
        - Avoid when possible; every external call is a potential security risk–assume that it will be malicious
        - Use `transfer()` when possible; both `send()` and `transfer()` are considered safe against reentrancy due to their low gas stipends (only enough for logging an event)
        - If you use `.call()`, `.callcode()`, `.delegatecall()`, or `.send()`, make sure to check their return code for failure
        - Isolate each external call into its own "pull" transaction (initiated by the recipient), especially for payment
        - Make it obvious when using an external contract (e.g. by using an `Untrusted` variable name)
        - Any function calling a function depending on an untrusted contract is also untrusted
    - Enforce invariants with `assert()`, validate inputs with `require()`
    - Precise math is hard; if you need perfect accuracy, store both the numerator and denominator
    - Self destructing contracts can forcibly send ether to an account
    - Ether can be sent to an address before a contract's created; don't assume the initial state will contain no ether
    - All data is public
        - Use enrypted blind auction techniques that check for validity of submissions after
        - Always generate random number after all submissions
    - In multisig or multiparty contracts, be aware that some participants may disappear forever
        - Provide a way of reaching settlement without all parties (no deadlock, liveliness)
        - Provide incentives to keep participation
    - Fallback functions usually only have 2300 gas (only enough to log an event)
    - Mark visibility in functions and variables
    - Lock pragmas to a specific compiler version
    - Differentiate functions and events (start with lowercase for functions, prefix events with `Log`)
- Known attacks
    - Race conditions
        - External contracts may hijack control flow, causing changes to your internal state before the original function finishes
        - Reentrancy: functions that could be called repeatedly
            - Use `send()` to limit recursion attacks
        - Cross-function race conditions
            - Be careful of an attacker calling another function (especially in another contract) that changes the same state
        - Complete all internal work before calling external contracts (as well as internal contracts that call external contracts!)
        - Use a mutex (more useful in simple situations), but be careful that they will always be released once held
    - Front running
        - The order of transactions can be manipulated by using fees or miners (who can include transactions working against you, e.g. in an exchange)
    - Timestamp difference
        - Miners can manipulate timestamps and should not be trusted if time is critical (use an oracle instead)
    - Integers can overflow and underflow
    - Denial of service via unexpected exceptions (external contracts can maliciously fail to deny a contract's full operation)
    - Denial of service via gas limit
        - Avoid looping over unknown sizes, but if you must, try to take multiple blocks (via multiple transactions)
- Software Engineering Techniques
    - Upgrading broken contracts
        - Use a registry contract or a contract that forwards calls and data to the latest version (`.delegatecall()`)
        - Separate complex logic from your data storage, to avoid recreating all of the data to change functionality
    - Include circuit breakers
    - Speed bumps and rate limits
        - Intentionally speed down some actions to allow reaction to malicious attacks
    - Rollout: test, test, and test everything in every environment
        - Force automatic deprecation
        - Restrict amounts / user
    - Bug bounties
- Documentation
    - Specifications, rollout plans, current status, known issues, history, changelog, processes for unexpected events, contact info

### The Idea of Lisp

[Article](https://dev.to/ericnormand/the-idea-of-lisp)

- "John McCarthy wrote 6 easy things [`atom`, `eq`, `cons`, `car`, and `cdr`] in machine code, then combined them to make a programming language."
    - Everything can be defined in terms of those 6 things
- *Universal* machines: when they can interpret any other Turing Machine
    - Lisp defined its interpreter via itself; it can interpret its own code
- The meaning of expressions are defined by the interpreter (holy shit!); we can hotswap meanings to avoid making too many early assumptions
    - These expressions are encoded in a way interpretable by Lisp itself
- Features:
    - Macros: code transformers
    - DSLs created from the same principles
    - Fast experimentation of alternative semantics
- "Most people who graduate with CS degrees don’t understand the significance of Lisp. Lisp is the most important idea in computer science." -- Alan Kay

### A Tool For Thought

[Article](http://swannodette.github.io/2016/06/03/tools-for-thought)

- Describing programs (*crispness* vs *correctness*) and actually writing them are two different tasks

### A Five Minute Guide to Better Typography

[Article](http://pierrickcalvez.com/journal/a-five-minutes-guide-to-better-typography)

- Tool for **effective communication** (and a bit of delight)
- "Type is a beautiful group of letters, not a group of beautiful letters" -- Matthew Carter
- Heuristics:
    - Think in blocks
    - Align with your eyes
    - Skip a weight
    - Multiply size by two
    - Line-spacing of 1.2x to 1.5x the font size
    - Between 40 and 70 characters per line
    - 14-25px is easier to read
- Dashes:
    - Dash: hypening
    - EN: range
    - EM: break in clause

### Solidity Workshop

[Workshop](https://github.com/androlo/solidity-workshop/)

- Constructors, Classes, and Contracts
    - Realize that partially initialized contracts exist, and that they may be dangerous
        - A contract is only fully initialized after its constructor has returned; before that, only the data and constructor are deployed (so no fallback, other methods, etc)
        - Avoid calling untrusted contracts in a constructor, and especially be wary of reentrant `callcode()`s and `delegatecall()`s

### Concurrent Programming for Scalable Web Architectures

[Thesis](http://berb.github.io/diploma-thesis/)

4. Web Server Architectures for High Concurrency
    - Performance: resource utilization should scale with increasing work
    - I/O operation models: blocking vs. non-blocking, synchronous vs. asynchronous
    - Multi-threaded and multi-process: synchronous, blocking threads/processes where each handles a single connection at a time (easy mental model)
        - Context switching may become a problem if too many concurrent requests are being handled
    - Event-driven: asynchronous, non-blocking threads where each handles multiple connections using an event loop (usually a queue populated by events coming from the connections)
        - Complicated mental model with inversion of control flow, but less context switching
        - A build-up of requests can happen if the event processor is saturated; request latencies increase linearly
    - Non-blocking I/O multiplexing: application registers itself as a listener to specific events and the platform provides an event demultiplexer to dispatch incoming events to interested listeners
    - Threads vs events:
        - Both can be mapped into the other, with the same performance features; the question is about style, developer reliability, and properties of the underlying system
        - Pre-emptive scheduling of threads makes reasoning about them extremely difficult (and performance suffers from locking)
        - Keeping execution context state of event handlers is very difficult
        - Sweet spot: mostly serial execution with cooperative-scheduling but with language constructs that hide the details of managing an execution context (Node.js is a close example)
5. Concurrency Concepts for Applications and Business Logic
    - Transactional memory: lock-free concurrency via serializable, atomic transactions to shared memory; see Clojure
    - Actor model: no shared state between actors, mutable state is coupled exclusively to a single actor entity
        - Actors can send messages to other actors, spawn new actors, change its internal behaviour for incoming messages
        - Can only communicate to actors via asynchronous message passing (i.e. each actor has a mailbox)
    - Event-driven: no call stack D; ; decoupling of caller and callee and shifts responsibility to event handler to know who to route events to (rather it being the caller's responsibility)
        - Hilariously, JavaScript has no I/O or concurrency baked in, so Node could expose a purely async, non-blocking API for great profit
    - Synchronous message passing (CSP): explicit message passing between sender and receiver (both have to be ready and blocked waiting for the message to exchange)
        - Message exchanges are an explicit synchronization point
    - Dataflow programming: define relations between operations, resulting in a graph of dependencies that the runtime can analyze and parallelize
6. Concurrent and Scalable Storage
    - **Dealing with distributed system == expect failures to happen**
    - Distributing *computation* is easy, distributing *state* is hard!
    - PACELC as further model of CAP:
        - P: Given partition, choose availability (A) or consistency (C)
        - E: Without partition, prefer latency (L) or consistency (C)
    - Consistency models:
        - ACID: atomicity, consistency, isolation, durability
            - Enables linearization of transactions
            - To get more performance, weaker levels of isolation are used (repeatable reads, read committed, read uncommitted) by removing locks
            - Can also relax durability by buffering rights to disk
            - Distributed systems using ACID usually have to relax ioslation and durability because there is no global atomicity (consensus protocols are as close as we can get)
            - **Isolation and serializability contradict scalability and concurrency**
        - BASE: basically available, soft state, eventually consistent
            - Windows of inconsistency are allowed; best effort consistency
                - If these windows are small enough, users probably won't even notice (if they even noticed stale data in the first place)
            - Slightly easier for the application developer; writes should always be accepted (unlike consistent systems) so they don't have to do any of their own error buffering
            - Causal consistency: operations linked to each other are always processed in the same order
            - Read your writes consistency: clients will always be able to immediately see a value they've written
            - Monotonic read consistency: after a read, no subsequent reads will yield older values
            - Monotonic write consistency: serialize all write operations from a client
    - Transactions in distributed systems must either be applied to all machines or none (consensus)
        - Requires a managing service that coordinates transactions
        - Quorum-based voting protocols: mark executing transactions and wait for majority of nodes to either accept commit or abort state
    - Distributed concurrency control
        - Pessimistic: prevent conflict by strict coordination of transactions
        - Optimistic: delay conflict checking to the end of a transaction (expecting most transactions to not conflict)
        - Locking-based: use locks to ensure safe operation
        - Timestamp-based: use time counters (usually vector clocks) for safe operation (e.g. MVCC)
    - Consistent hashing is used to allow partitions with a fluid number of nodes; can be seen as a ring (where all items and nodes are mapped onto it, and the next node is responsible for holding the items before)
    - Replication:
        - Synchronous: atomic semantics by all running replicas (requires coordination)
        - Asynchronous: single nodes can independently acknowledge operations; not all nodes will udpate at the same time
        - Active: all nodes receive all requests, and coordinate their response
        - Passive: only designated primary nodes handle requests
    - Replication strategies:
        - Snapshot: periodic copying of all data
        - Transactional: propagate changes with transactional behaviour
        - Merge: synchronize data as nodes become available (requires conflict resolution strategies)
        - Statement-based: forwards queries
    - Partitioning strategies:
        - Functional: separate distinct parts of the data (not dependent on each other)
        - Vertical: data partitioning via allocating row data into tables (e.g. splitting a complex table into multiple tables, where the columns that change more often are located together)
        - Horizontal (sharding): portion rows into structurally equivalent tables, via partitioning keys that map rows to shards (e.g. a hash function or a fixed set for each partition)

### Session types in programming languages–a collection of implementations

[Article](http://simonjf.com/2016/05/28/session-type-implementations.html)

- Session types: type discipline for communication-centric programming; formal checks for conformance to protocols
    - "Types for protocols"; allow us to describe communication protocols as a type
    - Duality: the exact opposite of a possible input/output sequence (e.g. server is usually a dual of a client)
        - If client is `!string . ?int`, then server is a dual if it implements `?string . !int`; these are formally verified to not be in deadlock
            - `!`: output
            - `?`: input
            - `+`: internal choice
            - `&`: available selection
- Multiparty session types: encompasses interactions containing more than two participants
    - Describe the interactions in a top-down manner, via a *global* type (that get projected into *local* types for each participant)
    - See [Scribble](http://www.scribble.org/)
- Require *linearity*, where each session endpoint must be used exactly once

### The Three Parts of Security

[Article](http://www.erights.org/elib/capability/3parts.html)

- Intuitive security:
    - Keeping objects secret -> withhold authority to access (e.g. ACLs)
    - Protecting objects from modification -> withhold authority to modify (e.g. ACLs)
    - Preventing the misuse of objects -> no way to prevent once someone has obtained access
- Thinking about actors, and their agency: individuals and programs are both actors, but once our shells have been authenticated by us, the programs have free agency and we need to trust them (really, their authors)
- ACLs fail at security because they implicitly assume that the program will always be loyal to the person running it
- Protection via least privilege and confinement: only give rights to do something if it's necessary (e.g. capability for local modification and communication channels)
- Always follow: **"trust, but verify"** (made easier by blockchains)
- Confused Deputy problem: program instance can't tell whether it has the authority to do something via the user or the program itself, so the user can persuade the program into misuse
- **Capabilities: distributed ACLs?**

### From Functions to Objects

[Article](http://www.erights.org/elib/capability/ode/ode-objects.html)

- **Objects == Lambda Abstraction + Message Dispatch + Local Side Effects**
- Lambda-based technique for defining objects! (Capture state via closure and return function describing possible functionality via "messages")
- Closure'd state can be considered to be safe; only explicitly exposed functionality from a *composite* (of state and behaviour) are facets that can be externally referred to
- Dynamic Reference Graph: seeing the objects as a *fabric* of nodes connected by references whose topology enable computations (and topological changes)

### The Hidden Trap of Code Coverage

[Article](https://ariya.io/2012/09/the-hidden-trap-of-code-coverage)

- Statements can have "hidden" complexities by including multiple branches; rather than relying on statement coverage, you should be worrying about branch (code path) coverage

### Concurrency is not Parallelism

[Talk](https://blog.golang.org/concurrency-is-not-parallelism)

- Concurrency: *composition* of independently executing processes
    - Structure; *dealing with* lots of things
    - How we *express* the problem, and break it down
- Parallelism: simultaneous *execution* of (possibly related) computations
    - *Doing* lots of things (usually at once)
- With some designs, we can add more independent processes to improve performance (more things going on == speed increase -> counter intuitive)
    - More parallelism via better concurrent design
- If we've got the concurrency right, the parallelism will come (by adding hardware, etc)
    - **Concurrency enables parallelism, and makes it easy**

### CallSuper

[Article](https://martinfowler.com/bliki/CallSuper.html)

- 'Just subclass the method, and remember to start your method with a call to the super-class' situations => anti-pattern
    - Better to have "hook" methods, so the base method will always run and then can delegate to customized subclasses
- **"Whenever you have to remember to do something every time, that's a sign of a bad API"**

### The Two Pillars of Javascript

[Article 1](https://medium.com/javascript-scene/the-two-pillars-of-javascript-ee6f3281e7f3)
[Article 2](https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a4)

- Constructors violate open/close principle: call sites are coupled with object instantiation (changing constructor to factory breaks existing uses)
    - Javascript doesn't need constructors, because any function can return a new object (although, not really sure if this is a great argument)
- Classical inheritance is the tightest (and most unobvious) form of coupling code
    - Duplication by necessity: you can't rearrange the inheritance hierarchy, so you end up duplicating it
- "Good programming style requires that when you’re presented with a choice that’s elegant, simple, and flexible, or another choice that’s complex, awkward, and restricting, you choose the former."

### A Beginner-Friendly Introduction to Containers, VMs, and Docker

[Article](http://preethikasireddy.me/2016/11/27/a-beginner-friendly-introduction-to-containers-vms-and-docker/)

- Goal of VM and containers: isolate applications and their dependencies into self-contained units that can be run anywhere
    - "Build once, run anywhere"
- VM:
    - Runs on top of physical machines using a hypervisor
        - Provides the "hardware" for getting (and sharing) resources (especially if there are multiple VMs running at the same time)
        - Hosted: runs on the OS of the host machine (hypervisor has to go through the host OS for resources)
        - Bare metal: runs on the bare metal hardware, usually is the first thing installed on the machine
    - Usually has its own virtualized hardware stack, including OS
- Container:
    - OS-level virtualization by abstracting user space
    - Share the host's kernel with other containers
    - Compared to VM: no virtualized OS layer

### There's no such thing as "fat protocols"

[Article](https://www.evanvanness.com/post/166666272011/theres-no-such-thing-as-fat-protocols)

- Definition between "app" and "protocol" isn't really defined
- **Ethereum replaces your server, not your networking**
    - Inherent value of Ethereum will be based on its inherent capabilities, e.g. scalability or interoperability
    - Price of ether should be dependent by supply and demand of computational power
- Technology becomes commoditized
    - When underlying technology becomes commoditized, the value start to accrue higher up the stack

### DNS Management Basics

[Article](https://pressable.com/blog/2014/12/04/dns-management-basics/)

- Domain registrar: probably where you bought your domain
- Nameserver: identify which servers to obtain DNS records for your domain
    - Your domain's nameservers should be pointed to where you're managing your DNS records
- DNS Zone: container of all DNS records for a specific domain (e.g. example.com)
- Records:
    - Usually only need to use: A, CNAME, MX (email), TXT, SPF
        - A: point domain to an IP address
        - CNAME: point domain to an existing hostname
        - MX (Mail Exchanger): route email; includes priority to indicate order in which servers should be attempted
        - TXT: text-based information (usually SPF and ownership info)
    - Name: descriptor and effective subdomain (e.g. blog for blog.example.com)
    - Value: where you want the record to point (IP or domain), or what to do (e.g. mail servers for MX)

### Encrypted Data for Efficient Markets

[Article](https://medium.com/numerai/encrypted-data-for-efficient-markets-fffbe9743ba8)

- "Claim: To solve a machine learning problem, open participation is key."
- Open participation is missing on the stock market
    - Most stock market data isn't publicly available
- Claim: increasingly effective machine learning algorithms will improve efficiency in markets
- Structure-preserving encryption schemes allow machine learning algorithms to learn without knowing what they're learning

### Super Intelligence for the Stock Market

[Article](https://medium.com/numerai/invisible-super-intelligence-for-the-stock-market-3c64b57b244c)

- Combining intelligence will be key in advancing machine learning
    - E.g. Random Forest -> combined many independent decision trees into a forest
    - E.g. Dropout -> combined intelligence from different neural networks

Life
----

### Why we should all stop saying “I know exactly how you feel”

[Article](https://ideas.ted.com/why-we-should-all-stop-saying-i-know-exactly-how-you-feel/)

- You probably don't; let the other person be heard instead!
    - *Support* and acknowledge their story, and what they're feeling
    - Don't *shift* attention away from them to yourself
- Conversational narcissism: "the desire to do most of the talking and to turn the focus of the exchange to yourself" -- Charles Derber
- Most social conversation time is actually devoted to talking about our own experiences or relationships, or to parties not present (rather than the othe party)
- We tend to use our own feelings to determine how others feel

### The Most Intolerant Wins: The Dictatorship of the Small Minority

[Article](https://medium.com/incerto/the-most-intolerant-wins-the-dictatorship-of-the-small-minority-3f1f83ce4e15)

- Complex systems: the interactions between components matter more than their individual natures
- Minority rule: we usually have a naive impression of why a preference exists; it's probably because of a small minority that won't budge
    - E.g. kosher drinks: 0.3% of US population is kosher, but almost all drinks are kosher; this allows producers, distributors, and retailers to not have to care
        - Is the cost higher to create an environment where you don't have to care, or is it most costly to produce different goods?
    - "An honest person will never commit criminal acts but a criminal will readily engage in legal acts."
    - **An asymmetry in choices: the flexible will have to bend to the *intransient*'s will**, given:
        1. Even spatial distribution
        1. Small cost differences in the choices
    - A "renormalization" occurs as the intransient forces their choices on successively more and more people by interacting with them
- "Decentralization is convex to variations"
- "Genes follow majority rules; languages minority rule"
- Religions spread and die following the asymmetry:
    - Islam forces a child to be Muslim if either parent is Muslim (stronger)
    - Judaism only forces a child to be Jewish if the mother is Jewish (weaker)
    - Christians were intolerant of the Roman pantheon, whereas the Romans allowed the Christian faith
- Moral virtues and civil rights are likely to come about because of the most intolerant person rather than consensus
- "Outcomes are paradoxically more stable under the minority rule"
    - Variance of results is lower, and rule more likely black and white
    - Majority rules are more likely to fluctuate around an average following, rather than everyone
- Do we need to be *intolerant* toward intolerant minorities to save our own *tolerance*?
- Markets: same deal, ruled by the most motivated
    - Those who want to get out will not change their mind, and the market follows
- Science: once you prove (or disprove) something, it is now held by the majority
- To move the needle: **"all one needs is an asymmetric rule somewhere"**

### Don't Scar on the First Cut

[Article](https://signalvnoise.com/archives2/dont_scar_on_the_first_cut.php)

- Policies will usually compound and add up to extreme rigidity
    - Avoid situations where it's "I'm just following policy"! => Don't treat the proxy as the real deal
    - Don't set and forget; update them
- **Embed learnings as stories (e.g. post-mortems?), and then use them to inform similar decisions later**

### Structuring Optimal Token Sales Admist 2017's ICO Mania

[Article](https://techburst.io/structuring-optimal-token-sales-amidst-2017s-ico-mania-27d6fff45cba)

- Tokens that are money tokens (medium of exchange, unit of account, and store of value) appreciate in value as their prices increase (e.g. Bitcoin)
    - Value from deeply ingrained societal myth; positive feedback loop
- Value tokens are different from money tokens!
    - Currencies within their mini-economy; price goes towards underlying economic value from network (i.e. actual usage)
        - No underlying store of value outside of network usage
        - Narrower use cases
    - Strong positive-feedback loops; if price goes up, network usage goes up via incentivization (and vice-versa)
- Real currencies get valued via the quantity theory of money: **MV = PQ**
    - Economic activity equals market cap * frequency of money changing hands (velocity)
- Real equity gets value from expected DCF, whereas a utility token does not (really skews valuations)
- IPOs: opens much deeper pools of capital
    - Usually sell 10-15% on first traunch (as opposed to rand(100) for ICOs)
    - Initial valuation is super important!
- "There's no asset that's a good buy at any price"
- **Psychological causes: greed, fear of missing out, envy, and self-deceit**
- Incentives are not aligned if founders can raise at arbitrarily high valuations!
- ICO structure:
    - Set a fair valuation, using *actual* expected usage of the network as the benchmark
    - Standarize to consistent structure across all ICOs
    - Questions to ask:
        1. What should the valuation be?
        1. How do I make sure to get tokens in the hands of as many long term holders or users as I can?
        1. What % of the protocol should be used?
        1. How much capital is necessary?
        1. How many rounds of token sales should there be?

Random
------

### The Colony Token Sale (But More Importantly, Securities Law)

[Article](https://blog.colony.io/the-colony-token-sale-7ac14c845bc0)

- Howey test: determine whether something is an "investment contract":
    1. Investment: anything of value
    1. Common interest: sharing risk and reward
    1. Profit: expected
    - "In searching for the meaning and scope of the word 'security'... form should be disregarded for substance and the emphasis should be on economic reality." -- Howey
- SEC can come after you anywhere in the world, if US investors are affected (ouch)
- If you've satisfied the SEC, you're probably good elsewhere too (but get a lawyer!)
- Bottom line: "going forward, boycott public sales except for those which confer immediate utility within a live and fully decentralised platform."
