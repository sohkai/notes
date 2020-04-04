August 2016
===========

Tech
----

### A Guide to Python's Magic Methods

[Article](http://www.rafekettler.com/magicmethods.html)

- `__init__` defines the initialization behaviour of an object, **but** it is not the first thing called (that's `__new__`)
- `__new__` is the class constructor, passing the new class to `__init__` for initialization; mostly useful if subclassing immutable type
- `__del__` is the class destructor, when the object is garbage collected (for objects that require extra cleanup after deletion); **not** reliable if the interpreter exits so good cleanup practices are still required
- `__cmp__` is the basic c comparison (negative result means it's less, etc; only in Python2)
- `__eq__`, `__ne__`, `__lt__`, `__gt__`, `__le__`, `__ge__` define behaviour for their operators
- `functool`'s `@total_ordering` automates defining comparison methods
- Unary operators: `__pos__`, `__neg__`, `__abs__`, `__invert__`, `__round__`, `__floor__`, `__ceil__`, `__trunc__`
- Arithmetic operators: `__add__`, `__sub__`, `__mul__`, `__floordiv__` (`//`), `__div__` (`/`; only in Python2), `__truediv__`, `__mod__`, `__divmod__`, `__pow__` (`**`), `__lshift__`, `__rshift__`, `__and__`, `__or__`, `__xor__`
- Reflective arithmetic operators (object as second argument to operator): just append `r` to the arithmetic operators; usually can just call their normal operator
- Augmented assignment (operator + assignment operation): just append `i` tot he arithmetic operators
- Type conversion: `__int__`, `__long__`, `__float__`, `__complex__`, `__oct__`, `__hex__`, `__index__` (when object is used in a slice operation), `__trunc__`, `__coerce__` (only in Python2)
- Class representations:
    - `__str__` (for humans, defaults to `__repr__`)
    - `__repr__` (for use in code and interpreters
    - `__unicode__` (doesn't work when `str()` is used on class; only in Python2)
    - `__format__` (for use in `str.format()`)
    - `__hash__` (for use with `hash()`; usually for dicts along with `__eq__`)
    - `__nonzero__` (for `bool()`; renamed to `__bool__` in Python3)
    - `__dir__` (should return list of attributes for the user; usually unnecessary)
    - `__sizeof__`
- Controlling attribute access
    - Encapsulation in Python comes through "magic", rather than explicit modifiers
    - `__getattr__` is called when a nonexistsent attribute is accessed; can be used for misspellings, deprecated attributes, or raising `AttributeError`s
    - `__setattr__` allows you to define custom rules for any changes in the values of attributes
    - `__delattr__` is similar to `__setattr__` but for deleting attributes
    - `__getattribute__` is similar to `__setattr__` but for getting attributes. Only works with new style classes, but can be tricky to implement
    - Implementing these can be tricky and can easily lead to infinite recursion
- Custom sequences
    - Immutable containers only need `__len__` and `__getitem__` defined
    - Mutable containers require `__setitem__` and `__delitem__` as well
    - Iterable containers require `__iter__`
    - Others: `__reversed__`, `__contains__`, `__missing__` (only for subclasses of dict)
- Reflection: `__instancecheck__`, `__subclasscheck__`
- Callable objects: `__call__` allows classes to be callable (as if they were functions!)
- Context managers: `__enter__`, `__exit__`
- Descriptors: `__get__`, `__set__`, `__delete__`
- Copying: `__copy__`, `__deepcopy__`
- Pickling: `__getinitargs__` (only for old style classes in Python2), `__getnewargs__`, `__setstate__`, `__reduce__`

### Dirty Tricks From the Dark Corners of Front-End

[Presentation](https://speakerdeck.com/smashingmag/dirty-tricks-from-the-dark-corners-of-front-end)

- Nesting anchors can require `<object>` tags around the nested anchor (browser short circuits on nested anchors)
- Can use `<object type="image/svg+xml" data="image.svg">` for SVGs
- `:before` and `:after` works (sometimes) with `<img>` elements
- CSS `calc()` is amazing
    - Calculate font-sizes with vw and vh to create fluid font-sizes based on viewport size
        - Also for line heights
    - Calculate column widths and then apply `min-width` or `max-width`
    - Calculate the necessary overflow padding from a container (e.g. if you want a child element to be full width when nested in a container with margin)
- Make sure your emails are bulletproof (test with images turned off!)
- Use progressive scans of images
- Use `table-layout:fixed` to fix the layout of the table based on the first row
- Transitions don't work on `min-height`
- Can override platform-specific emoji designs by using your own fonts that override the Unicode code points
- With HTTP2, multi-stage CSS loading removes the need for critical CSS
- `<img>` tags can use a `object-fit` CSS property to be similar to `background-size: contain` and etc
- CSS `currentColor` represents the calculated value of the element's `color` property
- CSS `contain` allows you to define priorities for loading and painting CSS

### Writing Idiomatic Python 3

[Book](https://jeffknupp.com/writing-idiomatic-python-ebook/)

- When checking `if` on a variable multiple times, use an iterable: `if x in (1, 2, 3):`
- Dict comprehensions also exist
- So do set comprehensions
- Sets have overloaded operators: `A | B` == union; `A & B` == intersect; `A - B` == difference; `A ^ B`: symmetric difference
- For longer lists, use a generator expression instead of a list comprehension to save memory
- Use `sys.exit()` in CLI scripts to return error codes; 0 means everything went well
    - The code after your `if __name__ == '__main__':` should only ever be `sys.exit(main())`
- Don't use relative imports
- Use the `os.path` module for file system paths

### Hitchhiker's Guide to Python

[Book](http://docs.python-guide.org/en/latest/)

- Use decorators
- Use context managers
- Most basic types (and tuples) are immutable; this includes strings
- To concat a number of strings, list comprehension into array and then `"".join(list)`
- Pythonic style:
    - Use keyword arguments generously to aid meaning
    - Don't change how core Python works unless you absolutely need to (e.g. object creation, imports, etc)
    - Put error checking returns at the top
    - Preferable to keep a single exit point
    - Use variable unpacking
    - Use `__` as an ignored variable when unpacking (to avoid clashes with `_`)
    - Length-N list of the same thing: `val = [None] * 5`
    - Length-N list of lists: `val = [[] for __ in range(4)]` (`xrange was renamed to `range` in Python 3)
    - Python's `set`s (and `dict`s) are hashtables; lookup using `in` is much more efficient than in a `list`
    - Use `in` or a default argument to `dict.get()` instead of `dict.has_key()`
    - Use `enumerate` to get the list index while using `for in`
    - Use parenthesed around multi-line statements to let the interpreter join the lines until the parentheses are closed
- Numeric zeroes, empty sequences, empty dicts, and objects whose defined `__bool__()` or `__len__()` methods return falsey values
- Use `not` instead of `!` to revert logic
- Documentation
    - Use docstrings
    - Do not use trip-quote strings for block-level comments
- Logging
    - The user should dictate what happens when a logging event occurs, not the library
    - Instatiate loggers in a library by only using the `__name__` variable; this ensures no name collisions
- Gotchas
    - Default arguments are created once during function definition, **AND CAN BE MUTATED**
        - Use a default argument to signal that no argument was provided to create a new object instead
        - Can be useful as a way to define static variables (i.e. to cache state between calls)
    - Closures are late binding; they only look up enclosed variables when the closure is actually invoked
        - Mostly felt when looping to create unique functions
        - Instead, bind a local variable or default parameter to the indended enclosed variable
    - `.pyc` files are automatically generated and should be ignored from version control
        - Use `PYTHONDONTWRITEBYTECODE=1` to disable this behaviour
    - Not supplying a license: "In the US, if no license is specified, users have no legal right to download, modify, or distribute."
- Web scraping
    - Use `lxml` to parse XML and HTML
- Performance
    - CPython is slow
    - The GIL (Global Interpreter Lock) prevents multi-threaded Python; necessary as CPython's memory management is not thread-safe
        - Maximizing performance requires a strong understanding of the GIL
        - Running another Python instance in another process does not run into this limitation (see `ThreadPoolExecutor` and `ProcessPoolExecutor`

### Intro to cron

[Article](http://www.unixgeeks.org/security/newbie/unix/cron-1.html)

- Format: `min hr dom month dow cmd`
- `crontab -e` loads your crontab file in your `$EDITOR`

### Asynchronous Tasks With Django and Celery

[Article](https://realpython.com/blog/python/asynchronous-tasks-with-django-and-celery/)

- `pip freeze > requirements.txt` is pretty rad

### The Most Diabolical Python Antipattern

[Article](https://realpython.com/blog/python/the-most-diabolical-python-antipattern/)

- Never `except Exception` and pass, as it hides all errors
- At the least, log the exception and its stack trace
- Only silently pass specific exception classes that you know about in advance

### Beyond PEP 8 -- Best practices for beautiful intelligible code

[Video](https://www.youtube.com/watch?v=wf-BqAjZb8M)

- **Make sure your code isn't beautiful but bad!**
- **Don't let PEP8 / etc cloud your vision (look for Pythonic vs Non-Pythonic instead); pay attention to things that really matter!**
- **Use adapter patterns to wrap bad packages with good interfaces!**
- Prefer Python's context managers for setup / cleanup code (e.g. `__enter__`, `__exit__`)
- Use Python's property descriptors rather than getters / setters
- Use iterables when you have iterables
- Avoid unnecessary packaging
- Use magic methods (e.g. `__len__`, `__getitem__`)
- Use `__repr__`
- Wrap bad exceptions with good ones

### Transforming Code into Beautiful, Idiomatic Python

[Video](https://www.youtube.com/watch?v=OSGv2VnC0go)

- Stop thinking in indicies
- Use `enumerate` to get foreach indicies
- Use `izip` to loop over multiple collections (iterator'd `zip`) and dict creation out of two lists
- Better performance: make sure your code is running in L1 cache!
- Use `key` functions to sort, instead of comparision functions
- `iter`'s second parameter is a sentinel value
- `for-else` exists
- Use `dict.keys()` to iterate over a dict if you'll be mutating it
- Use `dict.iterItems()` for an iterable over the dict
- Use `defaultdict` for dictionaries with defaults (needs to be converted back to a dict sometimes)
- Use `namedtuple`s!
- "Don't break atoms of thought into subatomic particles"

### Stop Writing Classes

[Video](https://www.youtube.com/watch?v=o9pEzgHorH0)

- Prefer easy things over complicated things
- "I hate code and I want as little of it as possible in our product"
- Ship **features** not code
- If you think you need it later, **do it later**
- Namespaces are not for creating taxonomies; use them to prevent name collisions

### Credentials: A Retrospective of Mild Successes and Dramatic Failures

[Article](http://manu.sporny.org/2015/credentials-retrospective/)

- Interesting retrospective on current and past identity schemes
- Sets out a number of criteria to judge strength identity schemes

### The case for setImmediate()

[Article](https://www.nczonline.net/blog/2013/07/09/the-case-for-setimmediate/)

- Modern `setImmediate()`s have a 4ms timer; using 0, 1, 2, 3, or 4 mean the same thing
- `requestAnimationFrame()` is more useful for animations; it requests a new UI update after the current one
- `setImmediate()` inserts the task after the last paint event in the current event loop
- Node has `process.nextTick()` as a similar API
- Polyfills needed for use

### Telehash

[Website](http://telehash.org/)

- Secure (full end-to-end encryption), mesh networking protocol
- Mesh: encrypted sessions (links) between any two endpoints

### Pure UI

[Article](http://rauchg.com/2015/pure-ui/)

- **UI as a pure function of application state**
- "When the magnitude of the undertaking is not clear for the developer or designer, let alone for the people removed from the creation process, it’s simply impossible to make any accurate predictions."
- Break designs into their smallest possible variations and implement against those
- **"A distinction of two very distinct (yet frequently interleaved) phases of the creation process: design and discovery"**
- Design, discover all possible variations, design, rediscover, etc.
- **"Applications must handle different states that are difficult to replicate under normal testing conditions."**

### Always on top in MacOS Yosemite

[Article](http://www.perfectlyrandom.org/2015/01/31/always-on-top-in-macos-yosemite/)

- Keeping random GUI windows afloat (i.e. always on top) on OSX is possible

### Hall of api shame: boolean trap

[Article](https://ariya.io/2011/08/hall-of-api-shame-boolean-trap)

- Don't add boolean parameters
- Prefer obvious, keyword, or human-readable arguments instead

### Fuzz testing

[Article](https://en.wikipedia.org/wiki/Fuzz_testing)

- Chaos testing
- Most common for file formats, network protocols
- Most useful when testing input that crosses a trust protocol (i.e. user-generated content)

### Falsehoods Programmers Believe About Names

[Article](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/)

- Long list of wrong myths about people and their names


Life
----

### Warren Buffett’s “2 List” Strategy: How to Maximize Your Focus and Master Your Priorities

[Article](http://jamesclear.com/buffett-focus)

1. Write down your top 25 career goals
1. Circle the top 5 goals
1. Eliminate the rest. **"Everything you didn’t circle just became your Avoid-At-All-Cost list. No matter what, these things get no attention from you until you’ve succeeded with your top 5.”**

### How to be More Productive and Eliminate Time Wasting Activities by Using the “Eisenhower Box”

[Article](http://jamesclear.com/eisenhower-box)

- **Immediately do** urgent and important tasks
- **Schedule for later** important but not urgent tasks
- **Delegate** urgent but not important tasks
- **Eliminate** neither urgent nor important tasks

### How to Stop Procrastinating by Using the “2-Minute Rule”

[Article](http://jamesclear.com/how-to-stop-procrastinating)

- Do anything that only takes two minutes **immediately**
- Any new habit should be started within two minutes, let **momentum** carry you to do it further

### How to Solve Difficult Problems by Using the Inversion Technique

[Article](http://jamesclear.com/inversion)

- Look at a problem and think about the exactly opposite of what you want to achieve
- E.g. Instead of how to be a better manager, ask what would a terrible manager do?
- **"It is far easier to avoid stupidity than it is to create genius."**

### Mental Models: How Intelligent People Solve Unsolvable Problems

[Article](http://jamesclear.com/feynman-mental-models)

- **"Point of View is worth 80 IQ points"**
- Develop multiple perspectives to look at a problem, and select the best for the problem at hand
- Developing perspectives:
    - Read and do things outside of the norm
    - Link separate, seemingly disparate ideas with others

### First Principles: Elon Musk and Bill Thurston on the Power of Thinking for Yourself

[Article](http://jamesclear.com/first-principles)

- Think from first principles, not analogies
- Build up from fundamental, hard facts to solve problems

### Be Coachable

[Article](http://sockpuppet.org/blog/2015/08/21/be-coachable/)

- **“If you don’t fall, you’re not trying hard enough.”**

### The Science of Speaking is the Art of Being Heard

[Article](http://firstround.com/review/the-science-of-speaking-is-the-art-of-being-heard/)

- Amygdala rewiring === rewiring fight, flight, or freeze instinct
- Goal is to remove differences as much as possible to make the listener feel comfortable to be engaged
- **Goal of management is a high performing team, focused on outputs, which can only be coordinated by communication**
- **Meta models for effective communication**
    - *Toward vs. Away*: Optimist vs pessimest
        - Toward: motivated to attain goals, **use words like "gain", "obtain", "achieve", ...**
        - Away: motivated to solve problems, **use words like "avoid", "exclude", ...**
        - **Frame actions as either moving away from something or towards another**
    - *Internal-referencing vs External-referencing*: Internal vs external motivators
        - Internal: decisions are based on their own self, **use language like "you decide", "what do you think"**
        - External: seek external information and feedback from others, **use language like "feedback", "approval", "others..."**
        - **How do you know you've done a good job at x**
    - *Specific vs General*: Details vs overview
        - Specific: operate with details, **use words like "exactly", "precisely"**
        - General: focus on overview, **use language like "essentially", "generally"**
    - *See, Heard, Read, Do*: Vector of convincing and persuasion
        - See: influenced by what they perceive **(55%)**
        - Hear: influenced by what they hear **(30%)**
        - Do: influenced by past and current action **(12%)**
        - Read: influenced by what they read **(3%)**
        - **How do you know that someone else is good at their job?**

### Interviewing to Hire Trailblazers, Nonconformists and Originals

[Article](http://firstround.com/review/adam-grant-on-interviewing-to-hire-trailblazers-nonconformists-and-originals/)

- "You want people who choose to follow because they genuinely believe in ideas, not because they’re afraid to be punished if they don’t."
- Seeds a resilient culture
- Hire as many originals as possible
- Look for:
    - Unsung heroes
    - Insubordinates
    - Inward-facing innovators
- Interviewing:
    - Do they default to challenging? Can they challenge the quo?
    - **"Why shouldn't I hire you?"**
- **“Originals are constructive contrarians. They're not just pointing out that the emperor has no clothes; they're also tailors.”**
- Look for diversity, curiosity
- Find out what they've tried but given up; "their roads not taken"
- Force references to be candid: make them choose between two seemingly undesirable choices

### The ‘Adaptable Leader’ is the New Holy Grail — Become One, Hire One

[Article](http://firstround.com/review/the-adaptable-leader-is-the-new-holy-grail-become-one-hire-one/)

- Constant learners can adjust to any new environment or role quickly
- **"When you boil it down, learning is about changing your mind"**
- **Gamer**: Take risks, be optimistic, keep trying
    - Clarity of objectives empowers individuals to be resourceful
    - **"How would we approach this if it were a game?"**
    - "The gameful leader expects adversity, but remains excited about solving the puzzle."
- **Beginner**: Be childlike and curious
    - Ask "why not" and "what if"
    - Reason from first principles
    - Take "yourself out of autopilot to shift into awe, curiosity, and wonder"
    - **"What would I think about this if I had no biases, or if I had never seen a situation like this before?"**
    - “What do I believe that the rest of the world doesn’t?”
    - "Create an inner alarm to sound the moment you have the thought: ‘Of course, this the way to do it!’ Silence it by stepping back and reassessing the situation."
    - "The only way to avoid bias and to stay open to the possibilities of learning, is vigilance."
    - **"Value asking questions and people who ask questions"**
    - "What have you learned in this conversation?"
- **Growth**: Your performance is always a reflection of your current self, which will grow in the future
    - Relish in taking on challenges
    - Possess a self-motivated passion for learning; always be in self-improvement and self-actualization mode
    - "Doing the right thing is more important than doing things right."
    - **Premature perfectionism is the root of all evil. Get the feedback you need immediately.**
- Be around constant learners, always look to hire constant learners
- References: ‘Please call me back if this is an outstanding candidate for a job that requires learning.’
- **"Hire people for the way they approach problems."**
- Make it clear to new team members you believe they'll make a difference and will get to grow a lot
- Help new team members set goals so they can experience wins early on and constantly
- **"We’re not knowledge workers. We’re learning workers."**

### This 90-Day Plan Turns Engineers into Remarkable Managers

[Article](http://firstround.com/review/this-90-day-plan-turns-engineers-into-remarkable-managers/)

- Put away the pencil to write code
- 0-30: Educate
- 31-60: Find rhythm and style
- 61-90: Assess this is a good fit for you
- Management is in all three directions: above, beside, and below
- **"You no longer ride on the rollercoaster. But you operate it."**
- Manage only if that's what you want, if you can channel empathy, and if you can give trust
- Figure out which are the important meetings, and cancel others
- Build an event loop / pipeline for the current day, week, month, quarter
- If this isn't for you, it's OK to step down after trying it!

### Don't Call Yourself A Programmer, And Other Career Advice

[Article](http://www.kalzumeus.com/2011/10/28/dont-call-yourself-a-programmer/)

- **"Engineers are hired to create business value, not to program things"**
- **"Nobody ever outsources Profit Centers"**
- **Describe your accomplishments by increasing revenues or decreasing costs**
- **Strive to help people**
- **Most important professional skill is communication**
- **"Modesty is not a career-enhancing character trait"**

### Salary Negotiation: Make More Money, Be More Valued

[Article](http://www.kalzumeus.com/2012/01/23/salary-negotiation/)

- **Salary negotiations are important**
- **"Rich, successful people negotiate**
- Start salary negotiations after all interviews and a fit looks possible
- **Never give up your number first**; use any number of excuses
- Repeat other people's words back to them for convincing; take notes!
- Stress "we" or "you" benefits
- Use things other than the salary to negotiate
- Use some new information to convince others you're valuable

### The Hiring Post

[Article](http://sockpuppet.org/blog/2015/03/06/the-hiring-post/)

- Interviewing is a terrible medium for hiring
- Interviews are hostile environments for candidates
- Interviews are biased twoards candidates who are good at interviews
- Ideas:
    1. Warm up candidates. Welcome them with an initial call. Send them material to review.
    1. Build a standardized interviewing format for every interviewer to follow. **Interviewers should hate it!** Use a script.
    1. Make sure the standardized format generates data, and is testable.
        - Strip existing systems and let the candidate build part of it back up
        - Collect objective facts for causation metrics (when looking back)
        - Score candiates using the same rubric
        - Remove tests that don't predict well
        - Avoid pressured situations
    1. Checklist:
        - Is it consistent? Does every candidate get the same interview?
        - Does it correct for hostility and pressure? Does it factor in “confidence” and “passion”? If so, are you sure you want to do that?
        - Does it generate data beyond hire/no-hire? How are you collecting and comparing it? Are you learning both from your successes and failures?
        - Does it make candidates demonstrate the work you do? Imagine your candidate is a “natural” who has never done the work, but has a preternatural aptitude for it. Could you hire that person, or would you miss them because they have the wrong kind of Github profile?
        - Are candidates prepped fully? Does the onus for showing the candidate in their best light fall on you, or the candidate?

Random
------

### The Raspberry Pi Has Revolutionized Emulation

[Article](https://blog.codinghorror.com/the-raspberry-pi-has-revolutionized-emulation/)

- RP3 has wifi!!!
- Cool available starter packs

### WELCOME TO AIRSPACE

[Article](http://www.theverge.com/2016/8/3/12325104/airbnb-aesthetic-global-minimalism-startup-gentrification)

- Design is becoming homogenized across the world, **digital globalization (of taste)** is somewhat of an apt description (or at least, a cause)
- Tasteful, but generic and empty; made to make changing places as frictionless as possible
- An anchoring to a recognizable home in an unfamiliar environment
- **Placelessness** and **digital nomads** are starting to become themes
- **The gentrification of taste**; **depersonalization** and the loss of identity
- **"AESTHETIC HOMOGENEITY IS A PRODUCT THAT USERS ARE COMING TO DEMAND"**
- **URBAN AREAS AROUND THE WORLD MIGHT INCREASINGLY RESEMBLE EACH OTHER AND BECOME INTERCHANGEABLE**
