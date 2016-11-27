October 2016
============

Tech
----

# Use the Unofficial Bash Strict Mode

[Article](http://redsymbol.net/articles/unofficial-bash-strict-mode/)

- Use:

```bash
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'
```

- `set -e`: Immediately exit if any command has a non-zero exit status
- `set -u`: Referencing any variable you haven't previously defined is an error
- `set -o pipefail`: A failed return code from any command in the pipeline will cause the entire pipeline to fail
- `IFS`: *Internal Field Separator*; controls word splitting (each character in the string will be considered for separating words)
- Use `|| true` to use commands that are expected to return non-zero statuses
- Use [bash exit traps](http://redsymbol.net/articles/bash-exit-traps/) to ensure resource clean up happens

### Scalability and Performance are the Least of your Worries

[Article](http://www.expatsoftware.com/articles/2007/06/getting-your-priorities-straight.html)

- "Speed is largely irrelevant for a web application"
- Readability, debugability, maintainability, and development pace are more important
- Make things easy to debug!
- Use good tools to stay productive (for hiring too)
- Use abstractions to allow horizontal scaling of bottlenecks

### Two Weeks Vacation is only a Recommendation, not a Rule

[Article](http://www.expatsoftware.com/articles/2007/02/two-weeks-vacation-is-only.html)

- "In practice, the amount of vacation time you can take is directly related to your value to the company"
- "You are a lot more valuable to your employer than they are to you"
- Just tell, don't ask, for time off

### A decentralized web would give power back to the people online

[Article](https://techcrunch.com/2016/10/09/a-decentralized-web-would-give-power-back-to-the-people-online/)

- "The original purpose of the web... was to build a common neutral network which everyone can participate in equally"
- Web 3.0: trend of building services that don't depend on any single central organization
- Services are provided by technologies that are powered by the people
- Big on privacy, data portability (and users owning their own data), and security
- Perhaps the current siloed applications will give way to decentralized ones

### Wat

[Article](http://danluu.com/wat/)

- Ingrained bad practices begin when companies are founded and are concentrated on product growth.
- The culture has to change once growth has been accomplished
- "Anyone who comes into one of these companies from Google, Amazon, or another place with solid ops practices is shocked. Often, they try to fix things, and then leave when they can’t make a dent."
- Companies only get better once they've been embarrassed a few times; these events give people who wanted to do something "right" more leverage
- "The data are clear that humans are really bad at taking the time to do things that are well understood to incontrovertibly reduce the risk of rare but catastrophic events. We will rationalize that taking shortcuts is the right, reasonable thing to do."
- "Humans are bad at reasoning about how failures cascade, so we implement bright line rules about when it’s safe to deploy. But the same thing that makes it hard for us to reason about when it’s safe to deploy makes the rules seem stupid and inefficient!"
- "In most company cultures, people feel weird about giving feedback. Everyone has stories about a project that lingered on for months after it should have been terminated because no one was willing to offer explicit feedback."
- "People get promoted for heroism and putting out fires, not for preventing fires; and people get promoted for shipping features, not for doing critical maintenance work and bug fixing. How do you change that?"
- Preventing normalization of deviance:
    - Pay attention to weak signals
    - Resist the urge to be unreasonably optimistic
    - Teach employees how to conduct emotionally uncomfortable conversations
    - System operators need to feel safe in speaking up
    - Realize that oversight and monitoring are never-ending
- "People write a lot about how things like using fancier languages or techniques like TDD or agile will make your teams more productive, but having a strong engineering culture is much larger force multiplier."
- "The larger the project, the more visiblity and promotions, even if the project could have been done with much less effort."
- "Something I’ve seen multiple times is that, when a VP leaves, a company will become a substantially worse place to work, and it will slowly dawn on people that the VP was doing an amazing job at supporting not only their direct reports, but making sure that everyone under them was having a good time."

### A Comprehensive Guide to Terraform

[Article](https://blog.gruntwork.io/a-comprehensive-guide-to-terraform-b3d32832baca#.z9lei1hmo)

- Goal is to write code to define, provision, and manage infrastructure
    - Automate provisioning and deployment rather than use humans

### Why we use Terraform

[Article](https://blog.gruntwork.io/why-we-use-terraform-and-not-chef-puppet-ansible-saltstack-or-cloudformation-7989dad2865c#.x7ai1ivcw)

- Configuration Management vs Orchestration
    - Install and manage software vs. provisioning servers
        - Using containers means that your configuration is already mostly done
- Mutable infrastructure vs immutable infrastructure
    - Mutable produces *configuration drift* since they update in-place rather than spin up new servers
- Procedural vs Declarative
    - Step-by-step instructions vs. declaring desired end state
        - Procedural requires you to know your current state, since rerunning configuration *adds* to the current state (rather than *updating to* it)
        - Procedural code doesn't describe the full state of the infrastructure

### An Introduction to Terraform

[Article](https://blog.gruntwork.io/an-introduction-to-terraform-f17df9c6d180)

### Kanban and the Stages of Grief

[Article](http://adzerk.com/tech/2016/04/kanban-and-the-stages-of-grief/)

- Software constantly changes, and "with change comes loss" --  code won't be around forever and is likely to break at some point
- Stages:
    1. Denial: Don't work on something unless you know it'll resolve the underlying problem (maybe a bug will be resolved better by a feature)
    1. Anger: Don't represent the development phase as a linear process; use frustration to find creative solutions
    1. Bargaining: Bargain to get code reviewed
    1. Depression: "Anger turned inward... [is] how we view our QA process". Make sure the work passes specs; if it's stuck, start intervening (e.g. abandoning, changing tactics, etc)
    1. Acceptance: Add finishing touches, e.g. update knowledge base, reach out to customers, follow-up for future work, etc

### We only hire the best means we only hire the trendiest

[Article](http://danluu.com/programmer-moneyball/)

- "If your [recruiting] type is the same type everyone else is competing for, “you are competing for talent with the wealthiest (or most overfunded) tech companies in the market”."
- Offerring non-competitive compensation packages likely means you have, proportionally, very few senior devs
- "And as people get more experience, they’re less likely to believe the part of the pitch that explains how much the stock options are worth."
- "People with great backgrounds are, on average, pretty great, but they’re really hard to hire. It’s much easier to hire people who are underrated, especially if you’re not paying market rates."
- Don't look for the "trendiest," look for those the market have undervalued
- People seem to have different levels of attractiveness to employers at various times, usually due to superficial factors based on trendiness and not on productivity
- Hiring pipelines can get crippled by going after the same people everyone else is going after
- "Not only are these decisions non-optimal for companies, they create a path dependence in employment outcomes that causes individual good (or bad) events to follow people around for decades. You can see similar effects in the literature on career earnings in a variety of fields."
- "But a large component of these markers of success, not to mention success itself, is luck."
- "I believe they [Google] talked about how focusing on top schools wasn’t effective and didn’t turn up employees that have better performance years ago"
- There's a momentum around strategies that are controversal, but effective (e.g. moneyball in baseball; unconventional hiring in tech)
- Training is also very important; and most companies spend little, if any, on training employees.
- Go out of your way to do stuff at a company; you'll likely learn a lot more that way
- Tools can make or break your productivity; they "can easily make a larger difference than “hiring only the best”"
- "I’ve literally never found an environment where you can’t massively improve productivity with something that trivial."
- "We like to think that we’re different from all those industries that judge people based on appearance, but we do the same thing, only instead of saying that people are a bad fit because they don’t wear ties, we say they’re a bad fit because they do, and instead of saying people aren’t smart enough because they don’t have the right pedigree… wait, that’s exactly the same."
- False positives in hiring are bogus: "If you hire anyone, you’re trading off the cost of firing a bad hire vs. the cost of spending engineering hours interviewing."

### Should I buy ECC memory?

[Article](http://danluu.com/why-ecc/)

- Don't blindly copy experiments from others; they may have failed (and not talked about it)
- Even if you copy the good ideas, it might not make sense for you (at your scale, for your needs, etc)
- "In a system that can tolerate a number of failures at the software level, the minimum requirement made to the hardware layer is that its faults are always detected and reported to software in a timely enough manner as to allow the software infrastructure to contain it and take appropriate recovery actions."

### Lession Learned from reading postmortems

[Article](http://danluu.com/postmortem-lessons/)

- Error handling:
    - Bugs in error handling code means that the probability of sequential bugs is not just the multipled independent probabilities of the individual errors
    - Not obvious that sufficient test and static analysis efforts for testing error handling
    - "If you care about building robust systems, the error checking code is the main code!"
- Configuration:
    - Configuration bugs may be more common than code bugs for causing outages (and definitely more common than hardware problems!)
    - Make sure to test and stage config changes; create environments to test configuration changes!
- Hardware
    - Consider that failover from bad components can also fail
- Humans
    - Humans are even more error prone than machines; don't put them in a position where they can accidentally cause catastrophic failure (or you'll eventually get a catastrophy)
    - Making humans take extra steps to mitigate human risk might not be a good idea; maybe use automation instead?
- Monitoring
    - "Heroism isn't a scalable solution"
    - Make sure alerts go to the right groups of people, and has the right processes behind them to mitigate risk
- "Just because something is obvious doesn’t mean it’s being done."

### Everything is Broken

[Article](http://danluu.com/everything-is-broken/)

- Check out:
    - Property-based testing
    - Generative testing
    - Random testing
    - Concolic Testing (which was done long before the term was coined)
    - Static analysis
    - Fuzzing
        - "If you’re going to spend a few hours writing tests, a few hours writing a fuzzer is going to go a longer way than a few hours writing unit tests."
    - Statistical bug finding

### Developer Hiring and the Market for Lemons

[Article](http://danluu.com/hiring-lemons/)

- Common wisdom (not necessarily true): great developers won't have many jobs (compared to bad developers) because companies try their best to keep great developers
- Good developers may not be overrepresented in the market; assuming you can't differentiate between a good developer and a bad developer, good developers will be sticky because employers know they're good and won't let them go. This eventually causes a feedback loop so that bad developers are the only hires available
- If you can tell someone is great, offer them lots more money; however, this requires an information asymmetry between what you know and what the market knows (but there might not be)
- "When I worked at a small company, we regularly hired great engineers from big companies that were too clueless to know what kind of talent they had."
- Making developers "sticky" requires an organization to create groups that people want to work for; finding such a group is incredibly hard.
    - Such teams are always full, because everyone wants to work for them. Hiring teams may be the ones that lose a lot of members each yeah, creating turnover
    - "As a dev, if you join a random team, you’re overwhelmingly likely to join a team that has a lot of churn. Additionally, if you know of a good team, it’s likely to be full."
- Assumption for common wisdom: there are more dysfunctional developers than there are dysfunctional work environments
    - This is likely to be blatently wrong!
    - Ancedotal: nobody thinks their company is not highly dysfunctional, but also doesn't know of one (or a group inside one) that isn't (they'd go try to work for them!)
    - Usually people know of good developers looking for work
- "Most companies invest pretty much nothing in helping people, you can do really well here without investing much effort"
- "The fact that joining a new team is uncertain makes developers less likely to leave existing teams, which makes it harder to hire developers. But the fact that developers often join teams which they dislike makes it easier to hire developers."
- No sympathy for hiring managers who complain that hiring "great" developers is hard:
    - May pay too little
    - Pass on what they think are "good" or "great" developers, because "they're not good enough": "almost everyone uses the same filters, so everyone ends up fighting over the 30 people who they think are solid"
        - Protects the hiring manager if the person doesn't work out; can't blame him for hiring someone who everyone thinks is "good"
    - Try to hire for rare combinations of rare skills
        - Hire people who only have a subset of those skills and then train them
    - Doesn't realize how dysfunctional the organization is (e.g. employees under hate the group)
- Often "great" devs may be unfashional or untrendy and go unnoticed for years without good opportunity
- Referral schemes are shotty–people will refer bad candidates for the incentive

### What's worked in computer science

[Article](http://danluu.com/butler-lampson-1999/)

- "To do parallel programming, what you need to do is put all your parallelism into a little box and then have a wizard go write the code in that box"
- If the vast majority of programmers can't easily use a class of technologies, it probably hasn't succeeded

### Levels of Fuzzing

[Article](http://blog.regehr.org/archives/1039)

- *Mutational* fuzzing: the input to a system under test is being randomly changed
- *Generational* fuzzing: the input to a system under test is being randomly generated

### Why You Only Need to Test With 5 Users

[Article](https://www.nngroup.com/articles/why-you-only-need-to-test-with-5-users/)

- Best results of user testing is with five people, and running as many tests as possible
- Based on stats, you can expect diminishing returns with extra people joining tests, but the sweet spot is five (~75% of all problems)
- Testing more often means you get to fix previous problems and test their solutions (or regressions!) as well (rather than blow the budget on a few tests)
- "The real goal of usability engineering is to improve the design and not just to document its weaknesses"
- Each iterative test will likely uncover deeper issues in the design than superficial problems
- Always test in groups of 3-5
- More people might be needed if your core audience is segregated into clusters of distinct personas

### Why's that company so big? I could do that in a weekend

[Article](http://danluu.com/sounds-easy/)

- "Businesses that actually care about turning a profit will spend a lot of time (hence, a lot of engineers) working on optimizing systems"
    - Even small (single digit) percentages are likely to be cause enough savings for one (or more) full time engineers
    - "Businesses should keep adding engineers to work on optimization until the cost of adding an engineer equals the revenue gain plus the cost savings at the margin."
- "The question isn’t whether or not there will inefficiencies, but how much inefficiency"
- "For a lot of products, the sales team is more important than the engineering team"

### HN comments are underrated

[Article](http://danluu.com/hn-comments/)

- Excellent developers are excellent because they know how to determine what work will be valuable; let them make their own architectural choices!
- The key to being a 10x developer is to work on problems that have 10x impact and not necessarily writing 10x more code

### Reflections of an "Old" Programmer

[Article](http://www.bennorthrop.com/Essays/2016/reflections-of-an-old-programmer.php)

- Other professions don't seem to have to shed some of their prior knowledge for new skills; the knowledge they've accumulated is fairly stable
- "Half of what a programmer knows will be useless in 10 years"; the **knowledge decay** in software is very rapid
- Balance knowledge decay against your **knowledge accumulation rate**
- Once you're a veteran, you go between losing some of your useful knowledge to regaining it depending on your knowledge **decay** and **accumulation** rates
    - **"There is no coasting"**
- Invest most in knowledge that is durable!

### Let's not be Slaves to Fashion

[Article](http://www.bennorthrop.com/Essays/2015/slaves-to-fashion.php)

- Don't use something for the sake of its "newness" or "coolness"
- "**Be judicious about adopting innovation.** The right tool for the right problem."

### How the Web Became Unreadable

[Article](https://backchannel.com/how-the-web-became-unreadable-a781ddc711b6#.yahcmuope)

- Decreasing the contrast between text and background makes it harder to read
- We should be building a baseline structure for text that everyone can read

### Combingin AFL and QuickCheck for directed fuzzing

[Article](http://danluu.com/testing/)

- Handwriting tests isn't the only way to test; think about automated tests too
- Random test generation
    - Try fuzzing
    - Start simple, generate dumb tests, and add constraints later for more complex bugs
- Random test generation frameworks
    - Try to use one!
- Random test generation, coveraged based
    - Hard to get a good balance between coverage metrics: line-based is too broad, whereas state-based is intractable
    - Use an approximation instead
- Why no coverage-based unit testing?
    - "I often assume that if there isn’t an implementation of a straightforward idea, there must be some reason, like maybe it’s much harder than it sounds"
- Attitude towards tests is a big factor; e.g. how much you accept bad bugs occuring frequently

### Testing v. informal reasoning

[Article](http://danluu.com/tests-v-reason/)

- "There’s no way to avoid bugs if you create a system that’s too complex to formally verify"
- You can't make everything simple enough to be reasoned by a single human
- "Testing may not be sufficient to find all bugs, but it can be sufficient to achieve better reliability than pretty much any software company cares to."

### Performance Is a Science

[Article](http://duartes.org/gustavo/blog/post/performance-is-a-science/)

- Make accurate measurements of real-world workloads to analyze performance

### Being a Developer After 40

[Article](https://medium.freecodecamp.com/being-a-developer-after-40-3c5dd112210c#.lm20c2tjz)

- To stay sane after 40:
    - Forget the hype, keep doing your thing
    - Only be interested if you have a genuine interest and feel it could bring benefits in the long term
    - Choose your tech stack/community wisely, but keep looking around at other communities and don't be afraid to convert
    - Learn the origins of your most used and favourite tools
    - Everything is a remix of older things
    - Learn lots, but teach more
    - "The fact that you understand something does not imply that you have to agree to it"
    - "Do not let a bad job kill your enthusiasm. It is not worth it. Disobey and move on."
    - "Do not blush or be embarrased for changing your opinions"; do what you think is right, and self-reflect to make sure it's ethically right
    - Great APIs enable great apps

### Firing People

[Article](https://zachholman.com/talk/firing-people)

- Not many people talk about getting fired publicly, and this is a problem
- There is real pain associated with getting forced out of a company
- A lot of advice is needed beyond the common wisdom of "fire fast"
- "How we treat employees, past and present, is a reflection on the company itself"
- Everyone's at risk: "unless you own the company, the company owns you."
- Be ware of any sudden goal post movement; if someone's suddenly changing specific guidelines for you to follow, it's probably not good
- Don't talk to HR, as an employee; HR exists to protect the company's interests, bringing something to the attention of HR is a risk
- Companies: don't surprise people; give them lead time, e.g. with a performance improvement plan for the employee
- If you get fired: chill out and get some time to think about things; arguing isn't going to help anything
- The person doing the firing does it more often than you do; they're definitely better at it
- If you're frustrated from firing people, vent up the chain of command, not down
- Coworker: find out why someone got fired, and if it'll impact you (e.g. team is shutting down)
- Companies: be truthful to your employees.
- "Be a bit misleading today and everyone will look at you as being misleading in the future."
- Getting fired and dying are some of the few experiences you don't share with others (arguably)
- Get everything in writing in terms of legal contracts, etc.
- Set up an alumni group on Facebook, Slack, etc.
- "You want them [your employees] to move on and do great things. You want them to carry with them the best parts of your culture on to new challenges, new companies, and new approaches."
- Alumni are great resources for recruiting talent
- "Maybe we should simply recognize it’s time for next"

### Applying the Linus Torvalds "Good Taste" Coding Requirement

[Article](https://medium.com/@bartobri/applying-the-linus-tarvolds-good-taste-coding-requirement-99749f37684a)

- The less conditionals required, the less edge cases to be considered, and (most likely) the better the code is
- Coders with good taste take the time to conceptualize what they're building and define their component's boundaries and interactions with each other
- Initializing a grid is probably good for a coding interview exercise (consider constraints, complexity, edge cases)


Life
----

### RethinkDB, SageMath, Andreessen-Horowitz, Basecamp, and Open Source Software

[Article](http://sagemath.blogspot.de/2016/10/rethinkdb-sagemath-andreessen-horowitz.html)

- RethinkDB did not have a *real* business model
- "Number of users tends to be roughly linearly related to mailing list traffic"
- "When founding a company, you can choose how your company will be incentived based on the amount of risk you are willing to take, the resources you have, the sort of business you are building, the current state of the market, and your model of what will happen in the future."
- "They [A16Z] said there was no place for A16Z to invest directly in what I was planning to do, since I was very explicit that I'm not looking for an exit, and my plan about how big I wanted the company to grow in the next 5 years wasn't sufficiently ambitious."
- "Our [SageMath Inc's] open source IP is considered worthless by investors"

### Is Facebook's Massive Open Office Scaring Away Developers

[Article](http://calnewport.com/blog/2016/10/09/is-facebooks-massive-open-office-scaring-away-developers/)

- Joel Spolsky: "Facebook is paying 40-50 percent more than other places, **which is usually a sign developers don’t want to work there.**”

### Be Kind

[Article](https://www.briangilham.com/blog/2016/10/10/be-kind)

- Give others the space they need to make mistakes and grow

### Bring Value

[Article](https://www.briangilham.com/blog/2016/10/3/bring-value)

- Ask how you can bring value to someone today
- "Time spent helping someone else is never time wasted."

### Focus on your 1%

[Article](https://www.briangilham.com/blog/2016/9/19/focus-on-your-1)

- "Focus on your 1%. The people who are genuinely interested in your work and what you have to say. The rest don’t matter."

### Be Boring

[Article](https://www.briangilham.com/blog/2016/9/12/be-boring)

- Focus on one thing at a time; don't be tempted to work on something else
- Set deadlines, and cut scope to make it
- Schedule tasks
- "Be boring in your life, so you may be fearless in your work."

### Submarine

[Article](http://www.paulgraham.com/submarine.html)

- "[Reporters] want statements with punch, like "top ten." And PR firms give them what they want."
- PR firms will feed the same story to multiple places; "when readers see similar stories in multiple places, they think there is some important trend afoot"
    - Self-reinforcing
- Trend articles are almost always the work of PR firms
- For reading PR: "ask not just whether the author is telling the truth, *but why he's writing about this subject at all*"

### What You Can't Say

[Article](http://www.paulgraham.com/say.html)

- "Moral" fashions exist
- "Fashion is mistaken for good design; moral fashion is mistaken for good"
- "What would someone coming back to visit us in a time machine have to be careful not to say?"
- If you don't have opinions that you're afraid to express, you're probably just thinking what you're being told
- If you independently came to the same conclusions, you'd also somehow arrie with the same errors too
- Find out what you can't say by looking at what people say and get in trouble for (assuming they're likely to be true)
- If statements are attacked without factoring in their truth, we should pay attention
- "We may imagine that we are a great deal smarter and more virtuous than past generations, but the more history you read, the less likely this seems."
- Between two sides that are divided on the righteousness of an action, the side that finds it shocking or taboo, may likely be the wrong one
- "A well brought-up teenage kid's brain is a more or less complete collection of all our taboos—and in mint condition, because they're untainted by experience"
- "To launch a taboo, a group has to be poised halfway between weakness and power. A confident group doesn't need taboos to protect it."
- Early adopters confidently want to distinguish themselves; mass adopters adopt because they are afraid of standing out (or missing out)
- "What groups are powerful but nervous, and what ideas would they like to suppress? ... What are conventional-minded people afraid of saying?"
- "When you find something you can't say, what do you do with it? ... Don't say it. Or at least, pick your battles."
    - Don't let it label you; that will only be a distraction
    - You can try to abstract conversations one level higher
- "When people are bad at open-mindedness they don't know it. In fact they tend to think the opposite."
- "You need to be able to watch your own thoughts from a distance."

### Tech Discrimination

[Article](http://danluu.com/tech-discrimination/)

- "When it’s part of a deep-seated belief, it’s hard for people to tell that they’re discriminating."
- "Turns out, the more biased people are, the more objective they think they are, too."

### Your Pipeline Argument is Bullshit

[Article](http://leanangry.tumblr.com/post/125716699460/your-pipeline-argument-is-bullshit)

- Not seeing senior roles representing new hires (e.g. a female) makes them feel uncomfortable
- The problem isn't the pipeline; it's after that: women could be in senior positions, but they left.
- "If you don’t make an effort now to create senior role models, you’re asking every woman coming thru your leaky, smelly, caustic pipeline to endure more stress, to work twice as hard and do twice as much to maybe, just maybe, get where their male peers are. If they don’t leave, which most probably will."

### Startup Tradeoffs

[Article](http://danluu.com/startup-tradeoffs/)

- Large, infrastructure systems are typically more advanced in big companies (they have the resources)
- "Many problems that would be hard problems at startups are curiosities at large companies."
- "There are experiments that startups have a very easy time doing that established companies can’t do"
- "The goal at most big companies to get everyone to the senior level."
- "The definition of senior engineer is basically someone who can independently find and solve problems and doesn’t require any handholding, i.e., someone who’s easy to scale horizontally."

### How to Build a Morning Routine by Habit Stacking

[Article](http://www.samuelthomasdavies.com/how-to-build-a-morning-routine-by-habit-stacking/)

- Take a series of small changes to build a daily routine
- Use an *existing* habit as a trigger for a new habit
- Most reliable cues for habits are behaviours that you already do
- Use a series of small and achievable steps to build momentum for the next task (rather than rely on momentum)
- Implementation intention: "Afer I [existing habit], I will [new habit]"
- "If you don't commit to something, you'll be distracted by everything"

### How to Embrace Boredom and Fall in Love with the Process

[Article](http://www.samuelthomasdavies.com/how-to-embrace-boredom-and-fall-in-love-with-the-process/)

- Make practicing fun and addictive
- "If it can be counted, it can be turned into a game"
- Build streaks for habit forming

### How Changing One Word Can Help You Achieve Your Goals

[Article](http://www.samuelthomasdavies.com/how-changing-one-word-can-help-you-achieve-your-goals/)

- Three levels of want:
    - "I want": I'll take it if it falls on my lap
    - "I decide": I'm choosing to do this
    - "I commit": I'm devoting myself to this

### Everything is a Remix

[Video](http://everythingisaremix.info/watch-the-series/)

- We like familiar things, but also are intrigued by novel ideas
- The most influential are those that seem novel, but have familiar elements
- Make your novel ideals more approachable by using old and familiar concepts
- "Creation requires influence"

Random
------

### The Anti-Helicopter Parent's Plea: Let Kids Play

[Article](http://www.nytimes.com/2016/10/23/magazine/the-anti-helicopter-parents-plea-let-kids-play.html?_r=0)

- Let yo kids play, yo
- Stop micromanaging kids
