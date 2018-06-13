Books 2018
==========

### Freakonomics

Author: Stephen J. Dubner, Steven Levitt

- Chaos theory applied to economics; hunt for data rather than "logical" / "rational" / emotional explanations to phenomenon

### Think Like a Freak

Author: Stephen J. Dubner, Steven Levitt

- Rethink your solution, restate your problems :)

### The Cathedral and the Bazaar

[Book](http://www.catb.org/esr/writings/cathedral-bazaar/)

- Cathedral: "carefully crafted by individual wizards or small bands of mages working in splendid isolation"
- Bazaar: "release early and often, delegate everything you can, be open to the point of promiscuity"
- Key lessons:
    - "Every good work of software starts by scratching a developer's personal itch"
    - **"Good programmers know what to write. Great ones know what to rewrite (and reuse)"**
        - Constructive laziness
    - "Plan to throw one away; you will, anyhow" -- Fred Brooks
        - You probably don't understand the problem until after the first implementation
        - Be ready to start over, at least once
    - "When you lose interest in a program, your last duty to it is to hand it off to a competent successor"
    - "Treating your users as co-developers is your least-hassle route to rapid code improvement and effective debugging"
    - "Release early. Release often. And listen to your customers"
    - Optimize for the minimum-effort path from point A to point B
    - Linus's Law: "Given enough eyeballs, all bugs are shallow"
        - Finding and solving a problem is necessarily done by the same person
        - The **Delphi effect** (the crowd is smarter than the individual) applied to debugging
        - "Debugging is parallelizable"; debugging doesn't require that much coordination between people and thus has less fall off in Brook's Law
        - Non-developer sourced bugs usually lack a lot of context that make debugging easier
        - Open source makes it easier for tester (/ user) and developers to share context
        - Brook's Law is based on development groups communicating in complete-graph patterns, but open-source projects separate the work of external contributors to parallelizable subtasks
    - "Smart data structures and dumb code works a lot better than the other way around"
    - "If you treat your beta-testers as if they're your most valuable resource, they will respond by becoming your most valuable resource"
    - "The next best thing to having good ideas is recognizing good ideas from your users. Sometimes the latter is better"
    - "Often, the most striking and innovative solutions come from realizing that your concept of the problem was wrong"
        - Reframe the problem! Your users will tell you :)
        - Open source parallelizes exploration of the design space
    - "When your code is getting both better and simpler, that is when you know it's right"
    - **Any tool should be useful in the expected way, but a truly great tool lends itself to uses you never expected"**
    - "When writing gateway software of any kind, take pains to disturb the data stream as little as possible—and never throw away information unless the recipient forces you to!"
    - "When your language is nowhere near Turing-complete, syntactic sugar can be your friend"
    - **"A security system is only as secure as its secret. Beware of pseudo-secrets."**
    - "To solve an interesting problem, start by finding a problem that is interesting to you"
    - "Provided the development coordinator has a communications medium at least as good as the Internet, and knows how to lead without coercion, many heads are inevitably better than one"
- Necessary preconditions for bootstrapping a community:
    - Runnable
    - Convince others it has potential to grow into something really useful
- **"While coding remains an essentially solitary activity, the really great hacks come from harnessing the attention and brainpower of entire communities"**
- **[Open source acts like a free-market, aligning a community of individuals' free wills with collective "principles of understanding"](http://www.catb.org/esr/writings/cathedral-bazaar/cathedral-bazaar/ar01s11.html)**
- "Feeling comforted by having somebody to sue would be missing the point. You didn't want to be in a lawsuit; you wanted working software."
    - Utility function for hackers is ego satisfaction and reputation
    - Altruism is a form of ego satisfaction for the altruist
- Boring tasks / problems in open software:
    - **You don't need "motivation" (by whip and cash) to get people incentivized to solve these problems; somebody will choose to solve it because they have a fascination with the problem itself**
- **"Play is the most economically efficient mode of creative work"**
- Open source ownership is similar to Lockean, common-law theory of land tenure
- Gift vs exchange economy
    - Exchange: social status primarily determined by what you have to use or trade
    - Gift: social status primarily determined by what you give away
    - Is open source more of a gift economy; the only measure of competitive success is the reputation among one's peers
        - Optimizing reputation incentives?
        - Is this the globally optimal way to cooperate for generating high-quality creative work?
        - Creative work may be demotivated by scarcity rewards (assuming nobody is worried of dying from scarcity); better to recognize and value output than to expect
    - For most, the exchange game has lost its appeal but not ability to constrain
- "Authority follows responsibility"
- Conflict resolution
    1. Territorial rule
    1. Seniority / Most invested wins
- Against tragedy of the commons in open source (inverse commons):
    - Using software does not decrease its value; widespread use tends to increase its value
    - People need solutions _on time_, so they if they derive value from fixing it, they'd rather fix it than be a free rider and wait
        - Also, they're incentivized to publish any patch to alleviate further maintainence themselves
    - Free-rider problems are exhibited mainly in friction costs of submitting patches
        - **Make submission easy and simple!**
- Use-value funding models
    - Cost-sharing (e.g. Apache web server)
    - Risk-spreading (e.g. software that might outlive someone's employment)
- The right to fork software is like the right to sue: nobody wants to employ them, but it's a signal of danger if they're taken away
- "When your key business processes are executed by opaque blocks of bits that you can't even see inside (let alone modify) you have lost control of your business"
- Rebranding free software to open source:
    - Free Software Foundation was damaging: "free" is really confusing because it can denote both "free speech" and "free beer"
    - Top-down > bottom-up: furthering the OS movement required evangelizing to CEO/CTO/CIO types
    - Focus on Fortune 500: lots of concentrated money that's relatively accessible
        - Capture the media that serves the Fortune 500
    - Make sure the hacker community was aligned in speaking the same language
    - Mitigate serious abuse of the language by corporates
- "Open source is [great, but it's] not magic pixie dust" -- JAmie Zawinski
- **"Computers are tools for human beings. Ultimately, therefore, the challenges of designing hardware and software must come back to designing for human beings"**
