September 2016
==============

Tech
----

### Asynchronous Object Initialization

[Article](http://as.ynchrono.us/2014/12/asynchronous-object-initialization.html)

- Avoid creating half-instantiated objects (e.g. part of it is still initializing asynchronously)
- Objects should primarily be about representing state; `__init__` should primarily be about accepting that state and turning it into a complete, internally consistent state
- Use an asychronous factory instead

### Node with Docker - continuous integration and delivery

[Article](http://mherman.org/blog/2015/03/06/node-with-docker-continuous-integration-and-delivery/#.VnmxVpMrLOQ)

- Some docker set up, CI tests, and deployment automation

### License from who

[Article](https://writing.kemitchell.com/2016/05/13/License-from-Who.html)

- Provenance: answers "Who owns this IP"?
- Only owners can license others to copy, change, share, and sublicense
- The "author" of software may not own the IP; e.g. if he was working for someone else
    - Author can't license without owner's permission

### How to get a job in deep learning

[Article](http://blog.deepgram.com/how-to-get-a-job-in-deep-learning/)

- Building and training a large neural network with transformations between the input and output
- **See** for links to other material

### Pylons Unit Testing Guidelines

[Article](http://docs.pylonsproject.org/en/latest/community/testing.html)

- Don't be too clever in your tests! It hides the intent and makes subsequent failure harder to figure out
- Don't try to replace documentation with "doctests"
- Ask:
    - Is the intent of the test clearly explained by the name?
    - Does it follow the canonical form of a test: set up preconditions, call the unit at test once, make assertions about the return, and **DO ABSOLUTELY NOTHING ELSE**?
- Tests should be as simple as possible, run as quickly as possible, and decoupled from others
- Import the module-under-test in each individual test case; import failures then only cause the individual test cases to fail rather than the test cases to not run
- Use helper functions instead of attributes on ``self``

### API Design for Library Authors

[Video](https://www.youtube.com/watch?v=Tedt47e9qsQ)

- Global state (e.g. module state in Python) is precious
    - AVOID MUTATING OR DEPENDING ON IT!
    - If it's convenient, give the user an escape hatch to not use the convenient API if they don't
      want side effects to happen
    - Depend on global state only if it's inherent to the OS / system (e.g. Windows vs Linux)
    - Don't bootstrap your application before `__name__ == '__main__'` is true
- "Push statefulness to a higher level and let the caller worry about it"
    - If you keep doing this, you'll end up with mostly functional code
- You can always add convenience to a library, but you can't take it away
    - Focus on the inconvenient version first
- Don't expose things that are not logically global as imports
    - Design API so that functions receive instances of these objects
- **Convenience != Cleanliness**
    - Clean means maximally convenient and understandable in unexpected cases
    - Design with fewer limiting assumptions!
- Composition should usually be favoured over inheritance
    - Good choice when the problem and interface is well-defined and understood (should **always** be true when writing a library)


### Using Trust in Open Networks

[Article](https://ssbc.github.io/docs/articles/using-trust-in-open-networks.html)

- "Trust-ranking is a key feature of open networks with shared data-structures"
- [Two primary means of managing trust:](http://www.inf.ufsc.br/~gauthier/EGC6006/material/Aula%206/A%20survey%20of%20trust%20in%20computer%20science%20and%20the%20Semantic%20Web.pdf)
    - Policy based: managing and exchanging credentials, access policies
    - Reputation based: past interactions and performance determines future trust
- Policy-based schemes scale poorly, since you have to make a decision on every other agent
- Reputation allows trust decisions to be automated

### Virtualenv Lives

[Article](https://hynek.me/articles/virtualenv-lives/)

- Use virtualenv along with Docker / VMs; Docker / VMs don't replace virtualenv since system-wide
  packages are still installed

### Why Everyone Should Use Attrs

[Article](https://glyph.twistedmatrix.com/2016/08/attrs.html)

- [`attrs`](https://attrs.readthedocs.io/en/stable/) is the Python of the future

### Better Python Object Serialization

[Article](https://hynek.me/articles/serialization/)

- [PEP 443](https://www.python.org/dev/peps/pep-0443/) and `functools.singledispatch` are cool!
    - Allows you to register custom function handlers based on the type of the arguments

### Python Development Anti-Patterns

[Article](https://hynek.me/articles/python-deployment-anti-patterns/)

- "Key infrastructure must not be dictated by third parties."
- Pinpoint your release dependencies with `pip freeze`
- "You have the responsibility to monitor them [security updates] yourself anyway"
- Use [`supervisord`](http://supervisord.org/) to run remote daemons
- Separate app configuration from the actual app (use something like ansible, chef, salt, etc)

### Advancing in the Bash Shell

[Article](http://samrowe.com/wordpress/advancing-in-the-bash-shell/)

- `!!` runs last command
- `!xyz` runs last command matching `xyz`
- `!<N>` runs last command with number `<N>`
- `!<...>:p` prints what would be executed, and adds it to history so you can do `!!` to run it
- `!$` expands to the last argument ("word") of the previous command, `!*` expands to all arguments
- `^<pattern>^<sub>` runs last command with `<pattern>` replaced with `<sub>`
- Some other word modifiers:
    - `:h` (keep dir)
    - `:t` (keep file)
    - `:r` (keep file name)
    - `:e` (keep file extension)
    - `:s` (substitute text)
    - `:g` (global, usually used with others, like `:s`)

### Immutability, MVCC, and Garbage Collection

[Article](http://www.xaprb.com/blog/2013/12/28/immutability-mvcc-and-garbage-collection/)

- "Immutability results in a lot of nice, elegant properties"
- Immutability is costly:
    - Infinitely increasing space
    - Fragmentation (of data), current state of data may be spread out
    - Lots of people may fall into an "tiny worst-case scenario" that's not handled well by desiging for immutability
- Opinion: ACID + MVCC solve some of the immutability issues
    - Use "short-term immutability" along with optimizations for space and IO

### Accountants Don't Use Erasers

[Article](https://blogs.msdn.microsoft.com/pathelland/2007/06/14/accountants-dont-use-erasers/)

- "The database is a cache of a subset of the log"

### A Guide to 256 Colors

[Article](http://lucentbeing.com/writing/archives/a-guide-to-256-color-codes/)

- Terminals are built *serially*; they only have one pass to display text
- Delimiters for terminals are escape characters

### The Power of B-trees

[Article](http://guide.couchdb.org/draft/btree.html)

- "If you weren’t looking closely, CouchDB would appear to be a B-tree manager with an HTTP interface."
- Data is only kept at the leaf nodes, and the height is small enough that the OS can cache the higher level nodes
- Using `_rev`, MVCC, and keeping around old versions of documents, readers could be reading multiple versions of a document at once (based on when they started reading)
- The database file only grows at the end (an append-only B-tree)

### Golang is Trash

[Article](http://dtrace.org/blogs/wesolows/2014/12/29/golang-is-trash/)

### Smart Contracts Make Slow Blockchains

[Article](http://www.multichain.com/blog/2015/11/smart-contracts-slow-blockchains/)

- May not make sense to introduce currency to private blockchains, limiting `gas` implementations and instead just enforcing a hard computational limit
- Smart contracts require global locks, hindering concurrency, as they may change any other contract's state
- Transactions cannot be processed until their order in the blockchain is confirmed
- Thought: possibly use the public blockchain to store code, and then execute it yourself

### Four Genuine Blockchain Use Cases

[Article](http://www.multichain.com/blog/2016/05/four-genuine-blockchain-use-cases/)

- Confidentiality of shared ledgers is a big problem in finance
- "Blockchains represent a trade-off in which disintermediation is gained at the cost of confidentiality."
- Use cases:
    - Lightweight financial systems
        - Remove the centralized control and concerns involved (e.g. security)
        - E.g. crowdfunding, gift cards, etc.
    - Provenance tracking
        - Remove centralized trust
        - Certificate of authenticities
    - Interorganizational record keeping
        - Jointly manage data, without involving intermediaries
        - Audit trails of data, e.g. communication
    - Multiparty aggregation
        - Avoid combining multiple systems of stored data together, or giving it to an intermediary

Life
----

### What's the Most Difficult CEO Skill? Managing Your Own Psychology

[Article](https://techcrunch.com/2011/03/31/what%E2%80%99s-the-most-difficult-ceo-skill-managing-your-own-psychology/)

- "If CEOs were graded on a curve, the mean on the test would be 22 out of a 100. This kind of mean can be psychologically challenging for a straight A student."
- It's **impossible** to not make mistakes managing a large number of people; don't take it personally and too harshly
- Be rational; separate out the importance of issues from your emotions
- "Tip to aspiring entrepreneurs: if you don’t like choosing between horrible and cataclysmic, don’t become CE"
- Techniques to help:
    - Make friends who have gone through or are going through the same
    - Get things on paper, and for second opinions
    - Focus on where you are going rather than what can go bad
    - Don't quit!

### A philosopher’s 350-year-old trick to get people to change their minds is now backed up by psychologists

[Article](http://qz.com/778767/to-tell-someone-theyre-wrong-first-tell-them-how-theyre-right/)

- Tell people how they're right to reframe their mind to what they've missed

### Investing For Geeks

[Article](https://training.kalzumeus.com/newsletters/archive/investing-for-geeks?__s=esaiz3kazigwidftsigk)

- Buy ETFs. The end.

### Age of Em

[Article](http://geoff.greer.fm/2016/07/23/age-of-em/)

- Economic growth bottlenecked by people with long learning curves and diminishing returns
- Brain emulations may be a precursor to AI

### The money in open-source software

[Article](https://techcrunch.com/2016/02/09/the-money-in-open-source-software/)

- Think about a business model from day one
    - Sell enterprise versions, Saas
- Picking a licensing model aligned with monetization stategy
    - Open-source software is always owned by someone
- Don't depend on consulting, but it might be necessary at the start
- Customer satisfaction is more important than sales; ultimately, happy people buy more

### The next big thing will start out looking like a toy

[Article](http://cdixon.org/2010/01/03/the-next-big-thing-will-start-out-looking-like-a-toy/)

- Technology tends to get better at a faster rate than users' needs increase
- Technology adoption is usually non-linear
- Look at external forces to see how a product could be ramped up the utility curve, **not** the designer's feature set

### Come for the tool, stay for the network

[Article](http://cdixon.org/2015/01/31/come-for-the-tool-stay-for-the-network/)

- Build a useful single-player tool, but then get people to stay and create a network by adding a social part

### Machine learning is really good at partially solving just about any problem

[Article](http://cdixon.org/2009/08/20/machine-learning-is-really-good-at-partially-solving-just-about-any-problem/)

- Machine learning can get you 80% of the way to a solution within reasonable amounts of time
- Getting the last 10% to 20% can be very difficult
- Easier to apply machine learning to contexts that are fault tolerant and can have fault tolerant UXs built around them (e.g. human corrections)
- Companies rarely maintain competitive advantage because of their machine learning algorithms; the magic is in the data and how they get it
    - ML algorithms are mostly publically available research done by academics

### The idea maze for AI startups

[Article](http://cdixon.org/2015/02/01/the-ai-startup-idea-maze/)

- Either create fault tolerant UXs on top of the 80% solutions, or find ways to obtain a large amount of data and have that be your advantage
- Public data sets suck
- Narrow your problem set until it's as small as possible while still usable
- Look towards creatively crowdsourcing your data (less capital requirements)

### The computing deployment phase

[Article](http://cdixon.org/2013/02/10/the-computing-deployment-phase/)

- Two phases of technological revolutions: the installation phase, and the deployment phase
- Financial bubbles propel the initial rapid installation (potentially irrational)
- Crash happens, and then recovery phase
- Finally, long period of productive growth as the technology is matured and deployed
- Entrepreneurial activity moves "up the stack" between the two phases; the initial part is focused on building the technology, the second part is on its applications
- Deployment doesn't just mean creating an app; it's a refactoring of an industry into its "optimal structure"
- Entrepreneurs will increasingly have mutli-disciplinary expertise

Random
------

### Zero Knowledge Proofs: An illustrated primer

[Article](https://blog.cryptographyengineering.com/2014/11/27/zero-knowledge-proofs-illustrated-primer/)

- Information leakage: what if you don't trust the other party you're giving information to?
- Prove statements without revealing any information aside from the truth of a statement
- Raise your confidence to the point where the other party can only be lying with a negligible probability
- Use constructs that both hides a digital value, but also binds the maker to it, and then test these constructs to the point of neglibible probabilitY
    - Digital commitment schemes
- Can be used for any NP-C problem

### Surviving a Bad RNG

[Article](https://blog.cryptographyengineering.com/2012/03/09/surviving-bad-rng/)
