November 2016
=============

Tech
----

### Inversion of Control Containers and the Dependency Injection Pattern

[Article](http://martinfowler.com/articles/injection.html)

- Component: software that's intended to be used without changing its code by an application
- Service: software that's used remotely, through some interface (e.g. web service, RPC, socket, etc)
- If a generic interface should be reused, the user class should be independent from the instance and only depend on the interface
- How do we create instances of these interfaces and then inject them into the dependent class?
- Dependency injection: use an "assembler" object to inject implementations into dependent classes
- Three types of dependency injection, where there is usually a container holding all the dependency registrations:
    - Interface injection
        - Use a interface or abstract class to define the expected interface for injecting dependencies
        - Define injector interfaces that are implemented by the injected classes to inject themselves into the dependent classes
        - A set up class can use a separate config to set up the classes through their defined interfaces
    - Constructor injection
        - List dependencies in the dependent class's constructor arguments
        - Can use a separate config file to manage the set up
    - Setter injection
        - Use setter functions to inject dependencies
        - A set up class can use a separate config file to create instances of everything
    - Constructor vs setter:
        - Should you fill fields in a constructor or with setters?
        - Usually you should default to creating valid objects at construction
            - You can hide private state by not providing setters (if setters are a thing)
            - "A long constructor is often a sign of an over-busy object that should be split"
            - May be a problem with objects that hold a lot of state of the same type (confusing constructors) or lots of inheritance (explosion of constructors)
- Service locator: An object in the system will know how to get all of the services the application needs
    - Register dependencies into these objects
    - Can be easily designed to be hard to test; they might not be substitutable by other implementations
    - Think of it as a registry, not a singleton
    - Could make it dynamic by not using field names but through dictionaries
- Dependency injection vs service locators:
    - Both provide the fundamental decoupling between the user of an implementation vs the actual implementation but differ in how the implementation is provided to the user
    - Inversion of control (dependency injection) may be harder to understand and debug, so it should be justified over a simpler alternative
        - But it does make it easier to see what a component's dependencies are
        - Imposes simple conventions for others using your component
    - Service Locators force users to have a depdency on the locator, which may not be elegant
        - Usually non-optimal when you can't depend on a constant interface for the locator (e.g. when providing a component for other developers)
- Code vs configuration files:
    - For applications deployed in multiple places, an external configuration file is likely preferrable
    - Complex configuration may be better suited for programatic configuration (maybe with a builder pattern)
    - Configuration files only work well if they're simple
    - If you start having a lot of configuration files (e.g. for each component), always provide an easy way to do configuration through a programmatic interface

### The Eight Fallacies of Distributed Computing

[Article](https://blogs.oracle.com/jag/resource/Fallacies.html)

1. The network is reliable
1. Latency is zero
1. Bandwidth is infinite
1. The network is secure
1. Topology doesn't change
1. There is one administrator
1. Transport cost is zero
1. The network is homogeneous

### A Crash Course on Product Design

[Video](https://www.youtube.com/watch?v=NF2Rb3Kd96k)

- Iceberg secret: users only see 10% of the company; they only see the frontend
- **Design is the product**
- "Design is about helping people achieve their goals"
- Figure out who is using your software: make personas
- Software products have **mental** limits
- Focus on simplicity for the user
- Humans interact with software as if they're human; they express emotions and feel emotions while using software
- Your software should act like a good, considerable person (e.g. help them, give them hints, tell them what's wrong, have humor, etc)
- User testing!
- Visual design
    - Use existing patterns and designs! Don't start from scratch! Use templates and existing tools!
    - Layout: position elements to communicate information (e.g. proximity, grouping, alignment)
    - Typography: use different fonts to communicate information; each one serves **one** purpose
        - Use 45-90 characters on a line (**measure**)
        - Use 1.2-1.45x font size for line height (**leading**)
        - Think about font pairing, but leave it to the pros
    - Contrast: use contrast to make things stand out (e.g. CTA)
        - Use colours wisely
            - Design everything initially in black and white, and then add colour (usually as highlights to add emphasis)

### Properties of Graph DBs & Use Cases

[Video](https://www.youtube.com/watch?v=-dCeFEqDkUI)

- In a DB, developers may be looking for:
    - Intuitiveness: is it logical and elegant? For developers and the business?
    - Speed of development and application
    - Agility: speed of adaption to changes

### OpenTimestamps: Scalable, Trustless, Distributed Timestamping with Bitcoin

[Article](https://petertodd.org/2016/opentimestamps-announcement)

- Timestamps prove that a message existed prior to some point in time ("proofs-of-existence")
- Timestamps do not solve the doublespend problem by themselves

### Time Well Spent

[Video](http://www.timewellspent.io/)

- Don't bulldoze other's attention
- Design for concious interruptions; allow an interruption back-door
- Design for highest-quality interactions, not easiest
    - Don't design for efficiency, design for high-quality
- Measure your design goals
- Ask people how much they want to consume (otherwise they'll just keep consuming it)
- Instead of "get things done," "get life well lived"

### Livable Media: Four Ideas for Better Human Systems

[Article](http://livable.media/)

- Soft automation
    - Software's expectations on humans interactions can be overly rigid and mediated
    - Don't put process above people; let software help humans, not manage them
    - Don't let people become tools for process
- Respectful metrics
    - Don't let metrics focus on manipulating people and exploit their engagement
    - Focus on helping people achieve what they want and express their values
- Meaning-making menus
    - Make menus and options tailored for humans and their goals
- Growth networking
    - Allow social networks to allow humans to grow and explore, rather than creating spaces of isolation
- Think about "who we are, what we need, and what we can be"

### How Technology Hijacks People's Minds

[Article](https://medium.com/swlh/how-technology-hijacks-peoples-minds-from-a-magician-and-google-s-design-ethicist-56d62ef5edf3#.82chmqbu7)

- “It’s easier to fool people than to convince them that they’ve been fooled.”
- Product designers use your psychological vulnerabilities to grab your attention:
    - Controlling the menu controls your choices (users usually aren't the ones creating the menus!)
        - Designers give people the illusion of free choice while making the menu for them means they win no matter what you choose
        - Nobody asks "what's not on the menu," "why only these options," or "what are the provider's goals"
        - Nobody represents a **complete** set of choices, so by only using their options, you might be missing a lot
        - *Most empowering* (to our original goals) is what we should be focusing on, and it's **not** the menu with the most choices
    - Random rewards based on checking frequently (e.g. a slot machine)
        - Designers link an action with a *variable* reward (sometimes a prize, sometimes nothing), to make you addicted to keep trying
        - Designers should try to reduce intermettent variable reward situations (like checking email) into more predictable activities (e.g. only delivering mail at 5pm)
    - Creating a fear of missing out
        - Forces people to keep checking even when they haven't derived recent benefits for the potential "what if"s in the future
        - But we shouldn't care: "we don't miss what we don't see." Instead, we should define our relationships with tools so that they're based on increasing our "time well spent"
    - Creating a desire for social approval
        - Social approval is one of our highest motivations, but now it's in the hands of attention-hungry tech companies
        - Teenagers are most vulnerable to social approval
    - Creating a culture of social reciprocity
        - Social forces incite us to reciprocate the gestures of others, but now this is increasingly in the hands of tech companies
        - Designers exploit an asymmetry in perception; when something notifies you, you think the other party did it *consciously* while tech companies often automate this or make it unconcious (e.g. mass invitations) to benefit from pulling people back into their own world
    - Creating bottomless bowls (e.g. infinite feeds and autoplay features)
        - Designers make it easier for people to keep consuming things despite whether or not they might be hungry
            - "Take an experience that was bounded and finite, and turn it into a bottomless flow that keeps going"
        - Bottomless bowls has been shown to make people eat 73% more than those from a limited bowl
        - The default action for you is to keep consuming, rather than making it harder
        - Designers should be trying to "conciously bound your experience" to align with what "time well spent" means for you
    - Creating interruptions as they come rather than being smart about your focus
        - "Messages that interrupt people immediately are more persuasive at getting people to respond than messages delivered asynchronously (like email)"
        - Interruption and heightened feelings of urgency and social reciprocity **is good for business**
    - Bundling your reasons with their reasons
        - Designers bundle why you use something with how they make money (e.g. watching a video with maximizing consumption)
        - Business won't let you get to what you want without making you go through what they want you to see (e.g. grocery stores)
        - We should be letting users navigate to what they want without forcing them through intentional distractions
    - Businesses make the choices they want you to make easier, and the other ones harder
        - We should be focused on lowering the "friction to enact choices"
    - Not forecasting errors you commonly make
        - Nobody forecasts the cost of a small action (e.g. click) even if it's usually costly
        - Typical sales technique: ask for a small request and then escalate
        - We should be aggregating user data to make it clear what your consequences might be (e.g. typical user spends 20min)
    - "We need technology to be exoskeletons for our minds and interpersonal relationships that put our values, not our impulses, first"

### What single-dispatch generic functions mean for you (Python)

[Article](http://lukasz.langa.pl/8/single-dispatch-generic-functions/)

- Rather than `switch` statements or a series of `if`/`elif`, it may be better to create small functions and put them in a dict (the "dispatcher")
- "Single-dispatch generic functions" are functions that execute different code depending on a single argument

### Best Practices for Designing a Pragmatic RESTful API

[Article](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)

- What should a resource be?
    - Nouns that make sense from the perspective of an API consumer
    - Don't leak irrelevant implementation details
    - Keep naming consistent; probably best to use plural rather than singular
- Only nest resources if the sub-resource can only exist within the parent resource; otherwise, just make it a top-level resource
    - If commonly used, could offer functionality to automatically include the sub-resource in the parent (e.g. an `embed` query parameter)
- If actions don't fit into CRUD:
    - Restructure the action to appear like a field in a resource
    - Treat it like a sub-resource with RESTful principles
    - Roll with the verb
- Throw errors if people try to access without SSL, to force them to switch
- Documentation:
    - Should show examples of complete request/response cycles
    - Preferrable pastable (e.g. in the browser or on curl)
    - Should include deprecation schedules and notices, with updates publicized (e.g. blog, changelog, mailing list)
        - Do what's appropriate given the industry and consumers
- Versioning:
    - Always version
    - Probably best to use URL versions, with headers used to differentiate smaller updates
- Filtering, sorting, searching:
    - Use query parameters
    - Sort should allow for complex requirements by allowing for comma separated fields with possible unary negatives (+/-) for order
    - Consider packaging common uses of some conditions into an accessible RESTful path (e.g. sub-resource)
- Use `fields` parameter to filter which resource attributes are returned
- Updates and creation actions should return with the modified resource (with the right status code and maybe a Location header)
- Hyperlinked REST: maybe, but probably not necessary
- Just use JSON
    - Also for API input (require the `Content-Type` header to be `application/json` though)
- Snake case vs camel case: ¯|_(ツ)_/¯
- Pretty print and use gzip
- Don't envelope your actual payload with some silly `data` property
    - Only do it if you need to support JSONP or if a client can't work with HTTP headers
    - JSONP:
        - Always has a `callback` or `jsonp` query parameter in the request
        - Should always return 200 with the actual status and additional headers in the response
- Pagination:
    - Right way is to use a Link header
    - Custom HTTP headers may be useful for other information, e.g. `X-Total-Count`
- Never change data on the server for `GET` requests
- Use `X-HTTP-Method-Override` on `POST` requests if you need to support clients that only work with `GET`s and `POST`s
- Use 429 to indicate too many requests, but maybe include custom headers for useful information along the way (e.g. `X-Rate-Limit-Limit`, `X-Rate-Limit_Remaining`, `X-Rate-Limit-Reset`)
    - Use actual time remaining before the reset rather than a timestamp due to clock skews, etc.
- Authentication:
    - RESTful APIs should be stateless, so each request should come with authentication credentials rather than relying on sessions
    - Could keep it simple with a unique access token delivered in the user name field, otherwise OAuth is around
    - Also `access_token` parameters might be necessary for JSONP; this is insecure since most servers store query parameters in logs
- Caching:
    - Use Etag and `Last-Modified` headers
- Errors:
    - Should be no different than the respresentation of a resource
    - Use 4xx codes for client issues and 5xx for server issues
    - 4xx codes should always come with consumable JSON information, would be nice if 5xx did too
    - Errors should contain at least a useful message, a unique error code (found in the docs)
    - Validation errors should include a field breakdown of which ones failed and why (and return a 422 status)

### Who Will Command the Robot Armies

[Talk](http://idlewords.com/talks/robot_armies.htm)

- Interesting notes about the (desperate!) state of tech, surveillance, AI, IOT, and centralization

### Inside Amazon: Wrestling Big Ideas in a Bruising Workplace

[Article](http://www.nytimes.com/2015/08/16/technology/inside-amazon-wrestling-big-ideas-in-a-bruising-workplace.html)

- How crappy it is to work at Amazon

### Interviewing a Developer: Try the Project Walkthrough Technique

[Article](https://business.stackoverflow.com/blog/interviewing-a-developer-try-the-project-walkthrough-technique)

- "Red flags at this stage include difficulty or inability to back up design decisions, misunderstandings of overall architecture or subsystems, too fast-and-loose logical reasoning, and defensiveness when giving suggestions."

### The Code I'm Still Ashamed Of

[Article](https://medium.freecodecamp.com/the-code-im-still-ashamed-of-e4c021dff55e)

- "As developers, we are often one of the last lines of defense against potentially dangerous and unethical practices."

### The Broken Window Theory

[Article](https://blog.codinghorror.com/the-broken-window-theory/)

- "Neglect accelerates [software] rot faster than any other factor"
- "If a window in a building is broken and is left unrepaired, all the rest of the windows will soon be broken"
    - If no one cares, breaking more windows costs nothing

### How to Spread the Word About Your Code

[Article](https://hacks.mozilla.org/2013/05/how-to-spread-the-word-about-your-code/?utm_source=statuscode&utm_medium=email)

- Ready the project:
    - Good name, without innuendos (lol Testacular -> Karma)
    - Homepage, or url to go to
        - Use good titles, as you can't guarantee your evangelists will come up with good ones for you
    - Get on those docs, explain what your project does, and give a tutorial
    - Maybe write a blog post if you want to
    - Maybe record a screencast or gif
- Get the word out
    - Stagger it, so your site doesn't break on day 1
    - Go through social media first
    - Then influences and bloggers but make sure it's **quick** and isn't demanding
- User support
    - Respond to issues, etc
    - Create a dedicated account on Twitter, FB, etc.
    - Be careful about feedback; don't let critism get to you

### One Pull Request. One Concern.

[Article](https://medium.com/@fagnerbrack/one-pull-request-one-concern-e84a27dfe9f1#.q1nwp57h9)

- Also relevant: One commit one change
    - Success measured by "the ability to deliver value to the application" with a clear focus (e.g. legibility or change in a single interface)
    - Should suceed entirely or fail entirely; they should always leave the project in a valid state
- A pull request should contain one or more changes that form a high-level concern
- Atomic; success measured by the "ability to deliver the smallest possible piece of functionality"
    - Don't change things that are not concerned with the piece of functionality being addressed (e.g. renaming, formatting, etc)

### 10 tips for better Pull Requests

[Article](http://blog.ploeh.dk/2015/01/15/10-tips-for-better-pull-requests/)

- "The more you make your reviewer work, the greater the risk is that your Pull Request will be rejected."
1. Make it small
    - Focus on focus!
    - Time required to review is exponential to size
    - Rejects pull requests that are too big if submitted by professional (e.g. getting paid to code)
1. Do only one thing
    - Agreements for multiple concerns might not come so fast, so it's easier to submit multiple pull requests to let the ones with agreement pass through faster
1. Watch your line width
1. Avoid re-formatting
    - At best, do it in another pull request
1. Make sure the code builds (and has no warnings)
1. Make sure all teset pass
1. Add tests
1. Document your reasoning
    1. Self-documenting code
    1. Code comments
    1. Commit messages
    1. Pull request comments
1. Write well
1. Avoid thrashing
    - Don't add more commits to remove previous ones, just force push
    - Don't keep merging to stay current, rebase

### Why and how to make smaller pull requests

[Article](http://robertheaton.com/2015/10/26/why-and-how-to-make-smaller-pull-requests/)

- Nobody pays attention long enough to fully review long pull requests
- People are more likely to understand smaller pull requests
- Smaller pull requests are easier to test, deploy, rollback, and allow you to move faster since there'll be less interactions
- Aim for less complex (a proxy for this can be smaller lines changed depending on circumstance)
- Any work that takes more than a day or two may be too big
- If something probably could be its own pull request, it probably should

### Yeoman Pull Request Guidelines

[Article](http://yeoman.io/contributing/pull-request.html)

- Start by opening an issue first
- Only touch what's relevant for your issue
- Keep code clean
- Make sure tests run, and add more to test your changes
- Keep your commit history clean: one commit per feature
- "Code reviews are the best way to improve ourselves as engineers."

### How to write the perfect pull request

[Article](https://github.com/blog/1943-how-to-write-the-perfect-pull-request)

- Creating the pull request:
    - Provide an overview of why the work is taking place
    - Anybody in the world may be reading this Pull Request
    - Be explicit about what feedback you'd like (e.g. quick double check, design, writing)
    - Be explicit about when you'd like feedback
    - Directly mention people and teams you want to be involved
- Offering feedback:
    - Chill out and think things through before responding if you disagree strongly
    - Suggest changes with questions, rather than commanding them, and avoid hyperbole
    - Explain why you'd like it changed
    - **Be humble!**
    - Aim to develop professional skills
    - Try to use more positive language than neutral language ("if [online] content is neutral, we assume the tone is negative")
- Responding to feedback:
    - Consider leading with expression of appreciation
    - If you don't understand something, ask for clarification!
    - Offer clarification for your choices if you think something's been missed or mixed up
    - Respond to all the comments
    - Link to commits that fix some feedback
    - Might be good to take things offline if discussion is ongoing or confusing

### Thoughtbot's Guidelines for Code Review

[Article](https://github.com/thoughtbot/guides/tree/master/code-review)

- Avoid selective ownership of code
- Don't use sarcasm
- On getting reviewed:
    - "The review is of the code, not you"
    - Consider extracting some changes into other pull requests
    - Push commits for individual feedback, and link to those commits in the comments
- On reviewing code:
    - Offer alternatives and assume the author's already considered them. If the discussion gets too philosophical, let the author choose.
- If discussion turn too philosophical or academic, move the discussion offline to a regular team discussion

### On Empathy & Pull Requests

[Article](https://slack.engineering/on-empathy-pull-requests-979e4257d158#.r3qy9lwom)

- "Good code review culture is rooted in empathy for fellow engineers."
    - For both the author and the reviewers!
- Give context for your pull request
    - Your reviewer likely doesn't know everything you know (or think you know) about your changes and what you ran into while making your changes
    - Maybe highlight what didn't work, or some trade-offs considered
    - Ask for specific feedback if you're unsure of some things, and give context if some of the changes may be confusing
- "The more information you give your reviewer, the better they will be able to review your code for you"
- Reviewers should take responsibility for problems in code that they reviewed

### How About Code Reviews?

[Article](https://slack.engineering/how-about-code-reviews-2695fb10d034#.fovvabg35)

- Code reviews are also a chance to teach others, share knowledge, and learn
- Should not be rushed
- "Code reviews aren’t a distraction from your job: they are your job."
- Be confident; if you're not confident in a change, don't approve it!
- Don't be superficial, look for design issues, etc.
- Make sure you understand what you're reviewing!
- If you don't understand, pass off the review to someone else (and then follow up to learn)
- If the review becomes too much work, it's probably best to turn it into a 1-1 discussion
- "If you see a problem with the code, try to put yourself in their shoes and try to help them see the problem without making them feel like a screw-up."
    - Your co-workers are smart! Trust them, assume they know something you don't.

### The (written) unwritten guide to pull requests

[Article](http://blogs.atlassian.com/2016/07/written-unwritten-guide-pull-requests/)

- Ask: "how could I make it easier for the reviewer?"
    - Small pull requests
        - If the problem is complex, or becomes complex, break it down into smaller issues and make pull requests against those issues
        - Spend the time and effort to break down your pull requests, potentially time box your pull requests
    - Make it clear what you're doing
        - Good title
        - Group changes together into concepts or parts of the solution
        - Talk about what and why changed
        - Add comments to your changes for your reviewer
        - Add visual elements, like screenshots or architecture diagrams

### The Art of a Pull Request

[Article](https://www.elastic.co/blog/art-of-pull-request)

- Use a scheme to prioritize issues, from those that affect most users to those that should be closed because they're not relevant
- Reviewers:
    - Fully review code rather than "failing fast" to avoid going back and forth
    - Manually test the PR and try to break it
    - Check that the tests actually test anything
    - Hand it back to the author (e.g. re-assign them) to let them work on it
    - Hand it off to someone else to look at if you're the only reviewer and things look good

### H.264 is Magic

[Article](https://sidbala.com/h-264-is-magic/)

- "A simple uncompressed video file will contain an array of 2D buffers containing pixel data for each frame. So it's a 3D (2 spatial dimensions and 1 temporal) array of bytes. Each pixel takes 3 bytes to store - one byte each for the three primary colors (red, green and blue)."
- Lossy: "remove everything except the things that matter"
- Information entropy
    - "Information entropy is the [minimum] number of bits required to represent some information"
    - Lossless conversion between different representations (ideally in a more efficiently manner)
- Frequency domain
    - Transform a dataset into frequency coordinates (lossless if the frequencies are high enough)
    - Can mask out the edges of this representation and discard them to lose the finer details
    - **quantization**
- Eyes / brains are terrible at detecting colour variations
    - You can shed half of the colour information by using chroma subsampling
- Motion compensation
    - Split the image into blocks and encode them separately
    - Use a number of prediction schemes to keep blocks the same


Life
----

Email Etiquette: How to Ask People for Things and Actually Get a Response

[Article](https://zapier.com/blog/email_strategies/)

- Over 50% of email is read on a phone
- Most likely the first quick glance will determine whether or not they return to it later
- Put your ask at the top, ideally in the message preview; have the reader's attention and let them know what you want from them
- Establish credibility: make them care about you
- Make it clear what you'd like the next action to be (e.g. coffee break, call, etc)
- If asking a question, propose a solution too (to let them say "yes" or "no")
- Make the email scannable, e.g. using bullet points
- If it's urgent, give them a deadline
- Make your subject line catchy
- Preview your messages on your phone and edit

### Identity Based Habits

[Article](http://jamesclear.com/identity-based-habits)

- "The key to building lasting habits is focusing on creating a new identity first"
- Use identity-based goals instead of performance or appearance goals
- Your appearance and performance stem from your identity
- Changing your beliefs about your identity:
    1. Decide on the type of person you want to be
    1. Prove it to yourself with small wins
- Make sure to start with small goals and victories!! Make yourself believe you're the type of person who can achieve those things!

### The Difference Between Professionals and Amateurs

[Article](http://jamesclear.com/professionals-and-amateurs)

- Just showing up and doing the work everyday will make you better at literall anything
- Don't quit when it gets annoying or painful; stick to the schedule
- On becoming a pro:
    1. Decide what you want to be good at
    1. Set a schedule (but base it on actions rather than results!)
    1. Stick to your schedule

### How to start a company with no free time

[Article](https://medium.com/startup-grind/how-to-start-a-company-with-no-free-time-b70fbe7b918a)

- "It’s a VC’s job to meet lots of people and learn about what everyone’s workg on so they know what investments to make, but it’s a founder’s job to build their business"
- "As a founder, hiring is the best thing you can spend your time on."
- Make help actionable for others: "“give me feedback” isn’t actionable enough for most people"

### Surround Yourself with People Who Hold You to a Higher Standard than You Hold Yourself

[Article](https://medium.com/the-mission/surround-yourself-with-people-who-hold-you-to-a-higher-standard-than-you-hold-yourself-822fc429154f#.ilnedjfw5)

- Most people select their friends based on proximity
- Be careful about your "external locus of control": external factors that dictate the direction of your life
- "Most people are willing to tolerate unhealthy relationships, poor finances, and jobs they hate" -- don't be like that!
- "Most people are a direct reflection of those around them"

### Why Hiring is So Hard in Tech

[Article](https://medium.com/javascript-scene/why-hiring-is-so-hard-in-tech-c462c3230017#.sjj6bcxxy)

- "Great candidates highlight accomplishments & products they built. Mediocre candidates list a bunch of skill buzzwords with no supporting evidence."
- Prove that you're great, and back it up

### Assessing Employee Performance

[Article](https://medium.com/javascript-scene/assessing-employee-performance-1a8bdee45c1a#.eoya9bjgu)

- Ask (and listen!) to what your employee has contributed (and their evidence)
- "Your most productive employees are the ones who **help** all your other employees be more productive"
- The more experience your employee has, the longer you should allow for their contributions to be assessed (reaping the benefits of making others productive takes time!)
- Code is a **long term investment**
- "We don’t thk about how much money we add to the company’s bottom line” is god awful advice; your job is to increase your company's bottom line!
- "The best way to be a 10x developer is to help 5 other developers be 2x developers"
- Don't pay people to slow down the rest of your team by focusing on short term productivity; focus on long-term productivity and quality!
- "The worst thing you could do is show them that you don’t value them. The moment you do that, you’ve lost them."
- "Employees need to feel appreciated, valued, and productive. The best managers learn from their employees and mentor employees (in that order) to maximize the value they bring to the organization."
- "Learn to value the things you can’t track and count directly"; be data-driven, but also listen to your employees!
- "The best organizations build listening, learning, and mentorship deep into the company’s cultural DNA"

### The Engineer Crunch

[Article](http://blog.samaltman.com/the-engineer-crunch)

- Be generous with giving out equity for early hires
- Have a (geniune) mission (not about making $$$)
- If you have to hire outside your network, don't be constrained to your local talent pool

### A beginner's guide to funemployment

[Article](http://robertheaton.com/2014/06/02/a-beginners-guide-to-funemployment/)

- It's nice to take some long time off to do some personal stuff. Freeing.

### You aren't getting any better

[Article](http://robertheaton.com/2013/03/04/you-arent-getting-any-better/)

- **"You have to show up, work hard and deliberately focus on the specific things that will make you get better"**
- Make sure you get feedback on your work!
- **"Grok the fundamental principles that drive the guys who are the best in your game"**
- Focus on getting better over the long run: "make sure that you aren’t just rationalising being stuck in a crappy situation that is never going to get better"

### Keep Your Identity Small

[Article](http://www.paulgraham.com/identity.html)

- "I think what religion and politics have in common is that they become part of people's identity, and **people can never have a fruitful argument about something that's part of their identity**"
- "The more labels you have for yourself, the dumber they make you."

### Getting Nothing Done: a misguided quest for productivity

[Article](http://robertheaton.com/2014/07/14/getting-nothing-done-a-misguided-quest-for-productivity/)

- "If you are going to do job X, project Y and hobby Z then you might as well be methodical about them. But the structure you use should exist to support your life, not the other way around. You have to be very careful not to get so caught up in organising and collating all the things you care about that you forget to actually do any of them."

### Scientific Debugging

[Article](http://robertheaton.com/2015/03/29/scientific-debugging/)

- State hypothesis, assumptions, and beliefs about the system (and why it might not be working)
- Gather evidence around this hypothesis
- View your attempts as plausible guesses that need to be proved, rather than believing it right away
- Separates your opinion and reputation from a hypothesis that should be proven right or wrong

### Increase Your Productivity. Work in 45 minute blocks.

[Article](http://mattmccormick.ca/increase-your-productivity-work-in-45-minute-blocks/)

- "People can only focus on one thing for about 45 minutes"
- Break larger projects into 45min chunks; helps with feeling overwhelmed
- "Fatigue accumulates with astonishing rapidity"


Random
------

[Autocracy: Rules for Survival](http://www2.nybooks.com/daily/s3/nov/10/trump-election-autocracy-rules-for-survival.html)

- Interesting take on how the Trump victory might play out
