October 2016
============

Tech
----

### A history of branch prediction from 1500000 GC to 1995

[Article](https://danluu.com/branch-prediction/)

- Computer: CPU + memory; instructions live in memory and are fed to the CPU for execution
- Branches: change the address the next instruction comes from
- Pipelined CPU: break the CPU into *m* parts, where one part does the "front mth" part, another the next part, and the finally the *m*th part does the "end" of an instruction
    - More performance from more granularity; you can start the next operation waiting half as long -> *m*x gain in instructions per unit time
    - Branches break this optimization because the CPU can't determine which operation to pipeline next
- Branch prediction: CPU guesses if a branch is taken
    - If it's wrong, it'll throw away intermediate results and start the actual branch fresh - > no worse than we would've otherwise been (in raw performance)
        - Usually high cost for misprediction
    - Strategies for prediction:
        - Predict taken: all branches will be taken (usually because of loops); maybe 70% accurate so much better than no prediction
        - Backwards taken forwards not taken: backwards (goes back to previous code) branches are taken more often than forwards (skips code)
            - Compiler writers may also follow this approach and optimize their results for this
        - One-bit: predict based on last result; store some last taken results as one bit values (e.g. keys as branch addresses)
        - Two-bit: slightly more information than one-bit; can use it as a saturating counter (+1 on taken, -1 on missed)
            - Going further to add more information doesn't really improve much
        - Two-level adaptive, global: store the history of the most recent branches as well as a table of predictions (combine branch history with address as key to table of saturating counters)
            - Keeping global history is cheaper than a table of local histories, and lets us predict correlated branches
        - Two-level adaptive, local: similar to above, but keep separate branch histories for separate branches
        - gshare: similar to above, but hash (e.g. xor) the branch history and branch address instead of concatenating them
        - agree: similar to above, but add a "bias" table where we store one bit for whether or not the prediction matches the bias
            - Decreases "interference" from unrelated branches
        - Hybrid: include both local and global predictors, and build a meta predictor to determine which one should be used
        - Perceptron: simple neural net (actually used by AMD)
- Predicting the branch target is fairly expensive; so much so that early CPUs used a "always predict not taken" strategy to avoid it if they could
- **Main limiting factor on complexity in software is your imagination; if you can imagine something in enough detail, you can write it down**
- Hardware has forces pushing back against complexity: cost, performance (more = slower), reliability

### The TTY demystified

[Article](http://www.linusakesson.net/programming/tty/index.php)

- Abstracting the teletype away from applications (via UART; Universal Asynchronous Receiver and Transmitter) was done for simplicity (UNIX philosphy):
    - OS provides an editing buffer with minimalistic editing commands (e.g. backspace, clear line, etc) and session management
    - Can turn it off by running in "raw" mode; most applications will do this today
- TTY device: combination of UART driver, line discipline instance, and TTY driver
    - Modern systems don't have the UART or physical terminal / teletype; now we use video terminals and keyboards (and their associated drivers)
    - Terminal emulation is usually in userland (xterm), requiring a pty (pseudo terminal)
- Processes:
    - Every pipeline is a job, as they should all be manipulated simultaneously
    - The shell creates a new process gropu every time it launches a pipeline
- Signals:
    - Allows the kernel to communicate asynchronously with a process
    - SIGHUP: sent to an entire session when a hangup condition has been detected; default to terminate
    - SIGINT: sent to the foreground job when the *interactive attention* character (^C) appears; default to terminate
    - SIGQUIT: similar to SIGINT, but for (^\); default to core dump
    - SIGPIPE: sent when a process tries to write to a pipe with no readers; default to terminate
    - SIGCHLD: sent to a parent process when a child process dies or changes state; default to ignore
    - SIGSTOP: unconditionally suspends the program
    - SIGCONT: sent explicitly by the shell when `fg` is used; un-suspend a stopped process
    - SIGTSTP: similar to SIGINT or SIGQUIT, but with (^Z); default to suspend
    - SIGTTIN: sent if a backgrounded process tries to read from a TTY device; default to suspend
    - SIGTTOU: sent if a backgrounded process tries to write to a TTY device; default to suspend
    - SIGWINCH: sent when the terminal size changes to the foreground job; default to ignore (but applications like editors will redraw themselves)
- If processes fill up the kernel buffers of the active pty, their `write` calls will block allowing the pty to handle its buffer

### What happens when (you type google.com into your browser)

[Article](https://github.com/alex/what-happens-when)

- Bunch of stuff about all the machinery, including physical keys, circuits, etc.
- Keyboard inputs work via interrupts as keycode integers once they're received via USB/BT
- Browser first does DNS via browser cache, then OS `gethostbyname()` (which first checks the local `hosts` file before going to DNS)
- DNS uses UDP on port 53 unless the response size is too large (it'll use TCP instead)
- Browsers open connections to a given URL and port via OS `socket()`, requesting a TCP socket stream
- Modem: converts digital signals (1's, 0's) to and from analog signals usable through telephone, cable, etc.
- Fiber: data remains digital
- TLS:
    - Server choses which cipher and compression algorithms to use
    - Public key of certificate from CA (certificate authority) is only used to encrypt the rest of the handshake until a symmetric key is agreed upon
    - All data sent afterwards only uses this symmetric key
- HTTPD (HTTP Daemon) servers handle requests/responses on the server side (usually Apache or nginx)
- Browser page rendering:
    - Calculating the preferred width of each node is done bottom-up by summing the preferred width of child elements
    - Calculating the actual width is done top-down by allocating available widths to children
    - Calculating the height of each node is done bottom-up by applying text-wrapping and summing child node heights
    - GPU rendering is mostly useful because of its massive parallelism for floating point calculations

### What's new in CPUs since the 80s and how does it affect programmers?

[Article](https://danluu.com/new-cpu-features/)

- Processors have sped up a lot faster than memory; solution is generally more caching and prefetching
    - Use predictable memory access patterns and operate on chunks of data smaller than CPU cache
- TLBs: caches for virtual memory lookups
    - Without them, it'd take at least 16 cycles to complete a virtual address lookup each time
    - Super small; usually 64 entries on modern chips
- Out of order execution
    - x86 is usually pretty good about dependencies being executed in the right order (so you can usually ignore out of order execution)
    - Loads can be reordered with earlier stores (prevent with memory fences)
    - No guarantee of maintaining interaction order between multiple cores
        - On not locking" "Doing clever things with memory barriers is almost always a bug waiting to happen" -- Linus
        - Using locks for concurrency primitives is often cheaper than using memory barriers
        - Intel has a `lock` prefix that can be used to make some instructions atomic
    - x86 has pretty strong guarantees, so be careful of porting things to other architectures
- NUMA: non-uniform memory access (memory latencies and bandwidths are different for different processors)
- Context switching
    - Context switching is super expensive because it usually has to flushes the caches
    - People batch syscalls to get away from context switching
    - vDSO: turns some simple syscalls that don't require privilege escalation into user space library calls
    - Use a thread-per-core and not a thread-per-logical-task
- SIMD: lets you operate on 128-bit chunks of data as if they were two 64-bit chunks, four 32-bit cunks, eight 16-bit chunks, etc
    - Common to get 2-4x speed up (although you'll probably have to hand roll your own assembly)
- Power management: the most efficient way is work to race to idle
- GPUs
    - API opened up in the last decade allowing us to do more general things with GPUs (e.g. linear algebra)
    - Core structure is usually super parallel (> 100 floating point units), but each is slower and communication between them is super slow
    - Memory: GDDR is global memory that's accesible by all threads; others are shared (only within a single core) and local (only within a single thread)
    - Threading: SIMT (single instruction multiple thread), so that all threads are following the same instruction
        - If a group of threads need to take a branch, all other threads are suspended until those threads are done
    - IO: PCIe bus increasingly becoming a bottle neck; IO is much slower so it only benefits the user to use the GPU is a large amount of work is going to get done
- Profiling and benchmarking today is super important; performance is a lot less predictable!

### Notes on Google's Site Reliability Engineering Book

[Article](https://danluu.com/google-sre-book/)

- Sysadmins vs SREs:
    - Sysadmins and devs are fundamentally at odds, which causes resistance to change
    - SREs are SWEs that do operations; cap on the amount of "ops" work they do to avoid manual labour trap (automate instead)
        - Responsible for: latency, performance, efficiency, change management, monitoring, emergency response, capacity planning
        - If there's too much work, it gets redirected to the product team
    - Also release engineer, whose sole job is to define how software is released and best practices
- Reliability
    - Diminishing returns: going from 5 9s to 100% is usually a large waste of resources
    - Set an error budget
    - Teams that consistently come under the error budget may be spending too much effort on reliability (if they should be focusing more on "moving fast")
        - Build confidence in your risk models via simulated disasters and testing
- Responses
    - Care about mean time to recovery (MTTR)
    - No human actions = higher availability due to lower MTTR (i.e. humans add latency)
    - Have a "playbook" of responses
- Change management
    - Most outages due to changes on a live system; make this automated and roll out updates progressively
- Forecast expected demand and capacity!
- Risk & reliability
    - If a user is on a device with only 99% reliability, and your service has 99.99%, they won't notice the difference!
    - Measuring: successful requests / total requests
        - Set quarterly goals
- Services
    - If services have clients who want different things (e.g. a data store who has clients who want low latency but some that want throughput), consider partitioning this service and offer different kings
    - If a service becomes so reliable people don't plan it ever going down, simulate outages to get them to handle it (if their reliability is a concern)
    - Metrics to care about:
        - User-facing: availability, latency, durability
        - Storage: latency, availability, durability
        - Big data: throughput, end-to-end latency
        - Correctness!
    - Aggregating metrics: use distributions, not averages; most people care more about tail latencies than better average
    - Metric targets:
        - Don't base off of current numbers; they may be unsustainable
        - KISS
        - Minimize number of targets
        - Perfection can wait; they can always be made better
        - Don't overachieve; there's probably better things to do instead
- Toil
    - If a human operator has to touch a system during normal operations, it's a bug
        - Manual, repetitive, automatable, no enduring value, O(n) with service growth type actions
    - Some toil can be good; predictable and repetitive tasks can be calming and give a sense of accomplishment
- Monitoring
    - Non-trivial; usually 10-20% of manpower devoted to monitoring
    - Trend towards simpler/faster systems, with better tools for post analysis
    - Avoid "magic" systems
    - Use simple alerts that represent clear failures
    - Mostly white-box monitoring
    - **Golden signals:**
        - Latency
        - Traffic
        - Errors
        - Saturation
    - Taking controlled hits in short-term reliability is usually the better trade (against spending effort for long-term reliability)
- Automation
    - **"Automation is a force multiplier, not a panacea"**
        - Consistency
        - Extensibility
        - MTTR
        - Faster non-repair actions
- Releases
    - Hermetic builds
        - Same rev number should always build to same result
        - Self-contained
    - Include config files and binaries in same package; simple but tightly couples binary and config (usually ok for most projects)
- Simplicity
    - Stability vs agility
        - Freezing things is a way to make thing stable—balance between speed and stability
        - Reliability can increase agility
    - Virtue of boring!
    - Ship only essential complexity, and push back against accidental complexity
        - **Essential complexity is caused by the problem to be solved, and nothing can remove it**
    - All code is a liability; remove bloat and etc
    - Smaller is easier to test and more reliable
    - Smaller releases makes it easier to track down issues
- Emergency responses
    - Test-induced emergencies are useful for flushing "hidden" dependencies, if teams report that they're unable to access resources
    - Changes can induce emergencies, e.g. bad config pushes
- Tracking outages
    - Systems should automatically escalate or notify other people if the immediately notified don't send ACKs
- Load balancing
    - Round robin
        - Usually 2x difference between most loaded and least loaded; most expensive request can be 1000x more expensive than cheapest request
    - Least-loaded round robin
        - Similar to normal round robin in practice, but may be better for some workloads
        - Depends on how you define "least-loaded"; could be number of connections per client
    - Weighted round robin
        - Much better, assume you have the right inputs and right weighting
- Handling overload
    - Typical strategy: serve degraded responses
    - Modeling capacity: better to measure directly available resources, rather than queries-per-second or based on requests
    - CPU utilization is usually good signal for provisioning requirements
    - Use client-side throttling, but be careful if most of the resources are being spent on rejecting requests
- Preventing overload
    - Load test with a realistic environment
    - Serve degraded results
    - Fail cheaply and early when overloaded
    - Fail at earlier systems (e.g. reverse proxy, load balancer, etc
    - Use request deadlines and throw away requests past their deadlines; each stage should check that the deadline hasn't been passed
- Data integrity defense
    - Allow "soft" deletions, but know that there will be accidents / mishaps
    - Keep backups in case of these accidents / mishaps, and try to keep them for as long as possible (corruption can go unnoticed for months)
    - Use sanity checks for early detection

### The Elephant was a Trojan Horse: On the Death of Map-Reduce at Google

[Article](http://the-paper-trail.org/blog/the-elephant-was-a-trojan-horse-on-the-death-of-map-reduce-at-google/)

- Generalized dataflow engines can implement map-reduce as a special case
- Computing systems can and should be built from relatively cheap, shared-nothing machines
    - Storage and compute become incrementally scalable
    - It's easier to build robust, fault-tolerant systems from unreliable components (really?)
- Map-reduce has fairly rigid, in its two-phase topology, and is hard to program for

### FLP Impossibility

[Article](http://the-paper-trail.org/blog/a-brief-tour-of-flp-impossibility/)

- Failure detection of nodes is impossible in asynchronous settings: there are no bounds on the amount of time a processor might take to complete its work and respond
    - Impossible to tell whether a processor has crashed or is just taking a really long time to respond
- **In an asynchronous setting, where only one processor might crash, there is no distributed algorithm that solves the consensus problem**
- Consensus properties:
    - Termination: all non-faulty processes eventually decide on a value
    - Agreement: all processes that decide do so on the same value
    - Validity: the value that has been decided must have been proposed by some process
- Asynchronous system model:
    - No upper bound on the amount of time an individual processor can take to receive, processor, and respond to an incoming message
    - Reliable communication links
        - Well known that there's no solution for consensus if a system uses arbitrarily unreliable communication links
        - TCP is reliable enough
- *Bivalent*: configurations that may lead to either decision value

### Numerai's Master Plan

[Article](https://medium.com/numerai/numerais-master-plan-1a00f133dba9)

1. Monopolize intelligence
    - NMR grows community and improves quality of intelligence via incentive alignment
    - Get all the data scientists in the world working together as part of a single entity rather than in siloed orgs
1. Monopolize data
1. Monopolize money
1. Decentralize the monopoly

- Shift the product from being for people, but rather an API for AIs
    - Goal: an API that any artificial intelligence could use to control capital in the economy
    - Adding compute: rather than "pushing" for predictions from connected AIs, if access to computational power is made super cheap, Numerai could "pull" just-in-time for predictions

### Dfinity Crypto

[Presentation](https://dfinity.org/pdf-viewer/pdfs/viewer.html?file=../library/intro-dfinity-crypto.pdf)

- Threshold relay: produce randomness that is incorruptible, unmanipuable, and unpredictable
- Unique, deterministic threshold signatures:
    - Only one correct signature for any public key, even for group thresholds
        - A threshold public key can only produce a single valid output signature for a given message
    - A signature can be validated by anyone who has the public key and seed data
    - The signature is a deterministically produced random number, and all verifiers reach immediate consensus over it without requiring a consensus protocol
    - An example in real life: Boneh-Lynn-Shacham signatures (BLS)
- Decentralized verifiable random function (dVRF): relay between groups to create a random sequence
    - Let's say we have independent nodes (with their own pub/priv key), who each belong to a single threshold group (with its own pub/priv key)
    - At each step there is a "current" group, who takes the previous group's signature and signs it, producing a random number
    - **This random number is used to select the next current group**
        - Deterministic, verifiable, unmanipulable, and infinite
- Death by poisson process (Ethereum)
    - A lot of blocks are empty, because miners prefer to build empty blocks (no validation, higher chance of being confirmed = more profit)

### Alan Kay on Lisp

[Answer](https://www.quora.com/What-did-Alan-Kay-mean-by-Lisp-is-the-greatest-single-programming-language-ever-designed/answer/Alan-Kay-11?share=1)

- Evolution: find fits to an environment; if your knowledge or understanding is lacking, then what you select will also be lacking
- **"Point of view is worth 80 IQ points"**
    - We make progress by making the things we can pay attention to (cognitive load) more powerful
    - "A fun thing about [Lisp] is that once you’ve grokked it, you can think right away of better programming languages than Lisp"
- Scientists: experience phenomena => devise models to negotiate relationships with the phenomena

### Write tests. Not too many. Mostly integration.

[Article](https://blog.kentcdodds.com/write-tests-not-too-many-mostly-integration-5e8c7fff591c)

- Diminishing returns on tests as coverage increases
    - You also start to test implementation details, rather than interfaces
        - **Aim to rarely change tests when you refactor**
- Integration tests are a balance on trade-offs between confidence and speed
- How to write integration tests:
    - Avoid mocking as much as possible

### Diminishing returns of static typing

[Article](https://blog.merovius.de/2017/09/12/diminishing-returns-of-static-typing.html)

- Benefit of static typing: increases proportion of bug-free lines of code deployed to production, and catches type errors earlier
- Cost of static typing: upfront investment, compile times, steeper learning curve, cryptic error messages
- **Important metric: velocity—speed at which we can deploy bug-free code**
    - Product of benefit and cost graphs; results in a maximum sweet spot for usage of static typing
    - Note that different people have different views on the cost and benefit graphs, resulting in different velocity sweet spots
    - Also business needs can dictate which is more important: speed vs reliability

### YC's Essential Startup Advice

[Article](https://blog.ycombinator.com/ycs-essential-startup-advice/)

- Launch product right away
- Do things that don't scale, and only scale if it's necessary
- Look for pareto efficiencies; find the 10% work solution
- Most important: write code and talk to users
- Take the ambitious path
- You choose your customers, and you can fire them too; pick the ones who come running to you
- Do less, really well
- **"Success is not determined by whether you are broken at the beginning, but rather what the founders do about the inevitable problems. Your job as a founder will often seem to be continuously righting a capsized ship. This is normal."**

### Estimating a front end web dev job

[Article](http://hanserino.github.io/2016/02/11/estimating-a-front-end-web-dev-job/)

- Avoid having non-doers set deadlines
- **User centered process:**
    1. Identify current problems and bottlenecks
    1. Define user needs (user stories)
        - "As a ____, I woiuld like _____, so that I can _____"
        - Rate them from crucial to nice-to-have, to set priorities
    1. Design to met user needs
    1. Prototype
    1. Implement
        - Estimate by breaking down user stories
    1. (And obviously, iterate 3-5)
- As a developer, if you don't get user stories handed down to you from the designers, you should fake them (and iterate with the design team on this)
- To make sure you and the client are on the same page:
    - Summarize understanding of problem
    - Summarize product concept
    - List of user stories based on problem
    - List of tasks based on stories
    - Estimate, including the task, delivery, hours, and cost
- Let the client help you to estimate and check the costs; this lets them collaborate with you and change anything in case they want to re-prioritize

### How the Catalan government uses IPFS to sidestep Spain's legal block

[Article](http://la3.org/~kilburn/blog/catalan-government-bypass-ipfs/)

- Using an international TLD (.io) makes it hard for Spain to mandate a redirection of a domain to its own servers (unlike .cat)
- P2P distributed makes it impossible for any actor to block access to the content, as it's replicated and distributed around the network in ways that are hard to identify and block at an ISP level

### Logging v. instrumentation

[Article](https://peter.bourgon.org/blog/2016/02/07/logging-v-instrumentation.html)

- Logs:
    - Services should only log actionable information
        - Serious, panic-level errors requiring human intervention (should be sparse; ideally silent if nothing's wrong)
        - Structured data consumable by machines (versioned schema)
    - Keep it simple: don't need too much configuration, only log what needs to be seen
    - Treat like event streams; apps should just stream to stdout and let other services pick it up
    - Very expensive in engineering time and resources
- Instrumentation:
    - Includes everything else diagnostic
        - E.g. everything you've left out of logging
    - Instrument every meaningful number available for capture
    - **RED: request rate (count), error rate (count), duration of requests**
    - **USE: utilization, saturation, and error count** of all resources
        - Utilization: average time the resource was busy
        - Saturation: degree the resource can't handle additional work
    - Libraries should include at least:
        - Counter, for events that happen (e.g. incoming requests)
        - Gauge, for events that fluctuate over time (e.g. size of threadpool)
        - Histogram, observations of scalar quantities (e.g. request durations)
- Tools to achieve system observability, also includes distributed tracing systems

### Introduction to Boosted Trees

[Article](http://xgboost.readthedocs.io/en/latest/model.html)

- Gradient boosting used for supervised learning problems (start with training data of multiple features to predict target variable)
- Objective function: measure the performance of the model (against known performance) given a set of parameters
    - Always contains two parts:
        - Training loss: how predictive the model is on training data (typical: mean squared error)
        - Regularization: controls complexity of the model, to avoid overfitting
        - Training and regularization gives us a model that's **both simple and predictive**
            - Tradeoff between the two is known as bias-variance tradeoff
- Tree ensemble model: set of classification and regression trees (CART)
    - Similar to decision trees, but with leaf nodes containing prediction scores rather than decision values
    - Ensemble: sums the prediction of multiple trees together
        - Trees try to *complement* each other
    - Models for random forests are the same as tree ensembles; the difference is in how you train them
- Training
    - Additive strategy: fix what you've learned, and then add one new tree at a time
        - Add the tree that optimizes your objective at each step
    - Optimize one level of a tree at a time (via pruning techniques)

### Intuitions in Machine Learning: Bias and overfitting

[Article](https://mycardboarddreams.wordpress.com/2017/06/19/intuitions-in-machine-learning-bias-and-overfitting/)

- Bias: ignored connections you shouldn't have ignored
    - Use more granular, nuanced views rather than large, sweeping conclusions
- Overfitting: concluded connections where none existed
    - Too optimistic with small sample; only gradually increase confidence in conclusion
- Balance is the most important thing!

### Intuitions in Machine Learning: Understanding ROC Curves

[Article](https://mycardboarddreams.wordpress.com/2017/04/17/machine-learning-101-understanding-roc-curves/)

- ROC: Receiver Operating Characteristic
    - Let you know if the features you're using to make decisions are good ones
- Classify decisions as true positives, false positives (type 1 error), false negatives (type 2 error), and true negatives
    - True positives: win!
    - False positives: disappointment
    - False negatives: regret
    - True negative: apathy
- Sensitivity: true positives divided by the condition positives => all the true positives you've predicted against all true positives
- Specificity: true negatives divided by the condition negatives => all the true negatives you've predicted against all true negatives
- Fallout: false positives you've predicted divided by all true negatives
    - Complement of specificity
- Miss-rate: complement of sensitivity
- Design a feature / decision criteria, and find a threshold to use to predict positives
    - Threshold is personal preference; do you care more about lowering specificity or getting more positives (increasing sensitivity)
    - Goal: increase sensitivity faster than fallout
        - Maximize the area under the curve; **let the machine run through potential features and optimize for this to "learn"**

### CSP and transducers in Javascript

[Article](https://tgvashworth.com/2014/08/31/csp-and-transducers.html)

- CSP: formalized way to describe communication in concurrent systems
- Transducers: (transform + reduce) "powerful and composable way to build algorithmic transformations"
    - Generic and composable way to operate on a collection of values
- Many array operations can be generalized to `.reduce()` (e.g. `.map()`, `.filter()`), and this generalized form allows us to build generalized versions of those operations (e.g. a generic `map()` that takes a "transform" and applies to it to a "collection")
    - "Algorithmic transformations" == `map()`, `filter()`, etc
    - Naive ways of composing these transformations together doesn't let us have these characteristics:
        - Parallelisation
        - Lazy execution
        - Decouple operations from input and output data structures
    - Key observation: we can use any reducing function in any other reducing function (not just `concat()` to make new result arrays)
        - Tranducers: a layer of abstraction on top of our generic transforms to allow them to use any reducing behaviour
            - Users of the transducer are responsible for combining the given input and result (e.g. `concat()`)

### A very casual introduction to Fully Homomorphic Encryption

[Article](https://blog.cryptographyengineering.com/2012/01/02/very-casual-introduction-to-fully/)

- Problem: it's kind of hard to use something when it's in encrypted form
    - Homomorphic encryption: you can perform useful operations on encrypted values without having to decrypt them first
        - Useful operations: mathematical operations on polynomials
        - Even better operations: any arbitrary operation—"cryptocomputing"
- Once you get doublly homomorphic algorithms that support both addition and multiplication, you can make a NAND gate (which allows you derive all the rest of the boolean logic gates and implement circuits)
    - But this computing model is pretty shitty, so we might only implement specialized computations rather than fully generic computation

### What is the Random Oracle Model and why should you care?

[Article 1](https://blog.cryptographyengineering.com/2011/09/29/what-is-random-oracle-model-and-why-3/)
[Article 2](https://blog.cryptographyengineering.com/2011/10/08/what-is-random-oracle-model-and-why-2/)
[Article 3](https://blog.cryptographyengineering.com/2011/10/20/what-is-random-oracle-model-and-why_20/)
[Article 4](https://blog.cryptographyengineering.com/2011/11/02/what-is-random-oracle-model-and-why/)

- Ideal hash function: behaves like a *random function*
    - Given an input, the output is completely random (but still deterministic; i.e. giant lookup table with random outputs)
    - Random functions are impractical (we can't build or use them in real life), but we can use them to prove security models that can't be proven in other ways
        - Note though, we eventually have to substitute a real hash function so this proof ends up technically meaningless, but lots of really important schemes are proved this way
- Confusion: each bit of the ciphertext should depend on several parts of the key (obscures connections between the two)
- Diffusion: if we change a single bit of the plaintext, then (statistically) half of the bits in the ciphertext should change, and vice-versa
- Random Oracle Proof: hashing is only done by a party called the "oracle"
    - Lazy random function generation: start empty and only add hash outputs as inputs come in
- XORing a message with a secret, perfectly random string is an effective way to encrypt something (a one time pad)
- When we say that an encryption scheme is "provably secure", it's usually only under some assumption (e.g. "hard" to do something)
- How reduction proofs work:
    1. Assume problem X is hard
    1. Show that if there exists an efficient algorithm that breaks our scheme, then there exists an efficienct algorithm that solves problem X
        - Write an algorithm to solve X, but have it require a blackbox subroutine that's identical to an algorithm that breaks the encryption scheme
            - Blackbox, because it should work with any possible algorithm that breaks the scheme
        - Random oracle model isn't a blackbox, because the adversary leaks information about what it wants hashed
            - We can tell what it's thinking internally, and possibly even change its operation by manipulating responses
    1. But if we had such an efficent algorithm, then problem X can't be hard

### Reactive Manifesto

[Article](https://www.reactivemanifesto.org/)

- Reactive Systems:
    - Responsive
        - Responds in a rapid and consistent manner, with reliable upper bounds
    - Resilient
        - Stays responsive in the face of failure, via replication, containment, isolation, and delegation
    - Elastic
        - Stays responsive under varying workload, via sharding or replication
    - Message Driven
        - Establish a boundary between components to ensure loose coupling, isolation, and location transparency

### Layers of the Internet Economy

[Article](https://staltz.com/layers-of-the-internet-economy.html)

- **Products** provide necessary capabilities: energy, computers, storage, connectivity
- The **Grid** provides remote products as a service (e.g. energy grid, internet connectivity)
- The **Cloud** Infrastructure as a Service -> Platform as a Service -> Software as a Service; only utilizes grid resources via software
- **Big Data** Data as a resource, AI as a Service via surveillance capitalism
    - *Software feedstock*
- **Off Grid** is a lifestyle based only on the product layer
    - Become self-sufficient in all four capabilities
    - Connectivity and Energy are still mostly centralized to a high degree

### State Channels

[Article](http://www.jeffcoleman.ca/state-channels/)

- State channels: interactions which *could* occur, but usually gets conducted *off* a blockchain
    - Payment channels are a specialized version where the only state held is financial balances
- Components:
    1. Part of the state is locked into the channel, and can only be updated via multisigs
        - Nuance: you probably want to delegate to a party who is always online, in case you accidentally lose network connection and the other party tries to screw you
    1. Participants independently talk to each other to update the state, signing incrementally updating transactions off-chain (but who *could* be submitted to the blockchain)
        - Nuance: need to give a chance for either party to update any provided state from the other party, "trumping" their "old" update with a newer one (simplest is a timer)
            - Note that this mechanism will usually not be used, if designed correctly, because it incurs more costs than mutual agreement
    1. Participants submit the end state back, mutually agreeing on the final state and closing the channel

### Privacy on the Blockchain

[Article](https://blog.ethereum.org/2016/01/15/privacy-on-the-blockchain/)

- Holy grail: converting arbitrary applications into fully privacy-preserving applications
    - Most promising: cryptographically secure obfuscation (but absolutely perfect obfuscation has been proven to be impossible)
        - Indistinguishability obfuscation: given two equivalent programs, one cannot determine which outputs came from which program
        - But this is way too expensive
    - Secure multi-party computation: split a program and its state amongst multiple parties such that you need a subset of them to execute computations or reveal any state
        - Relies on trust on the participants (who may save revealed state for later, etc)
    - Zero knowledge proofs
- Low-tech approaches
    - One-time accounts: every transaction must completely empty one or more accounts and create one or more accounts
        - Users' funds are not linked to each other by default, but they can still be linked when you have to combine separate transactions together
    - Auditable computation: participants send funds to a contract that has the hash of the code; when the time comes to submit a result, if you don't agree with the other party, you can send the actual code to have that be executed
        - A version of receipts provided in state channels
    - Ring signatures: proves that the signer has a private key corresponding to one of a specific set of public keys, without revealing which one
        - Creation of the signature requires usage of a private key to "close the loop" in the signature chain; it's easy to verify correctly created signatures but impossible to tell which "link" used a private key
    - Encryption: just encrypt basic documents, can use a deterministic wallet to control access for certain documents
    - Secret sharing: encrypt via multisig where multiple parties have to cooperate to decrypt the data

### Crypto Evolution

[Article](http://blog.ycombinator.com/crypto-evolution/)

- "Forks clone the original DNA, i.e programming code, of the currency and then modify it to adapt it better to the demands of the market/community."
    - Preserves original ownership, idea, and beliefs
- Forks allow a network to try out many different futures at the same time (**think: A/B testing!**)
    - Natural process for evolution?
    - Many of the individuals (forks / alternative tokens) will perish, but the resulting species as a whole will evolve to be anti-fragile
        - **"Recall that the fragile wants tranquility, the antifragile grows from disorder, and the robust doesn’t care too much."** -- Nassim Taleb
        - Volatility and stress both signal stability

### A Crash Course in Cryptoeconomics

[Article](https://medium.com/blockchannel/a-crash-course-in-mechanism-design-for-cryptoeconomic-applications-a9f06ab6a976)

- Cryptoeconomics: combination of cryptography and economic incentives to design robust decentralized protocols and applications
    - Similar to mechanism design: incentivization of rational actors to behave in socially desirable ways
- Blockchains increase the range of problems that can be incentivized
- Mechanism design:
    - Inverse game theory; we start by defining desirable outcomes and work backwards to create a game that incentivizes players towards those outcomes
    - Players:
        - Possess private information (types), which may fall under a common prior (probability distribution over types)
        - Individual utility: function of reported type (may be a lie), actual type, and output of decision rule
    - Social decisions: set of potential decisions
    - Decision rule: mapping of types to social decisions
    - Transfer functions: using transferrable goods to incentivize players
    - Social choice function: maps reported types to separate monetary and non-monetary components
    - **Mechanism**: (message/strategy spaces, function mapping messages/strategies to resulting decisions and transfers)
        - "Implements" social choice functions, if the mechanism produces the same mapping as a social choice function
    - **Revelation Principle**: Any social choice function implementable by an arbitrary mechanism can also be implemented by a truthful, direct-revelation ("no lies") mechanism
    - Constraints for optimization (note that many are impossible to satisfy simultaneously):
        - Incentive compatibility: every agent achieves best outcome by acting true to their preferences
        - Individual rationality: no agent loses by participating in the mechanism
        - Efficiency: sum of individual utilities are maximized
        - Budget balance: transfers net to zero
        - Weak budget balance: transfers less than it receives
    - **Specifying user utilities and objectives is super hard**
- Cooperative game theory
    - "Blockchain architecture is mechanism design for oligopolistic markets" -- Vlad Zamfir
    - Analyze what types of coalitions can be created, the payouts associated with each (characteristic function), and how to divide payouts to participants
    - Shapley Value: payoff such that each member receives their marginal contribution to the coalition
- Challenges with cryptoeconomics:
    - Mechanism design often relies on a trusted intermediary to ensure correctness and privacy, but a blockchain can only guarantee correctness
    - Decentralized mechanisms will require algorithmic agents to "run" the mechanism and reason about how to maximize objective functions

### Best Practices for Flow Typing React Components

[Article](https://building.coursera.org/blog/2017/06/01/best-practices-for-flow-typing-react-components/)

- Prefer `React.Component<DefaultProps, Props, State>` over `props: Props; state: State; defaultProps: DefaultProps;` in the body
    - Use `void` if `DefaultProps` or `State` aren't used
- Don't use `*` in place of `DefaultProps`
- Use `React$Component<DefaultProps, Props, State>` for function parameter types
- Use `Element` for refs
- Input of an HOC: `Class<React$Component<DefaultProps, Props, State>>`
- You have to explicitly type exports; follow the pattern of typing the exported variable and then exporting that variable separately
- Writing a HOC: it might be easier to use `.js.flow` files next to the `.js`, because the types can get pretty big

### Creating accessible React apps

[Article](http://simplyaccessible.com/article/react-a11y/)

- Dynamically set the page title if it should change, since this is the first thing screen readers will announce
    - Set `document.title` in `componentWillMount()`
- Focus is really hard (e.g. you might want to focus on your loading message so the screen reader can announce it!)
    - Be careful to focus on an element on the current page if you've come from a React Router `<Link>` transition (otherwise, focus will be lost on the old page)
- Aria live messages: use `aria-live` and `aria-atomic` on a hidden element to annouce something to the user

### The Most Important Rule in UX Design that Everyone Breaks

[Article](https://blog.prototypr.io/the-most-important-rule-in-ux-design-that-everyone-breaks-1c1cb188931)

- Miller's Law: humans can only hold ~7 bits of information at a time in their head
    - *Chunking*: assembling multiple pieces into a cohesive whole
- **Always organize elements of information in categories no larger than 9, but preferrably ~5**
    - Avoid the temptation to add more to the interface!

### Dynamic import() (TC39 proposal)

[Article](https://developers.google.com/web/updates/2017/11/dynamic-import)

- Dynamic `import()` allows you to:
    - Import a module on-demand
    - Compute the module specifier at runtime
    - Import a module from a non-module script

Life
----

### How I got to 200 productive hours a month

[Article](https://qotoqot.com/blog/improving-focus/)

- Tiers (in this order):
    1. Environment
        - Set safeguards in advance to overcome low points in willpower, motivation, and self-awareness
        - Increase the friction to slip into distracting activities
        - Use another device for leisure in another room; **people anchor different types of behaviour to different locations with conditioning**
        - Planning:
            - Split into small tasks, so everything looks achievable and daily progress is possible
            - Leave boring tasks for the evening when you're tired
            - Adjust task order before sleep, so you have a clear plan in the morning
    1. Body
        - Crunch is an emergency effort to compensate for lack of real productivity
        - Discipline is more sustainable than motivation
        - 3-5 min break every hour that's away from work
    1. Mind
        - Watch your mind, and adapt your workflow to suit your mental state
            - Have music playlists prepared for your mood waves
        - **You are not your thoughts, and they have no power over you until you feed them with attention**
        - Find something worth doing, and results in helping the world
            - Escape procrastination by shifting focus to long-term goals

### How to win friends and influence repos

[Article](https://robertheaton.com/2014/07/21/how-to-win-friends-and-influence-repos/)

- Time for a feature to go from idea to deployment may be much important than aggregate throughput and capacity

### Three Paths in the Tech Industry: Founder, Executive, or Employee

[Article](https://blog.ycombinator.com/three-paths-in-the-tech-industry-founder-executive-or-employee/)

- Founder:
    - Prerequisites:
        - Identify potential teammates
        - Figure out financial plan
        - Identify a problem your team is passionate about solving
        - Having an idea of how to solve the problem
    - Don't hustle around a missing prerequisite instead of solving the root issue, e.g. make friends with devs who you can convince to join you rather than outsourcing
    - **Experience is over-valued**
        - You'll learn most of what you need to know about your problem, customer, and solution after starting
- Executive
    - Strategies:
        - Find a company that's growing rapidly (hard to do)
        - Work for more established companies, looking for opportunities to work their way up diagonally across multiple companies
- Employee
    - Similar to executive
    - Easier to optimize as a software engineer
- **It takes a lot of time to truly get good at something**; understand the costs of exploration

### City Walls & Bo-Taoshi: Exploring the Power of Token-Curated Registries

[Article](https://medium.com/@simondlr/city-walls-bo-taoshi-exploring-the-power-of-token-curated-registries-588f208c17d5)

- Token curated registries:
    - Provide identity and sourcing mechanisms for consumers of the registry
        - Lower transaction costs (sourcing, verifying, etc) for both consumers and candidates
    - Decouples incentive structures so that token holders have only the goal of making the registry better
    - Decentralized list making, opened up to market forces
- "The core, incentivized game being played through the token-curated registry system is to include reputable actors and exclude non-reputable actors."
    - Challengers receive more if their challenge on an application is voted in the majority
    - Any party in the registry can be challenged at any point in time
- Churn when the registry gets large (diminishing value for curators to do work) will inevitably happen
    - Curation markets may be useful, as they're on a continuous (rather than binary in/out) spectrum
    - Prediction markets for whether a candidate will remain in the registry might provide more signals and incentives
    - Split registries into sub-registries when they're too big

### Eustress, Complexity, Social Systems Design & Blockchain Tokenization

[Article](https://medium.com/@simondlr/eustress-complexity-social-systems-design-blockchain-tokenization-5c3e264dc258)

- "A system generally responds favourably to specific stressors up to a certain point (depending on its design), after which the stressors negatively affects it."
- Coordination often increases with cost, up to a point
- What is the optimal stress level we need to rapidly roll out opt-in coordination around shared goals

### Curation Markets

[Article](https://medium.com/@simondlr/introducing-curation-markets-trade-popularity-of-memes-information-with-code-70bf6fed9881)

- Curation market: pairing topics/memes/ideas/goals with a token of value to curate information inside it
    - Coordination around shared goals
    - Components:
        - Continuously minable token, based on set price
        - Price increases as more tokens are circulated (???)
        - Amount paid for the tokens are kept in a deposit
        - Tokens can be burned to withdraw deposit
        - Curators bond tokens back their opinions in curating information

Random
------

### Cryptoasset Valuations

[Article](https://medium.com/@cburniske/cryptoasset-valuations-ac83479ffca7)
[Model](https://docs.google.com/spreadsheets/d/1ng4vv3TUE0DoB12diyc8nRfZuAN13k3aRR30gmuKM2Y/edit#gid=1912132017)

- TAM: total addressable market
- Cryptocurrencies are "currencies"; not companies! They don't have future cash flows (usually)!
    - Use a format similar to a DCF, but use the equation of exchange instead of revenues, margins, and profits
    - Cryptoassets serve as a currency in the protocol economy that it supports
- Equation of exchange:
    - M = size of asset base
    - V = velocity of asset (times traded per period for the "same" coin; e.g. 1.5 would be a coin trading hands 1.5 times in that period)
    - P = price of provisioned resource
    - Q = quantity of provisioned resource
    - Provisioned resource: actual useful good provided by the network, e.g. file storage (Filecoin: P is $/GB, Q is GB; PQ = $)
        - Represents the exchange of value in the economy for provisioning the resource
- GDP of a crytoeconomy: the on-chain exchange of value over a period of time (transaction volume)
    - Slightly lower due to speculation volume, e.g. FX trading
- Valuation: largely solving for M, where M = PQ / V
    - What are the levers of value within a cryptoeconomy?
    - Should bonders (PoS / state channels) and hodlers be accounted in the supply of the cryptoasset?
    - Money supply can be increased through vesting and foundation releases
    - P will usually be associated with a deflationary nature (e.g. cost of storage usually goes down)
    - Q is based on adoption of the provisioned resource, compared to TAM (use an S curve?)
    - V: Bitcoin's velocity can be assumed to be 14 if we roughly discard complete hodlers
    - **Price of a coin should be based on its future expected utility**, not just its current utility
        - Simple analysis: discount a single future utility value to the present
            - Note that the discounting is not accumulative, since you exchange and use cryptoassets rather than accumulate them
            - Pick a super huge discount rate and use a holding period (e.g. 10 years)
                - Current asset price = Future utility / (1 + discount rate) ^ holding period
                - Note that this discount rate is what you believe to be your expected ROI
                    - Basically, this discount rate is what you expect to get returned for taking on the risk of holding the asset for that period of time
        - Additional factors: n-order valuation, where your future utility is based on its future utilities (e.g. 10 year utility is based on the 20 year utility, etc)
            - This will eventually max out to just be maximum utility, given by the maximum saturation rate (where there is no more potential for future growth)
        - Current utility can be a good measure to check assumptions and track progress

### What is Money?

[Article](http://www.imf.org/external/pubs/ft/fandd/2012/09/basics.htm)

- Money is anything that can serve as a:
    - Store of value: you can save it as use it later
    - Unit of account: provides a common base for prices
    - Medium of exchange: something people use to buy and sell from one another
- Indirectly: holds value over time, can be easily translated into prices, and is widely accepted

### Extraordinary UX: What's the line between a well-designed user experience and an extraordinary one?

[Article](https://medium.com/@austincoleschafer/extraordinary-ux-whats-the-line-between-a-well-designed-user-experience-and-an-extraordinary-one-f0a472c85968?ref=hackingui)

- Copy:
    - Cut the copy by 50% while still making it easy to lead from interest to transaction?
    - Cut number of clicks to go from landing to actual sale?
    - How to make the experience pleasurable and easy without taking away from the actual product or service being sold?
    - If they don't convert, how can I get them to later?
    - How do I leave extraordinary impressions via marketing (e.g. social media channels)?

### How not to screw up your National ID

[Article](https://www.medianama.com/2017/11/223-how-not-to-screw-up-your-national-id-india-aadhaar/)

1. Make it optional: national identities are a recipe for surveillance and data leaks
    - **Data is a toxic asset!**
1. Make it one of the many ID's for authentication: don't increase risks by centralizing on one single ID
    - Centralization creates a new power center, who has full control over listing and delisting individuals
1. Give control to users, to change and revoke an ID: users should have knowledge of when and where their ID has been used, and have control over freezing it, etc
1. Enforce the usage of derived authentication/pseudomisation: use derivative IDs rather than a single ID
1. Give citizens legal right to recourse: if something screws up, make sure you're accountable
1. Purpose limitation for national ID usage: don't use the ID unless absolutely necessary
1. No biometric authentication: biometric information is permanent, and **can be easily compromised**; they can also degrade with time
1. Data protection law comes BEFORE national ID: make sure you're accountable
1. Don't push for 100% penetration right away: causes unnecessary stress and opens up attack vectors
   for exploitation and fraud
1. Budget for citizen awareness, education, and grievance redressal
