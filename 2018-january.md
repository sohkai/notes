January 2018
============

Tech
----

### Confidential Transaction, the Initial Investigation

[Article](https://www.elementsproject.org/elements/confidential-transactions/investigation.html)

- Pseudoanonymity breaks down when transaction amounts are known
- Confidential Transactions: makes the transaction amounts private, while preserving the ability of the public network to verify that the ledger entries still add up
    - Possible due to homomorphic commitments (Pedersen commitment): commitments that can be added (the sum of a set of commitments is the same as a commitment of the sum of the data)

### Ethereum Casper 101

[Article](https://medium.com/@jonchoi/ethereum-casper-101-7a851a4f1eb0)

- Proof of Stake offers:
    - Explicit Economic Security: has flexibility to design explicit penalties for Byzantine behaviour (rather than just energy or hardware costs); cost of damage is a proxy for security
        - Repeated attacks in PoS are much more costly: as if "your ASIC farm burned down" with each round
    - Mitigation of Centralization: mitigates economies of scale that exist in PoW consensus
    - Lower energy costs: substitutes realized costs (non-reversible, e.g. power and depreciation) with potential economic value-at-loss (risk of slashing)
- Issuance costs:
    - Internalized costs: PoW miners pass them on to holders
    - Externalized costs: environmental and governmental costs
    - PoS has much lower issuance costs (and may even reach negative if there are enough tx fees and penalties)
- Casper establishes explicit finality (as opposed to probablistic)
    - Explicit finality enables maintaining network security when sharding is introduced
- Design principles:
    1. Economics to design behaviour
    1. Maximize cost of attack
    1. Public (social) cost-benefit, not just private
    1. Prevent economies of scale
    1. network security is derived from "skin in the game"
    1. Design for oligopolies
    1. Accountable safety (attribute faults to bad actors)
    1. Plausible liveness (avoid "blocks")
    1. Minimal synchronicity assumptions (validators can deliberately go offline)
    1. Decentralized things should be able to regenerate (recoverable from last node standing)
    1. Disincentivize censorship
- Challenges:
    - Nothing-at-stake: during forks, optimal strategy for validators is to validate every chain
    - Long range attack: rewrite the entire chain's history; problematic because PoS isn't secured by time-intensive operations
- Criticisms:
    - Adverse selection: potentially large risk to participate, so participants will likely be ones with more to gain via some advantage or attack
    - Rich get richer: PoS is actually more egalitarian than PoW due to economies of scale in PoS
- 3 Es of Sybil resistence:
    1. Entry Cost
    1. Existence Cost
    1. Exit Penalty

### The History of Casper 4

[Article](https://medium.com/@Vlad_Zamfir/the-history-of-casper-chapter-4-3855638b5f0e)

- **"Blockchain architecture is mechanism design for oligopolistic markets"** -- Vlad Zamfir

### Money, blockchains, and social scalability

[Article](http://unenumerated.blogspot.ca/2017/02/money-blockchains-and-social-scalability.html)

- Social scalability: ability of an institution (relationship or shared endeavor) to overcome shortcomings in human minds in determining who or how many can successfully participate
    - All about human limitations!
    - How does technology constrain or motivate participation in an institution?
    - Extra benefits of new person joining - expected costs and harms to other participants
- Technology: moving function from mind to paper or mind to machine, lowering cognitive costs while increasing the value of information flowing between minds, lowering the cost of discovering new participants
- "Civilization advances by extending the number of important operations which we can perform without thinking about them" -- Alfred North Whitehead
- Trust-minimized: reducing the vulnerability of participants to each other's and to outsiders' and intermediaries' potential for harmful behaviour
- Nothing can completely remove all vulnerabilities: trustless is a misnomer (easy to use though)
- Internet: all about matchmaking, baby
- Markets: removing trust in other's altruism but incentivising them to work on our behalf
    - Pricing: monopolizing collective intelligence for costs and demands
- Blockchains: trust minimization
    - Bitcoin: computationally expensive, but institutionally (socially) cheap
- Scalable markets and prices require scalable money, and scalable money comes from scalable security
- **"Lawyers are costly. Regulation is to the moon."**
- "Typical computers are computational etch-a-sketch, while blockchains are computational amber"
- "Public blockchains are automated, secure, and global, but identity is labor-intensive, insecure, and local."
- We are limited by our minds; we require redesigned institutions that take advantage of social technological advances

### Notes on Blockchain Governance

[Article](http://vitalik.ca/general/2017/12/17/voting.html)

- On chain governance has a number of upsides, e.g. evolves rapidly inside the protocol, not informal and has due process, can impose arbitrary performance requirements for nodes without economic centralization
- Blockchain governance:
    - Decision function: inputs are a bunch of decisions / opinions from people; output is decision
    - Coordination: governance in layers, where bottom-most is truth, but it can be influenced from above (i.e. coordination institutions that create focal points around how and when individuals should act to coordinate)
        - Coordination flags (in coordination games): everyone's watching a signal to do the same things as others; incentivized into mob behaviour because most beneficial (e.g. charging into battle)
- Key questions concerning governance:
    1. What should the bottom layer be, e.g. what is the "truth" layer, and what parameters / levers can we manipulate in it?
    1. What should layer 2, i.e. coordination institutions, be?
- Where should voting occur? Layer 1? Layer 2?
    - Voting has a lot of bribing vulnerabilities, and so to have things committed automatically via threshold voting may be dangerous
- Think about multifactor systems; e.g. using voting and dev team voice as signals

### The Problem with Voting

[Article](https://medium.com/@nayafia/the-problem-with-voting-8cff39f771e8)

- Voting is a competitive game
- What would cooperative governance look like?
    - Work with others to achieve a shared outcome
        - Default mode is failure, so bias is towards action

### Non-Interactive Proofs of Proof of Work

[Paper / Video](https://iohk.io/research/papers/#67CHCNP8)

- Using NiPoPoW / NiPoPoS to prove transactions across chains (to transfer funds across sidechains)
- Gist of PoPoW: only 1/(2^n) blocks will exist in the chain given _n_ and total number of blocks _N_ such that there are 2^_n_ partitions in the blockhashes in _N_
    - If we choose _n_ large enough, there will only be a small amount number of blocks that should exist within N that maintain the property of existing within a certain partition
    - For ~400k blocks, if we choose _n_ = 15, there should only be about 10 blocks with this property

### Mechanism Design Security in Smart Contracts

[Article](https://medium.com/@matthewdif/mechanism-design-security-in-smart-contracts-87f08555b38b)

- Frontrunning
    - Transactions can be front-runned! Any secrets getting exposed in a transaction (e.g. to solve a puzzle) can be detected and mined earlier by someone else (or a miner)
    - Solution: use blind commitments (e.g. ENS: first give hash bids, then later reveal)
- Malicious Wrappers
    - Contracts can be constructed to "wrap" existing contracts, potentially avoiding conditions set out in the original contracts (e.g. lock-in periods for tokens)
    - Solution: case-by-case, but can be difficult. For some use cases, simply ensuring that users are not smart contracts can be enough (done by asking for a signature that can be checked via `ecrecover`: contracts can never own private keys, and hence they cannot create signatures)
        - `EXTCODESIZE` will not work if a call happens from a constructor: be aware (it returns 0)!
