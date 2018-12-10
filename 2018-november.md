November 2018
=============

Tech
----

### Trust Minimized Governance Tokens

[Article](http://blog.aragon.one/trust-minimized-governance-tokens/)

- Governance tokens need at least these mechanisms:

  1. Only proposals which align with the stated intent of the organization are executed
    - Traditional stakeholders in organizations are protected by the legal system that enforces an organization's charter and bylaws
    - A way to protect decentralized organizations, whose execution is irreversible, is to prevent malicious intentions from reaching a stage where they could be considered (e.g. a challenge response system for intents)
  2. Ability for participants to safely exit en masse in response to contentious policies
    - Rather than mass selling, allow "rage quitting" individuals a equal share to the pie
      - The organization may be forced to hold fully liquid assets
      - The organization could fund the "rage quitting" by taking on debt and then liquidating its other assets

### How Contract Migration Works

[Article](https://blog.trailofbits.com/2018/10/29/how-contract-migration-works/)

- Rather than use proxies to upgrade, full data migration could be used to _migrate_ a contract
- Really depends on the use case

### Building Ethereum’s public smart contract infrastructure

[Article](https://medium.com/authio/building-ethereums-public-smart-contract-infrastructure-part-2-of-2-74e32f52c9fe)

- Runtime utility: global public good, sometimes acting as a forwarder
  - E.g. account registrar: only allow an action if it's been forwarded through the registar
  - _Public_ aspect can leverage network effects
- Gateway contracts: "frontend" gateway holding runtime utilities
  - Interesting: the gateway would hold both _code_ and _state_; the utilities provide code, and all their state is shared
  - Delegatecalls into the runtime utility, and expects a `revert` to ensure that no state changes happened; the return data is parsed and set


Life
----

### The Premium Mediocre Life of Maya Millennial

[Article](https://www.ribbonfarm.com/2017/08/17/the-premium-mediocre-life-of-maya-millennial/)

- **Premium Mediocre**
  - "Mediocre with just an irrelevant touch of premium, not enough to ruin the delicious essential mediocrity."
  - "Creating an aura of exclusivity without actually excluding anyone."
  - "Dressing for the lifestyle you’re supposed to want, in order to hold on to the lifestyle you can actually afford — for now — while trying to engineer a stroke of luck"
- Social mobility options: illusion of upward potential, anxiety about downwards possibility
- People pay for premium mediocracy for:
  - Reassuring their parents
  - Reassuring / cheerleading their heros


Random
------
