February 2018
=============

Tech
----

### Premises, Promises, and Reality

[Article](http://blog.ycombinator.com/the-decentralized-future-series/)

- Technological breakthroughs: what did they unlock that wasn't previously possible?
- Distributed databases: without an incentive, who would maintain it? Cryptoeconomics to the rescue.

### You Could Have Invented Monads

[Article](http://blog.sigfpe.com/2006/08/you-could-have-invented-monads-and.html)

- Monads: mostly related to solving side effects
    - Bind: mostly for plumbing
    - Set of `(m, unit, bind)` is a monad (where `m` is the "other" dimension of return, e.g. a debug string)

### Placeholder Investment Thesis

[Thesis](https://ipfs.io/ipfs/QmZL4eT1gxnE168Pmw3KyejW6fUfMNzMgeKMgcWJUfYGRj/Placeholder%20Thesis%20Summary.pdf)

- IT cycles: expansion, conslidation, decentralization
- Value creation shifts upwards as old platforms become commoditized and standardized
- Current web distribution incumbents (e.g. Google, FB, Amazon, Apple) are too entrenched and too expensive to overcome
    - Conslidating market; best to invest heavily into them and then progressively invest in new platforms that may grow to commoditize the incumbent business models
- Cryptonetworks: collapses the cost of building and scaling information networks by replacing centralized coordination with universal financial incentives
    - Cryptoeconomic incentives incentivize independent 3rd parties to scale the network (leveraging the community)
        - Diminishing capex of scale
    - ==> Native business model of any network
- **Traditional valuation: price of stock reflects ability to monetize user base, rather than actual network value**
- Key developer-side infrastructure (cryptocommodities) are still under-developed
- Networks don't die like businesses die; decentralized is inherently more robust
- **Cryptoeconomic model is to a network what a business model is to a company**
- Token valuations are more like national currencies: they track the overall activity within a network / economy

### How to Make Bonding Curves for continuous Token Models

[Article](https://hackernoon.com/how-to-make-bonding-curves-for-continuous-token-models-3784653f8b17)

- Bonding curve: defines token price as a function of supply
    - Allows us to have instant liquidity
    - Dynamic inflation rates according to demand
    - Difficulty in computing: every small adjustment of supply will change the price
        - Sounds like a task for integration
    - Child tokens have compounded risk, and are likely to be extremely volatile
- Power functions allow us to define our bonding curve in terms of a reserve ratio:
    - ratio = poolBalance / (currentPrice * tokenSupply)
        - poolBalance is the integral of the pricing function (e.g. 1/3*x^3 if pricing function is x^2)
        - Often simplifies down to a constant value, e.g. 1/3 for quadratic curves


Life
----

### 36 Ways To Hire, Develop, and Retain Great People

[Article](https://medium.com/@barmstrong/35-ways-coinbase-hires-develops-and-retains-great-people-cbfdf93b1c5c)

1. Don't let managers make unilateral decision (Ray Dalio: believability weighted decision making)
1. Give people freedom (Montessori method)
1. Default to open
1. Have an ambitious mission
1. Create internal competition
1. Create "bureaucracy busters" (aka fix what's annoying with your ops / processes)
1. Culture isn't static; keep your values consistent
1. Have a Chief Culture Officer (consistency over constancy)
1. Invest more in hiring than in training
1. Don't rely on inbound applications; seek out superstars
1. When you find someone great, pursue them for years
1. Only hire people who are better than you
1. The CEO should review every hire
1. If you're not a hell yes, you're a no
1. Referrals can be a high quality source of hires: jog people's memories and go through their network
1. Increasing hte referral bonus does not increase the referral rate
1. Pay unfairly for top talent: human performance follows a power law distribution
1. Be more like an all-star team than a family
1. Most people aren't good interviewers
1. Interview based on sample work and structured interview questions
1. Find and develop your best interviewers
1. Have at least two interviewers assess each value or key competency
1. Create a safe space for employees to speak up: encourage revealing pain instead of concealing blame
1. Encourage acting like an owner, rather than an employee
1. People Ops should be transparent on the process and statistics, but private on individual details
1. Constantly A/B test People Ops
1. Remind people about bias, right before the performance review
1. Identify and transition low performers
1. Manager quality is the single best predictor of whether an employee will stay or leave
1. Remind/nudge people frequently about how to be good managers
    - Be a good coach
    - Empower the team and don't micromanage
    - Express interest/concern for team members' success and personal well being
    - Be very productive/results oriented
    - Help the team with career development
    - Have a clear vision/strategy for the team
    - Have important skills that help advise the team
1. Survey employees about how well managers are doing on the above
1. In training, spend more time on practice/repetition, and less on content
1. Have the best employees in each area run trainings
1. Give experiential awards, not monetary awards (non cash rewards trigger emotional responses)
1. Reward thoughtful culture
1. Hire only one-third "traditional HR" people in People Ops

### Netflix Culture Deck

[Article](https://www.slideshare.net/BarbaraGill3/netflix-culture-deck)

- "The **real** company values, as opposed to the nice-sounding values, are shown by who gets rewarded, promoted, or let go"
    - Behavious and skills we value in colleagues
- The best workplaces are those where you have stunning colleagues: direct all your processes towards attracting them
- "Adequate performance gets a generous severance package"
    - If you're not going to fight hard to keep an employee, give them a severance package now
- Don't curtail freedom to avoid errors; relying too much on processes makes you fragile and lose out on talent
    - Find responsible, self-disciplined people to avoid chaos when growing
    - Increase talent density faster than complexity grows!
- Make mistakes, recover rapidly
- Processes:
    - Good: help good people get more done
    - Bad: attempt to prevent recoverable mistakes
    - Avoid rule creep!
- Get outcomes through context, rather than control
    - Inspire through goals, vision, strategy
- Highly aligned, loosely coupled teams
    - Interactions are about strategy and goals, not tactics
- Compensation reviews should be adjusted to their market: "rehire" each year
- Individuals should manage their own career paths, rather than relying on their corporation for planning their careers

Random
------

### Why I am an Austrian Economist

[Take 1](http://bytemaster.github.io/article/2015/01/04/Why-I-am-an-Austrian-Economist/)
[Take 2](http://bytemaster.github.io/article/2015/01/06/Why-I-am-an-Austrian-Economist-Take-2/)

- Using complex math / logic to describe humans is often a mistake: using complicated measures for complex systems is systemically hiding risks / simplifications
    - If you can't follow it, most will assume it's right (pose smart; appeal to authority)
- Principles:
    1. All value is perceived value (wealth is the cumulative perceived value of all parties); subjective value (vs. objective value)
        - Controlled by each individual and can only be changed by that individual
    1. There is no unit of value
    1. An individual can only rank how they value things
    1. You cannot compare value judgements among mulitple people
    1. A price is only valid the instant it happened and only for the parties involved
    1. You cannot perform mathematical operations on prices to draw conclusions
    1. Only voluntary trade can reveal relative value of items
- Heuristic: when you get results that justify violating "do not do unto others what you do not want done to you", there was probably a mistake somewhere
- Challenge: a voluntary trade between two people may result in a loss of value to a third party
    - However, the change in value of property due to 3rd party transactions is controlled by the owner, and only when a transaction is made with the property

### Why I am Not an Austrian Economist

[Article](http://econfaculty.gmu.edu/bcaplan/whyaust.htm)

- Modern neoclassical economics draws from microeconomic blocks:
    - Utility functions
    - Indifference analysis
    - Kaldor-Hicks (cost-benefit)
- Austrian: reject all of these elements
- Utility functions vs. value scales
    - Utility functions model individual preferences
    - Value scales: ordered set of preferences
    - Both are used to approximate utility maximization, either to maximize the function or finding the highest ranked feasible preferences in the set
    - Austrians: scales are better because you can't measure the distance between preferences; utilities are not quantities and cannot be measured / have mathematical operations done to them
    - Neoclassical: utility functions are not meant to be cardinal; they only signal preference; you can only monotonically scale (re-scale however you scaled it)
        - Argues that Austrians got this part wrong: the math does not bound the thereoms to cardinal utility
- Indifference curves
    - Utility of two choices are the same
    - Austrian: however, action demonstrates preference; no preference can exist which cannot be revealed in action
    - Neoclassical: there are more to actions than just the manifestation (what happened and what you can observe)
- Continuity
    - Utility functions, supply and demand curves are continuous
    - Austrian: human beings' perceptions are not continuous
    - Neoclassical: without continuous functions, supply and demand will rarely be equal
- Welfare
    - Austrian: every market transaction benefits all participants, every government intervention benefits some people at the cost of others
        - Changes in social utility from intervention are ambiguous
    - Neoclassical: using utility values allows you to make hard judgments about which choices are more or less efficient than others
- Socialism
    - Austrian: socialism is impossible because it lacks any method of economic calculation
        - However, Austrian economics is all about qualitative judgments rather than quantiative judgments...
        - The economic calculation problem is overstated as an argument against socialism; hardly empirical science backing it up
- Monopoly Theory
    - Neoclassical: free-market structures are "second-best" efficient; there is no feasible real-world way to improve them
- Austrian Business Cycle
    - Widely accepted:
        1. Unemployment increases during downturns; caused by excessive wages and inflation as a unreliable means of reducing wages

### Decentralized Governance in Sovrin

[Article](http://www.windley.com/archives/2018/02/decentralized_governance_in_sovrin.shtml)

- Governance is in everything we do, the question is whether this governance is ad-hoc and implicit or formal and explicit
- Explicit governance is a *protocol*
- Both code and operators are governance questions in blockchains
- "Rules and regulations, laws and contracts, can never replace clarity of shared purpose and clear, deeply held principles about conduct in pursuit of that purpose." -- Dee Hock
    - Can this clarity be encoded into a consitution?
- Argument for permissioned / known set of validator nodes: protecting decentralization and trust-minimization by using a binding constitution (that minimizes ability for parties to force actions from one another / control others)
