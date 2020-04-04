March 2020
==========

Tech
----

### The Monitoring Death Spiral

[Article](https://grafana.com/blog/2016/01/11/the-monitoring-death-spiral/)

- Rather than blindingly trusting instinct, intuition, or a single instrument, get the full picture
- Observability practically means we bring telemetry data together under a seamless experience to help people troubleshoot, understand, and explore the data that is coming out at an increasingly rapid rate from all systems and application

### Monitoring for Everybody

[Video](https://grafana.com/blog/2018/05/23/monitoring-for-everyone/)

- Good introduction to logging, metrics, and tracing, and when each should be applied

### An Inside Look at the Life of a Technical Writer at Grafana Labs

[Article](https://grafana.com/blog/2020/02/20/an-inside-look-at-the-life-of-a-technical-writer-at-grafana-labs/)

- Technical content should be separated into:
  - Concept
  - Task
  - Reference

### Shitty First Software Drafts

[Article](https://sirupsen.com/drafts/)

- Simplify, simplify, and then simplify
- "If you can't rewrite what you did in an hour, it wasn't simple enough"

### Research Debt

[Article](https://distill.pub/2017/research-debt/)

- Research can have debt similar to technical or institutional debt
- Research debt is the accumulation of missing interpretive labor

### Up and Down the Ladder of Abstraction

[Article](http://worrydream.com/LadderOfAbstraction/)

- Ladder of abstraction: technique for explicitly defining and navigating the different levels of abstraction available
- As an engineer, you should not be doing something if you don't know what you're supposed to do
- "The most exciting engineering challenges lie on the boundary of theory and the unknown"
  - Emergent behaviour: "high-level effects that arise indirectly from low-level interactions"
  - Challenge lies not in constructing the system, but understanding it
- Design which parameters should be controllable
  - Do not be a slave to real time! Design tools that will allow you to skip forward, backward, or play in loops and reverse!
- Abstract over a parameter (e.g. time) to visualize it against other parameters: first layer up
  - It will be useful to view these abstraction as "layers" that we can also apply as we go down the ladder (e.g. visualizing path over time, but still seeing position at a specific moment in time)
- As you abstract over more parameters, you step higher up the ladder. Once you do this, it's useful to take these into mind and "layer" over previous steps to examine and compare specific cases
- At some point, you will have to abstract over the data that the system works over (e.g. all possible input variations)

### The Best Advice We Overheard at First Round's CTO Unconference

[Article](https://firstround.com/review/the-best-advice-we-overheard-at-first-rounds-cto-unconference/)

- "Debate, decide and persuade"
  - Every pending decision will be in one of in one of these modes (early, middle, or late); be clear with the team on where a particular decision is in this cycle

### Track and Facilitate Your Engineers’ Flow States In This Simple Way

[Article](https://firstround.com/review/track-and-facilitate-your-engineers-flow-states-in-this-simple-way/)

- Interesting article on managing flow states of managees

Life
----

### User and player types in gamified systems

[Article](https://yukaichou.com/gamification-study/user-types-gamified-systems/)

- Bartle's four player archetypes in games:
  - Achievers (diamonds): obtain success or rewards, even if they don't translate to gameplay advantages
  - Explorers (spades): focus on discovery; want to dig and uncover new pathways or treasure
  - Socializers (hearts): social elements and building relationships are most interesting
  - Killers (clubs): compete and beat others
- Gamified systems do not have as much freedom to explore or play
- Andrzej's archetypes in gamified systems:
  - Player (only one "willing" to play): reacts to extrinsic rewards
  - Socializer: social and relatedness
  - Free Spirit: autonomy, self expression
  - Achiever: mastery
  - Philanthropist: purpose, selfless dedication for a "cause"
- Quadrants according to acting (vs. interacting) and system (vs. user) (all intrinsically motivated):
  - Achievers: acting, system
  - Free spirits: interacting, system
  - Philanthropist: acting, user
  - Socializer: interacting, user
- Quadrants according to material desires and amount of structure (all extrinsically motivated):
  - Consumer: acting, system
  - Exploiter: interacting, user
  - Self seeker: acting, user
  - Networker: interacting, user
- **Design around the four intrinsic motivations, and then build rewards on top; it be self-sustainable even without the rewards**

### Gamifying Corporate Politics: Chou’s Corporate Player Types

[Article](https://yukaichou.com/workplace-gamification/gamifying-company-politics-chous-corporate-matrix/)

- Quadrants according to performance and political ability:
  - Survivors: lowest effort to stay alive ("NPC"s, "losers" in Gervais Principle)
  - Performers: passionate, don't care about politics ("clueless" in Gervais Principle)
  - Politicians: just want to get ahead via politics (wannabe "sociopaths" in Gervais Principle)
  - Stars: sociopaths
- Motivational design moves survivors into performers
  - Epic meaning, development and creativity, coaching
- Leadership training moves performers into stars
- Rewarding politicians, while easy, destroys the company ("the dark side"); others will see that as the path and lose motivation / increase scheming

### Warning: This Is Not Your Grandfather’s Talent Planning

[Article](https://firstround.com/review/warning-this-is-not-your-grandfathers-talent-planning/)

- **Superstar mode**: the people on your team who are going to change everything; responsible for Schumpeterian change; a force — and source — of growth on a team.
  - Continue offering them challenges
- **Rock star mode**: the people on your team who don’t want their boss’ job; very talented at their role and will keep doing and digging into it for years if a boss doesn’t screw it up; a force — and source — of excellence and stability on a team.
- "People in superstar mode want a world they can change. Those in rock star mode seek a world they can stabilize. You’ll need both."
- Be care with overvaluing _potential_--your rock stars are not going to be directing their energy for upwards mobility
  - Look instead for _growth trajectory_
