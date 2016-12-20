Books
=====

### Extreme Programming Explained

1. What is XP?
    - The more humanly we treat myself and others, the more productive we all became
    - Use a "mentality of sufficiency"
    - You can do your best work even when there are constraints. Fussing about the constraints distracts you from your goals.
    - It's other peoples' job to manage their own expectations. Just communicate what you know to set that expectation.
1. Learning to Drive
    - Stay aware. Adapt. Change.
1. Values, Principles, and Practices
    - Practices: skill at normal activities; evidence of values
    - Values: intuition about what we like and don't like; brings purpose to practices
    - Principles: domain-specific guidelines; bridge gap between values and practices
1. Values
    - Difference between what we think is valuable and what is actually valuable creates **waste**
    - Most important: how individuals behave as part of a team and as part of an organization
    - Communication
        - Others probably already know the answer
        - Motion without communication is not progress
    - Simplicity
        - What is the simplest thing that **could possibly work**?
        - Simplicity only makes sense in context
    - Feedback
        - Use feedback to get closer and closer to our goals
        - Generate as much feedback as fast as possible
        - If team starts to ignore feedback, slow down
    - Courage
        - Effective action in the face of fear
        - Do the right thing, regardless of fear
    - Respect
        - Care about each other
    - Others
        - Could be: safety, security, predictability, quality-of-life
1. Principles
    - Should always be able to trace a path from the work done to a customer need
    - Humanity
        - Basic needs: safety, accomplishment, belonging, growth, intimacy
        - Balance personal needs with business needs
        - Trust goes a long way
    - Economics
        - Don't focus on a "technical success"; worry about the business
        - Generate money sooner, spend money later
        - Avoid investing in speculative flexibility
    - Mutal Benefit
        - All activities should strive to benefit everyone involved, including you in the future
        - Write tests, carefully refactor to reduce complexity, choose good names
    - Self Similarity
        - Copy structures that work in one area to others (e.g. apply TDD to an entire year, quarter, or week)
    - Improvement
        - Nothing is perfect, but it can always be improved
        - Do the best today, to improve tomorrow
        - Start right away and refine later
        - **Don't wait for perfection**
    - Diversity
        - Multiple ideas about a design present **opportunities**, not problems
        - Resolve conflicts productively
    - Reflection
        - Analyze how you succeeded or failed
        - Make sure reflection happens **after** action
    - Flow
        - Deliver value in small and frequent chunks
    - Opportunity
        - See problems as opportunities for change
    - Redundancy
        - Problems should be solved in multiple ways; cost of redundancy is cheaper than having a disaster
    - Failure
        - "If you're having trouble succeeding, fail"
        - Failure isn't wasteful as long as it imparts knowledge
        - **Fail, instead of talk**
    - Quality
        - "Projects don't go faster by accepting lower quality"
        - Pushing quality to be high often results in faster delivery too
        - People need to do work they're proud of
        - Use project scope for controlling a project's time and costs
    - Baby Steps
        - "Momentous change taken all at once is dangerous"
        - Take many small changes frequently
        - Overhead of small steps is smaller than aborting from a large change
    - Accepted Responsibility
        - Person directly invovled in the task should be responsible for it, from planning to practices used to testing
1. Practices
    - Practices are situation dependent; choose the best for yours
1. Primary Practices
    - Sit Together
        - Decrease barriers to open communication
        - "No matter what the client says the problem is, it is always a people problem"
    - Whole Team
        - Use whole, cross-functional teams
        - Find ways to fracture a big problem into smaller ones to use multiple smaller teams
    - Informative Workspace
        - Should be able to quickly and easily understand what a team is working through some visual means (e.g. cards on a wall)
    - Energized Work
        - Recognize when you've started being unproductive, or started removing value from your work
    - Pair Programming
        - Respect cultures and personal space, hygene, etc
        - "Ideally, emotions at work will be about work"
    - Stories
        - "Plan using units of customer-visible functionality"
        - Try to estimate the development effort of a story immediately
        - Balance cost of features with their value
        - Don't plan by focusing on appeal; focus on the cost and intended use first
    - Weekly Cycle
        - Start week by writing tests for features to be developed
        - Have deployable software by the end of each week
        - "Shifting the start of the [planning] cycle [to after Monday] makes sense as long as it doesn't put pressure on people to work over the weekend"
    - Quarterly Cycle
        - Focus on themes and the big picture
        - Good for team reflection on process bottlenecks, etc
    - Slack
        - Add minor tasks to planning that can be dropped if necessary so important commitments can be met
        - "Meeting commitments, even modest ones, eliminate waste"
    - Ten-Minute Build
    - Continuous Integration
        - Team programming is a "divide, conquer, and integration" problem
        - The longer you wait to integrate, the more risky, unpredictable, and time consuming it'll likely be
    - Test-First Programming
        - Avoids scope creep
        - Gives focus to the implementation
        - If it's hard to write a test, you likely have a design problem (usually a coupling issue)
    - Incremental Design
        - Common wisdom: cost changes to an existing system increases with time
            - May no longer be true; or there may exist areas where this is not true
            - XP's practices may lower the cost of changes over time
            - Introduce changes and implement at the *last* responsible moment
        - "The most effective time to design is in the light of experience"
1. Getting Started
    - "Change begins with awareness"
    - "Metrics can lead to awareness"
    - Change begins with yourself
1. Corollary Practices
    - Real Customer Involvement
        - Make (visionary) customers part of the team and planning
        - Build relationships and trust with customers with your transparency
    - Incremental Deployment
        - Make frequent, gradual replacements rather than singular, large ones (e.g. new systems, refactors) even if it means duplicating some services
        - Working harder to prepare for something means they'll also be less productive after
    - Team Continuity
        - "Keep effective teams together"
    - Shrinking Teams
        - Alow teams to shrink and reform into bigger teams by not overloading them with work
    - Root-Cause Analysis
        - Eliminate both a defect's symptoms as well as its cause; never make the same mistake twice
        - Add tests for the found defect
        - Five whys questioning (ask "why" five times on the cause) usually ends up with the root people problem
    - Shared Code
        - Anyone can improve any part of the system at any time
    - Code and Tests
        - Maintain only the code and the tests, generate other documents from these two
    - Single Code Base
        - Only keep one version of the code
        - Use configuration files / etc to maintain other necessary versions / builds
    - Daily Deployment
    - Negotiated Scope Contract
        - Signing a series of small contracts rather than a large one decreases scope and risk
    - Pay-Per-Use
        - Force users to pay to use the software each time
1. The Whole XP Team
    - Testers
        - Help define what the acceptable functionalities are before they're implemented
    - Interaction Designers
        - Work with customers to write stories
    - Architects
        - Look for large-scale refactors, write system-level tests
        - Keep complexity of architecture balanced with size and needs of project
    - Project Managers
        - Facilitate communication: internally, up and down, sideways, and externally
    - Product Managers
        - Picks stories and themes to work on
        - A plan is what *could* happen, not what *will* happen
        - Stories should be sequenced for business, not development reasons
        - A project should be demo-able (for the most basic of tasks) in the first week
    - Executives
        - Articulate and maintain long term goals
        - Health of XP teams:
            - Number of defects found after development
            - Time lag between initial investment and start of revenue
    - Technical Writers
        - Explains the features and creates closer relationships to the users
        - Track which parts of the documentation is actually used by users
    - Users
    - Programmers
        - Estimate tasks, break stories into tasks, write tests, write code, improve design
    - Human Resources
        - Evaluate employees based on the XP traits: acting respectfully, playing well with others, taking initiative, and delivering on promises
        - Could use team-based incentives and raises
        - Emphasis on hiring should be for teamwork and social skills
        - Interview: let candidates work with the team for a day, pair program
1. The Theory of Constraints
    - Theory of constraints: most systems' throughput are only constrained by one component
        - To improve, find this constraint and improve upon it
        - To find it, look for work piling up
    - Focus on overall throughput, not micro-optimization
    - The organization as a whole may change once the bottleneck shifts
1. Planning: Managing Scope
    - Make goals and direction clear and explicit, so as to align them with others
    - Analogy: grocery store
        - Time is like money; can only spend as much as you have available
        - Stories are groceries; their estimates are their costs
        - Need to prioritize your needs and wants
    - Estimates are uncertain; defer decisions to as late as possible to get the best info
    - Three variables to manage projects: price, speed, quality
        - Pick two and negotiate the third
        - However, price and speed are typically decided already, so you can only change quality
        - Lowering quality just leads to more work in the future; offloading responsibilities to someone else
    - Missing variable: scope
    - Acknowledge wishes, commit to needs
    - Get more perspectives on your stories by laying them out by different criteria (e.g. riskiness, estimates, feature / tuning, etc)
    - Estimate based on prior experience
        - Get feedback and reiterate estimates as fast as possible (e.g. split one month into four iterations, or one week into five iterations)
    - There is a real limit on how productive someone can be (creatively)
    - Adjust your plans as soon as you have information from previous sprints (to the extreme: only plan to do as much as you did last sprint)
    - If slipping in the middle of a sprint, try to realign with process changes (e.g. stopping work on less important issues) or communicate to customers what they'd like to have and replan
- Testing: Early, Often, and Automated
    - Defects destroy trust
    - Most defects are more expensive in the field than preventing them (in the long run)
    - The sooner you find a defect, the cheaper it is to fix
    - The more it costs to find and fix defects, the more defects will persist
    - Frequent tests means that the person making mistakes is also writing the test
    - The more stressed a team is, the more mistakes they make. However, with frequent testing, more stress results in more tests to verify behaviour
    - Write tests first:
        - Interfaces shouldn't be unduly dependent on the implementation
        - Tests provide certainty, as well as a measure of progress (i.e. making failing tests run)
1. Designing: The Value of Time
    - XP is based on incremental design; design should be done every day
    - Use prior experience to get to the next stage, while the software is still running
    - Design just enough to get feedback, then improve the design with that feedback
    - Real constraints on a design should become obvious after implementation; go after those in the next iteration
    - "Design quality doesn't ensure success, but design failure can ensure failure"
    - Can design by instinct, thought, or experience; if you don't need to spend more effort on the design, you can go with the lowest effort approach
    - Design heuristic: "Once and Only Once"
        - Data, structure, and logic should only exist in one place
    - When confronted wtih a mess, improve only the pieces that affect you today
    - Balance design with needs and relationships; delivery of functionality is what others want, design is not
    - Simplicity of a design:
        - Appropriate for the intended audience: should be understandable by those who need to work with it
        - Communicative: the system's components should be clear to future readers
        - Factored: little to no duplication of logic or structure
        - Minimal: system should be as small as possible
1. Scaling XP
    - Number of people
        - Factor large teams into smaller teams that work on smaller problems
        - Initially solve a small problem with a small team and then add more teams, making sure to integrate frequently ("conquer-and-divide")
    - Size of organization
        - Make sure to maintain communication with others (in a format they're used to)
    - Complexity
        - Continue to delivery, but gradually reduce the complexity
    - Even security audits should be done frequently and gradually
1. Interview (with a manager using XP)
    - Train one team, get them to master it, and then let that team teach another team
1. Creation Story
    - Consultant's job: find the person who has the knowledge (of the problem) and convey that knowledge to the person with power
1. Taylorism and Software
    - When picking a name, it helps if the opposite of the name is unappealing
    - Micro-optimization doesn't always lead to macro-optimization
    - Separating quality from engineering allows engineering to defer quality responsibilities to another department
1. Toyota Production System
    - "If you eliminate enough waste, soon you go faster than the people who are just trying to go fast"
    - Make the quality of the production line good enough that you don't need to check quality later
    - Using a part immediately (from another producer) gives you information about whether that producer is functioning correctly
    - "The greatest waste is the waste of overproduction"
        - E.g. large requirements documents, elaborate architectures, stale code, stale documentation
1. Applying XP
    - "The waste [in software development] is rooted more in what we believe and feel than in what we do"
    - "Adopting" a process doesn't solve your problems; you solve your problems by tackling them with the help of the process
    - Start changes with yourself, lead by example
    - Only when you know how to improve, do you improve
    - Practices that work for one team might not work for another; some practices contain hidden dependencies or a team might not be ready for them
    - Conditions that can facilitate change:
        - Aligned values: people are willing to accept the changes
        - Pain: recent pain makes everybody more willing!
1. Purity
    - Saying your process is "x" sets other people's expectations of how to communicate and work with you
1. The Timeless Way of Programming
    - Keep in mind the needs of users, sponsors, but also developers
    - Focus on integrity, balance, and harmony; hold yourself to high quality standards
    - Believe in your process and try to make deep changes

### Planning Extreme Programming

- Foreword
    - What matters is building the **right** product **fast**
    - Invest in people so they can work quickly and effectively without formal process
- Preface
    - "Planning is not about predicting the future"
    - Development may not go as according to plan, but without a plan it will go awry
    - "Keep the human beings focused, happy, and motivated and they will deliver"
1. Why Plan?
    - Business and software changes too quickly for plans to be able to perfectly predict the future
    - "Plans are about figuring out a likely course of events and the consequences of the inevitable changes"
    - "The more obvious it is that you should do something, the more important it is to ask why"
    - Before planning, figure out why you think you should be doing this task (and how you can measure its success)
    - Planning is useful because:
        - We need to be doing the most important things
        - We need to coordinate with others
        - We need to understand the consequences on the first two when unexpected events derail our plans
    - In the face of unexpected events, make sure to adjust our plan and coordinate with others
    - Coordination requires that you know where you are in your own plan
        - Set up clear milestones that anyone, including the customer, can understand and trust
    - Don't plan to control events; you can only control your reaction to events
    - Don't pretend that a plan is on-track when it's not; this is only trying to turn reality into an illusion (requiring more effort and inflecting more pain later)
    - "If things seem to be going exactly according to plan, that's usually a sign of trouble"; **expect plans to change**
1. Fear
    - To develop effectively, we must acknowledge our fears of things going wrong
    - "Unacknowledged fear is the source of all software project failures"
        - Don't build useless political structures and processes aimed at protecting yourself (and then hide behind them)
        - Aim to work with each other and help out as needed (including customers)
1. Driving Software
    - "Driving [software] is about making lots of little course corrections"
    - "We are trying to maximize the benefit of a process," not trying to hit a target
    - Continually assess your direction frequently, compare it to your ideal direction, and course correct
    - "If you get lost driving, it isn't the car's fault, it's the driver's"
1. Balancing Power
    - Balance software decisions against business decisions
        - The business people should be making business decisions
            - Deadlines
            - Feature scope
            - Feature priority
        - The technical people should be making technical decisions
            - Development estimates
    - Create a set of rules that encourage technical people to make technical decisions and business people to make business decisions
        - Have a customer, represented by one voice (e.g. the product manager), that is **a part of the team**
        - A good customer (representative):
            - Understands both the domain and how it works
            - Understands how software can help in the domain
            - Delivers value regularly, bearing on the side of too little than nothing
            - Makes decisions about what's needed **now** and what's needed **later**
            - Accepts ultimate responsibility of the project's success or failure
            - Asks, at all times, "What is the most valuable functionality to have next?"
    - **Never slip a deadline!** (It's a slippery slope)
        - Always provide a little functionality each release, and release to real customers as often as possible
1. Overviews
    - Recognize that there are two cycles to accomodate and synchronize: the business cycle and development cycle
    - Any activity that goes between the engineering of a release and then delivering it represents a risk, so each development iteration should result in a production-ready system
    - The business side determines the most valuable tasks to work on at the start of an development iteration
    - Small iterations mitigates implementation risk by allowing plans to be affected as quickly and as visibly as possible if something goes wrong
1. Too Much To Do
    - When you're overloaded, give yourself less things to do (rather than trying to get more time, which is impossible)
    - "We always ate Korean; it seems to be good for the brain"
    - Not having enough time breeds hopelessness, which in turn, breeds frustration mistakes, burnout, and failure
    - Having too much to do breeds hope, we can:
        - Prioritize what to do
        - Reduce the scope of some tasks
        - Delegate tasks to someone else
1. Four Variables
    - Interrelated variables for projects (changing one affects the rest):
        - Cost
        - Quality
        - Time
        - Scope
    - Delayed reaction after moving one variable
    - Cost
        - People: non-linear effect and long delay
            - Brook's Law: "Adding people to a late project just makes it later"
        - Tools: some delays
        - Don't be afraid to spend money to keep motivation up; well-motivated people are well worth it!
        - Try your best to keep overtime low, **make** your employees do something else if you have to!
            - Results in lack of motivation, bugs, mistakes, etc
    - Quality
        - External: how the customer perceives the product
        - Internal: the quality of the system's internals
            - **Dangerous**: don't let this drop; you might get a small increase in speed at first but it'll come back as a huge decrease later
            - "Nothing kills speed more effectively than poor internal quality"
        - Push non-functional requirements (e.g. performance, aesthetics) to scope
    - Time and Scope
        - Scope is easy to increase without realizing the ramifications while time is hard to see
        - "Every time you add scope, you [should] immediately see the effects on time"
        - Short iterations force you to reconcile the consequences of changing scope with time
    - Usually best to assume cost and quality and fixed levers
    - Planning should:
        - Preserve developers' confidence in completing the plan
        - Preserve customers' confidence in getting value
        - Be as efficient as possible
    - Each iteration has stories, costs of the stories (their estimates), a budget (in time), and constraints (business constraints)
        - Costs on stories can go up or down depending on their actual complexity, and stories may have to be delayed to meet the budget (but never modify the budget!)
1. Yesterday's Weather
    - Assume you'll do as much this week as you did last week
        - Avoids habitually overestimating a team's abilities
        - Forces teams to focus on finishing at least some features rather than having them all "in progress"; imagine telling a customer they can have 0 features next week
    - If you commit to too much, everyone will know the plan is doomed and will do everything they can to protect themselves and hide their failing schedules
1. Scoping a Project
    - First estimate coarsely, to get a feel for the project
        - Does it make any sense (in regards of time, scope, quality, and cost)?
        - It's OK to guess, and leave lots of padding
    - To make the initial estimate:
        1. Break the project into smaller pieces
        1. Estimate each piece (don't get too into the details!)
        1. Defer less valuable pieces
    - Make sure to separate actual business functionality from "context" items (e.g. performance, aesthetics, reliability)
    - Turn generic ideals about the product (e.g. "easy to use") into actual functionality (e.g. "personal profiles")
    - You don't have to accomplish everything in this first plan, **priorities and requested features will change!**
    - "A pep talk is no substitute for a plan that everyone believes in"
1. Release Planning
    - Synchronize the date and the scope of the project with the business (may be external factors, e.g. run way)
    - Allocates user stories to releases (and development iterations)
    - Effort between the customer and the developers; customer drives and developers help navigate (business prioritizes, technical gives estimates and technical risks)
    - Does not need to be stable; it's just a snapshot of of the current view on what is (and should be) being built
    - The further ahead the plan, the less accurate it will be, so plan only a few iterations and releases ahead
    - Evolve the infrastructure as you build functionality, not ahead
    - Use past performance ("velocity") to determine how much you can do
1. Writing Stories
    - "A user story is a chunk of functionality that is of **value** to the customer"
    - Emphasis on the **simple** and **providing value**
    - Make them understandable to the customer (the end ones)
    - Should be short, and act as a contract for the developers to talk to the customer during implementation
        - Only add more details when you actually need them (usually when you start implementing)
    - A few stories should be implementable in an iteration, otherwise they're too large
    - Developers should **not** be writing stories (though they may suggest them); the responsibility lies solely on the customer
        - Customers write the stories, developers estimate them
        - Estimate sooner than later; this allows you to refine stories so that they become estimatable (e.g. turning "make it easier" into "make it easy to start the process," etc)
    - Stories should be independent, should be able to be completed in any order
    - Stories should be testable (and an implementation is only complete when it successfully passes this test); automated is better
    - Avoid lumping too many things in a story: not only is it not simple or clear, it bundles different stories' priorities together when they may be separate
        - When a split is needed, split tasks along priorities; the customer should drive this
        - Developers and the customer should iterate on this, to make sure the stories written by the customer are small enough and estimatable
    - Exploratory programming is sometimes a good way to investigate and come up with an estimate
    - "Writing stories is not the point. Communication is the point."
    - Start developing when the most important stories have been identified and enough work is available for several months (so the custom can make choices)
1. Estimation
    - Use a comparable you've previously done
    - Keep it simple
    - Use what happened in the past
    - Learn from experience
    - The team should estimate, and favour optimistic estimates during disputes (to avoid the team from getting too optimistic; those who get burned by optimisim will probably learn)
    - "Estimates are not commitments"
    - Don't predict the effect of external influences (e.g. changing team size), measure it and react accordingly
    - Instead of worrying about short term data fluctuations in real, calendar time, use ideal time (assumed 100% productive) to estimate tasks
    - Encourage better estimates, and make sure to record your actuals!
1. Ordering the Stories
    - Do the stories that have the highest business value first!
    - Don't worry too much about technical dependencies
    - Focus on minimum technical commitment for stories
    - "Most ordering dependencies are false"; you probably only *think* you need them when you actually don't
    - Don't look for dependencies to order things, **look for business value**!
        - Business value is determined by the business guys
    - Even if you can't release, people are happy if you've done the most important things first since it looks like you're listening and incorporating their feedback
    - Technical risk: "When developers feel nervous [after thinking about a story], everyone should listen"
        - "Programmers want to do higher risk stories first"
    - The programmer should make the risk visible, and the business side should factor this in to their ordering of items
        - Keeping technical commitment low should prohibit risk from impacting too much
    - "Not all usable behaviour has to be usable by the user [at first]... the key criteria is that it is testable"
1. Release Planning Events
    - Requirement creep is OK since you're iteratively defining the requirements (rather than all up front)
    - Build a new plan when:
        - You have too many deferred items
        - Your development velocity changes
    - To rebuild:
        1. Re-estimate stories (you have more experience now than before)
        1. Re-prioritize and pick items for release
    - Should be done every 3-4 iterations
1. The First Plan
    - "The first plan... is always high on expectations and usually low on delivery"
    - Guessing velocity:
        - Measure progress while writing and estimating first stories
    - Story estimating:
        - Start with the ones you're most comfortable with estimating first
        - Use data from other teams, but don't get attached to comparing your results with theirs
    - Iteration length:
        - 2 - 3 weeks generally
    - Getting development started
        - Mob program for a bit to evolve the design and begin initial implementation
        - Get some zero functionality tasks (e.g. infrastructure) ready
1. Release Planning Variations
    - Shorter releases: every iteration (or story) becomes a release
        - May result in optimizing short term features over long term ones
    - Longer releases
        - First, question if you really, really can't make it shorter
        - Create internal releases that are shorter
    - Smaller stories
        - Divide stories up; offers finer control for more cognitive load and lower flexibility
1. Iteration Planning
    - The iteration plan is the developers': they decide how to do things and in what order
    - Break down stories into tasks, have developers sign up for tasks, and then estimate
    - Report progress mid-iteration to adjust scope and get a sense for what will actually happen
    - Deal with dependencies inside the iterations!
    - **Never slip release dates**; defer functionality (let the customer choose what he cannot live without)
    - Let the customer decide if a release date can be moved back
    - Timeboxing is not about time; it's about functionality trade-offs
1. Iteration Planning Meeting
    - Summarize stories to get everyone empathetically on the same page
    - Break down stories into tasks each taking a few days
        - You never plan exactly when these tasks will be finished; dependencies will usually sort themselves out (or people will)
        - Write tests for the tasks
        - Try not to set priority of tasks solely by technical reasons (slippery slope)
    - Absolute values of velocity =/= productivity; it's more useful as a predictive tool
    - Don't use other people's work to estimate your tasks
    - Tasks are only complete when tests are written and passing
    - Let customers remove stories and functionality when you come up short on capacity
    - The sum of tasks is more granular than their parent story's estimate; they provide better (and more accurate) information
1. Tracking an Iteration
    - A designated person should ask each developer how many days they've spent on a task and how many days are left
    - If the actual and estimated (to finish) days left aren't similar, adjustment might be necessary
    - If someone reports not being able to spend as much ideal time working on their tasks as usual, maybe they need some help (with e.g. clearing something up, getting familiar, etc)
    - Let the customer decide when a task is complete (if possible)
        - **Known bugs are the customer's choice to accept**
    - Let customers demo the features (if the developers don't mind); this ensures the customer knows what's going on
    - If you know you probably can't finish something, let others know (they might be able to take over that part or help significantly)
        - If the team absolutely can't handle it, the customer needs to descope
    - Don't use overtime to catch up on a release
1. Stand-up Meetings
    - Let everyone know what's going on, and what's not
    - What you did yesterday, what you'll do today, problems, annoucements
    - **Communicate problems, not solve them**
1. Visible Graphs
    - "You can't manage what you can't measure" -- Denning
    - Don't let the measurements become the ends (keep them as means!)
    - Use intuition:
        - Smell a problem
        - Devise a measurement
        - Display measurement
        - If it doesn't go away, keep devising measurements
    - "Many an insight comes when idly staring at a graph when you're half doing something else"
1. Dealing with Bugs
    - There will always be defects
    - Remove the emotion; consider changes to be enhancements
    - Customer decides if time should be used towards fixing bugs vs new features (business decision: cost of bug vs value of feature or earlier deployment)
    - Treat the defect as a story if it's big
    - Prioritize small bugs before iteration planning
    - Rotate some development members to production support
    - Customer makes the call on what's a critical bug that has to be fixed now
1. Changes to the team
    - Scale teams by dividing by half after ~10 people
    - Could try putting management tasks for each iteration to give visibility and maybe let others try
1. Tools
    - **"Communication is more important to success than whizbang"**
    - Problems in project management:
        - Tracking data
        - Maintaining communication
    - Keeping everyone honest is usually the most difficult problem
    - Everyone understanding the current state of development is better than keeping whatever tool you're using current
1. Business Contracts
    - Don't put the interests of the supplier against those of the customer (work together instead)
    - Outsourcing: try to let the scope be visible (and adjusted) within quick iteration cycles (e.g. by applying this book)
    - In-house: find a good customer who can speak for business
        - If you have a committee of customers, make sure their individual goals are aligned
    - If you have a number of product managers, make sure they reconcile their priorities and present themselves as one voice to development
1. Red Flags
    - "Slow down until you're under control, then speed up again"
    - Missing estimates
        - Don't guilt trip yourself into overestimating
        - Iterations should be finishing comfortably
        - Make better estimates (and by adjusting with prior work)
    - Customers won't make decisions
        - Find a better customer, or reassure them that the process is iterative and they can fix any mistakes later
    - Defect reports
        - Slow down and fix defects until you stop seeing them (or see less of them)
    - Not going end to end
        - Don't stop developing if you get uncomfortable; do your job
    - Failing builds
        - Make your production environment similar to your test environment
    - Customer won't finish
        - Make better release plans that are visible by upper management
1. Your Own Process
    - Start by trying the whole system (synergies), and then adjust with time through each iteration by experimenting


### Investment Biker

> "If you’ve got a dream, you have to try it; you must get it out of your system. You will never get another chance.
  If you want to change your life, do it"
