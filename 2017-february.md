February 2016
=============

Tech
----

### RethinkDB: Why We Failed

[Article](http://www.defstartup.org/2017/01/18/why-rethinkdb-failed.html)

- **Picked a terrible market and optimized the product for the wrong metrics of goodness**
- "You're in the market *your users* think you're in," and that frames what they think of you (and who you really are)
- Understand how microeconomics works in your market (e.g. developer tools: lots of free competitors; difficult to get anyone to pay for your product)
- "Early distribution challenges almost always doom you to eventual death"; getting a feedback loop for traction from the start is important!
- "It turns out that correctness, simplicity [...], and consistency **are the wrong metrics of goodness** for most users"
    - Most users want things fast, usable by them, and solving a specific problem (that they have)
- "MongoDB turned regular developers into heroes *when people needed it*"
- You have all the time in the world to fix your problems, one by one, once you're established
- **Don't be three years behind your competitors!** Pivot your way into something you can control.
- Avoid optimism bias; you are (likely) **NOT** to be different from other people who fall into the same trap
- Advice:
    - Pick a large market but build for specific users
    - Learn to recognize the talents you're missing, then work like hell to get them on your team
    - Read The Economist religiously. It will make you better faster.

### The Rise of Worse is Better

[Article](http://dreamsongs.com/RiseOfWorseIsBetter.html)

- Worse-is-better
    - Favour simplicity; try to maximize correctness, consistency, and completeness, but favour them in that order (rather than trying to sacrifice some attributes to maximize the latter attributes)
- Implementation simplicity is more important than interface simplicity
    - Simple means it's easier to port, change, and modify
    - Sacrifice safety, convenience, hassle, and magic (to the user) to keep performance good on worse machines
- Favour things that will make distribution easier in the long run (e.g. simplicity!)
    - But make sure the simple thing is **good**
- Worse-is-better: gain acceptance, condition users to expect less, and then improve to a point that it's close to the right thing
- **"Often undesirable to go for the right thing first. It is better to get half of the right thing available so that it spreads like a virus."**
    - Note that half of the right thing is still basically right!

### Measure Anything, Measure Everything

[Article](https://codeascraft.com/2011/02/15/measure-anything-measure-everything/)

- Track everything: network, machine, and application
- Application is the hardest, yet most important
- StatsD uses UDP because it's fire-and-forget
- Sampling can be important for very frequent events (sample: only fire an event once in a while) to not overload monitoring
- "As long as a given solution has next to no management overhead, and is trivially easy for engineers to use, you’ve got something useful."

### HyperLogLog

[Article](http://antirez.com/news/75)

- HyperLogLog approximates the unique size of a set using very little memory (hashes subsets of data, and uses the hash -- a binary value -- to determine how likely the result was; note that in binary, each next result in a row is 50% likely)

### Respect My Authority - Hijacking Broken Nameservers to Compromise Your Target

[Article](https://thehackerblog.com/respect-my-authority-hijacking-broken-nameservers-to-compromise-your-target/)

- Wow DNS caching can be a *b3h*.

### Are we overcomplicating everything?

[Thread](https://news.ycombinator.com/item?id=13426896)

- Always ask yourself if the problem is actually complex or if you're just making it complex (for various reasons, e.g. ego, trying to make work interesting, etc)
    - **Avoid Complexity-for-the-sake-of-complexity**
- Ask the question "when is practice X useful?" instead of "is practice X a good idea?"
- "Microservices probably reduces the asymptotic cost of scaling but add a huge constant factor."
- "Statefulness is inherently complex"
- There is no silver bullet (a single design will not work best everywhere)
- Favour disposable code over reusable code (YAGNI; don't generalize prematurely)
- "Code means communication"
- "The smartest people in the room are the ones who can speak about complex topics in a simple way"
- Understand when a best practice is best; it may not always apply
- "I think this is down to the sad truth that most developer roles offer very little challenge outside of learning a new stack"
- "Comparative analyses to make objective recommendations between different solution alternatives [including architectures and tools]" should be in interviews
- Think about goals rather than specific solutions first: **your solution should be the best fit for the problem at hand**
- Hand *repeatable* and *repeatable* tasks to computers (and feel free to make those more complicated)
- "You can know what features are in a release or when the release will ship, but not both" -- Rob Gingell

### Logs Are Streams, Not Files

[Article](https://adam.herokuapp.com/past/2011/4/1/logs_are_streams_not_files/)

- Logs are time-ordered streams
- Streams are more powerful than files; if you want to, you can redirect a stream into a file but you can also redirect to multiple locations or programs
- Use the syslog protocol (`logger`) for logging distributed systems


Life
----

### Why time management is ruining our lives

[Article](https://www.theguardian.com/technology/2016/dec/22/why-time-management-is-ruining-our-lives)

- "The pressure of trying to complete an ever-increasing number of tasks, in a finite quantity of time, was becoming impossible to bear"
- Lots of things are happening today because of our "quest for increased personal productivity" (products, rhetoric, etc)
- Being more efficient / productive at something doesn't always bring benefits (e.g. hyper productive on email == more email, whereas neglected email means people stop caring)
- Don't live under the illusion that everything, eventually, will come under control. This is impossible in modern life.
- **"The average lifespan consists of only about 4,000 weeks"**
- There's a momentum towards more work; it often feels impossible to cut down on it
- Current gig-economy dynamics enforce this behaviour; the only person who suffers if you get lazy is you
- Maybe "getting things done" is the wrong focus; what do those things amount to?
- If everything is centered around efficiency (or economic gain), then other activities are judged by their usefulness towards productive activities (e.g. sleeping for work)
- Awareness of limited time degrades performance; stress gets in the way
- The more productive and efficient you are, the less adaptable you will be to new or unexpected events (e.g. unexpected patients)
- "Personal productivity presents itself as an antidote to busyness when it might better be understood as yet another form of busyness"

### When You Are Depressed, Make Something

[Article](https://byrslf.co/when-you-are-depressed-make-something-49467edd1933#.81ttzaq8m)

- "Sadness is when you feel down because things aren’t going your way. Depression is when you feel down even when all is going well."
- Depression masks itself as circumstantial sadness --> reinforced feedback loop of negativity
- **"No one judges you more than the way you judge yourself"**
    - Don't be afraid, you're already your worst critic
- Creativity and making something allow you to focus on the present and enjoy it
- "The ability to create and share is a vessel for your spirit. It is a gift that has been passed down through millennia. Use it when you need it most."
- "Every child is an artist. The problem is how to remain an artist once he grows up." -- Picasso

### The Real Reason Your City Has No Money

[Article](https://www.strongtowns.org/journal/2017/1/9/the-real-reason-your-city-has-no-money)

- "Humans are predisposed to highly value pleasure today and to deeply discount future pain, especially the more distant it is.”

### Poor Neighbourhoods Make the Best Investment

[Article](https://www.strongtowns.org/journal/2017/1/10/poor-neighborhoods-make-the-best-investment)

- "Poor neighborhoods subsidize the affluent; it is a ubiquitous condition of the American development pattern."
- Poorer areas have less infrastructure to manage (and may be denser)

### The Risk of Discovery

[Article](http://www.paulgraham.com/disc.html)

- We often discard failures and embelish successes once we know the results. But until then, everything has a chance and is risky.

### The Reality of Developer Burnout

[Article](https://www.kennethreitz.org/essays/the-reality-of-developer-burnout)

- "Burnout is sneaky. It doesn’t usually announce itself. It slowly grinds at you until these feelings become the new normal, and at that point it’s not easy to dig yourself out of the hole." -- Zach Holman
- Publish-only: stop paying attention to all outside events and noise
- Have other hobbies than writing code

### If Your Boss Could Do Your Job, You're More Likely to Be Happy at Work

[Article](https://hbr.org/2016/12/if-your-boss-could-do-your-job-youre-more-likely-to-be-happy-at-work)

- “People don’t quit bad jobs, they quit bad bosses”
- "Bosses matter far more for employee job satisfaction than any other factor we measured"
- "Employees are far happier when they are led by people with deep expertise in the core activity of the business"

### How Much Does Employee Turnover Really Cost

[Article](https://medium.com/latticehq/how-much-does-employee-turnover-really-cost)

- Most understand turnover is costly, but don't have a way of quantifying it
- People optimize what they can measure (quantitively!)
- Understanding something quantitively is often a first step towards a solution
- Formula: cost = # of regrettable departues x average cost of departures
    - # of departues = # of employees x annual turnover percentage
    - Average cost includes:
        - Cost of hiring
        - Cost of onboarding and training
        - Cost of learning and development
        - Cost of time with unfilled role
- Addressing churn: low pay can contribute, but high pay doesn't make up for bad workplaces
    - Focus on (long-term) growth, impact, and care (making them feel valued; surround your company with people who want something for **others**)

### The Best Way to Find More Time to Read

[Article](https://www.farnamstreetblog.com/2013/09/finding-time-to-read/)

- Reading: "Mastering the best that other people have already figured out"
- "Men who have made these discoveries before us are not our masters, but our guides.” -- Seneca
- “In my whole life, I have known no wise people (over a broad subject matter area) who didn’t read all the time – none, zero.” -- Charlie Munger

### The Meaning of Low Interest Rates

[Article](https://keepingstock.net/the-meaning-of-low-interest-rates-5409de0173e8#.2k77yprhu)

- "What does it mean to our culture that interest rates are so low, even negative, in many places?"
- "For interest rates to be so low effectively means that there are not a lot of good ideas about how to make life better in the future."
- Cash is sitting idle (albeit safely) because there's nothing obvious left to explore (that will create returns)
- "Europe and Japan keep rates at rock bottom, and indeed negative in places, to placate otherwise-tottering balance sheets of zombie enterprises."
- "The inability to honestly face failure has led to its subsidization."

### The Psycohology of Human Misjudgement

[Video](https://www.youtube.com/watch?time_continue=36&v=pqzcCfUglws)

- Economics is **always** behavioural
- Economics <==> Psychology
- Don't do sloppy accounting (when it's bad for business, the accounting should show that)!
- Your advisors have **a lot** of bias!
    - Either apply some slack to their advice, or
    - Learn some of the trade and ask them to explain their advice (and why they're right)
- "I don't think vengence is much good"
- When you want to persuade someone, you **really** should tell them why (and maybe add in one of the below)
- Recognize:
    - Power of incentives (i.e. reinforcement)
    - Psychology of denial
    - Incentivized bias (i.e. agency costs)
    - Bias from consistency and commitments to conclusions
        - Don't chain your brain by declarations and commitments
        - What you do will change what you think
        - Medical training: watch one, do one, train one
    - Bias from past correlation and association
    - Information inefficencies
    - Reciprocation tendency
        - Ask for a lot, then back off a bit
    - Bias from conclusions of others
        - Don't cargo cult
    - Contrast bias
        - If it comes to you in small pieces, you might miss it
    - Influence from authority
    - Bias from present or threatened scarcity
        - Minor depreciations or appreciations
    - Envy and jealousy
        - "It's not greed that runs the world, it's envy" -- Warren Buffet
    - Misgambling compulsion
    - Liking distortion (e.g. one's own self, ideas, etc)
    - Disliking distortion (e.g. somone disliked)
    - "Man with the hammer" syndrome (don't force every problem into the same box)
    - Your brain is not (!) mathematical; it is heuristical!
        - Don't overweigh the information you have at hand
        - Don't jump on available information
    - Overinfluence by extra vivid information
    - Not properly explaining "why" -- don't kid yourself when you don't do a good job
    - Stress-induced mental changes
    - "Say something" syndrome
        - People might not know how to express something, but just want to say something
- **Combining multiple of the above produces an exponential result**
- Do something painful and then something rewarding to treat yourself
- Revisit your choices, and understand why something did (or did not) work out

### How to Read a Book

[Article](http://www.artofmanliness.com/2013/06/17/how-to-read-a-book/)

- Stages of reading:
    1. Elementary
    1. Inspectional
    1. Analytical
    1. Syntopical (synthesis of different opinions into another work)
- What does the book tell us about the "six great ideas" (Truth, Beauty, Goodness, Justice, Liberty, and Equality)
- Inspectional reading
    - Read title and front and back (what do they try to convey?)
    - Pay attention to the first few pages
    - (Non-fiction) Read headings and conclusion
    - Read reviews
- Analytical reading
    - Research the author a bit
    - Do a bit of inspectional reading
    - Do a first superficial run through first
        - Ask questions, highlight important parts (but leave those for later)
    - Read it again, more slowly, some time after
    - Try to figure things out first on your own (like unknown words), but use aids if necessary
    - **Answer:**
        - What is the book about? **Write a few sentences yourself to summarize!**
        - What is being said in detail? **Write a few sentences about the overall structure and what happens where (e.g. per chapter)**
        - Is the book true (in whole or part)? What do you believe is true?
        - What's the significance? What's the takeaway? **How does it make you think differently about the world?**
    - Critique and share your thoughts with others

### How to Mark a Book

[Article](http://chuma.cas.usf.edu/~pinsky/mark_a_book.htm)

- To get the most out of anything, "read between the lines"
- "Full ownership comes only when you have made it a part of yourself"
- Marking up a book keeps you awake (more than just consciously) ;)
- **Active reading is thinking**
- Preserve your reactions and sharpen your questions
- **Reading a book should be "a conversation between you and the author"**
- Understanding is a two-way operation
- Marking:
    - Underlining: major points, important statements
    - Vertical lines at margin: emphasize underlined statement
    - Asterisk at margin: most important statements in the book
    - Numbers at margin: sequence of points made for developing a single statements
    - Page numbers at margin: other areas in the book the author made relevant points
    - Writing at margin: questions, answers, reducing thoughts into a single statement
- End papers: index of author's points, and outline of book
- "There is no such thing as the right speed for intelligent reading... The sign of intelligence in reading is the ability to read different things differently according to their worth"


Random
------

### Never Talk to the Police

[Article](https://www.vice.com/en_us/article/law-professor-police-interrogation-law-constitution-survival)

- Always ask for a lawyer, and keep on asking
- Anyone may misinterpret or forget what you said
- You never know if what you're saying could implicate you

### VR

[Article](https://blog.ycombinator.com/vr/)

- "With VR, there isn't already an app for that"
