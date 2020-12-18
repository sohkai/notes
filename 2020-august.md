August 2020
===========

Tech
----

### Exploring Bayesian Optimization

[Article](https://distill.pub/2020/bayesian-optimization/)

- Active learning: estimate an accurate model
  1. Start with prior function (can assume uniform)
  2. Evaluate point with greatest uncertainty (usually highest variance and furthest away from last evaluated point)
  3. Go back to 1 until model is accurate enough or budget runs out
- Bayesian optimization: find global optimization
  1. Start with prior function (can assume uniform)
  2. Evaluate next point by optimizing an _acquisition function_ around our current knowledge
    - Probability of improvement
    - Expected improvement
- Based on prior knowledge, where should we evaluate next?
  - Active: most uncertain
  - Bayesian: balance between uncertain and current optimums
