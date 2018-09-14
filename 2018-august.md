August 2018
===========

Tech
----

### Augur hijack via dormant service workers

[Article](https://medium.com/@peter_szilagyi/augur-hijack-via-dormant-service-workers-bea254258f98)

- "From a technical perspective, the reason the exploit can be considered of a significant impact is because it **doesn’t require elevated permissions** to run, after running a single time it **remains dormant forever** in the user’s system and it’s a **fully legitimate browser functionality**, so no exploit detection software can ever catch it."
- Avoid running apps from `localhost`, due to `origin` clashes (`localhost` is typically treated special to make it easier for development)

### How to Hire World Class Engineers

[Article](https://angel.co/talent-hacks/how-to-hire-world-class-engineers)

- What engineers are looking for (beyond compensation):
  - Opportunity
  - Challenge
  - Community
- Steps:
  1. Build brand
    - Make your org more desirable
    - Document and promote your org's mission, culture, and philosophy so that others can rally behind it
      - Easiest is to start with what you're specializing in, and why that's interesting
    - Don't be sloppy
  1. Always be sourcing
  1. Screen at scale
    - Screen after spending some time with the candidate
    - Questions:
      - "Why are you taking the time for me today?"
      - "What's your proudest achievement?"
      - "What's a recent find (blog post, github repo, etc) you recommend we check out?"
  1. Interview effectively
    - Pair program with an actual engineer on real problems
    - Use a recent problem you've had to solve, and re-solve it with them
  1. Close quickly
    - Discuss and negotiate compensation openly
    - Stay responsive in your communication
    - Showcase your own passion

### Real Work vs. Imaginary Work

[Article](https://m.signalvnoise.com/real-work-vs-imaginary-work-8bdb84a7d1da)

- "Thinking about how you’re going to do something is not the same as rolling up your sleeves and trying."
- Test out ideas by writing real code, to hit the unknowns before declaring something as "downhill"

### How To Write Fast, Memory-Efficient JavaScript

[Article](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)

- V8
  - **Base compiler**: parses JS and generates machine code
  - V8 represents code in an internal type system optimized for lookups
  - **Runtime profiler** identifies "hot" functions that then gets optimized by the **optimizing compiler**
  - **Deoptimization**: backs out of optimizing code that the optimizer realizes it made bad assumptions about
- Avoid using `delete` to dereference: it changes an object's hidden class
  - Especially hot objects that get used a lot!
- Be careful when using timers; they're kept alive (to continue executing) and may leak state
- Use `DocumentFragment`s to avoid page reflows


Life
----


Random
------
