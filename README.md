# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** Raghuram Kadirabada  
**Student ID    :** [Your ID]  
**Date Submitted:** March 26, 2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

```
The fitness() function returns the total value of items in the knapsack if the total weight is within the 15 kg limit, otherwise it returns 0. An overweight solution scores 0 because exceeding the weight capacity violates the knapsack constraint and makes the solution invalid. This penalizes the algorithm for selecting too many items, forcing it to find valid packing combinations.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

```
tournament_select() randomly picks k individuals from the population and returns the one with the highest fitness score. Higher-fitness individuals are more likely to be chosen because they win more tournaments by definition—comparing fitness scores ensures better solutions are selected for breeding. This creates selection pressure that drives evolution toward better solutions.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

```
This line implements elitism—it copies the best solution found so far into the first position of the next generation. This is important because it guarantees the algorithm never loses the best solution through random mutation or crossover, preventing regression and ensuring the algorithm's convergence improves monotonically over time.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 | 60 |
| Final best value | 77 |
| Total weight of best solution (kg) | 14.4 |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
```
The curve shows rapid improvement in the first 10-15 generations, where the best value increases from 60 to 77. After this initial phase, the curve flattens out and remains stable at 77 for the remainder of the 50 generations. This indicates that the algorithm converged quickly to a good solution and then plateaued, unable to find better solutions despite continued evolution.
```

---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         | 75              | 14.9        | Yes    | Flattens early |
| 0.05         | 77              | 14.4        | Yes    | Rapid then stable |
| 0.30         | 78              | 14.1        | Yes    | Steady improvement |

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
```
With mutation_rate=0.01 (too low), the population loses diversity quickly and converges prematurely to an inferior solution (value 75). With mutation_rate=0.30 (too high), the algorithm maintains more exploration and finds a slightly better solution (value 78), but the curve shows less stable convergence. The mutation_rate=0.05 (balanced) provides good exploration-exploitation trade-off, achieving a strong final value of 77 with smooth convergence. The sweet spot appears to be around 0.05, where the mutation provides enough diversity to escape local optima without becoming random noise.
```

**Which mutation_rate gave the best result? Why do you think that is?**
```
The mutation_rate=0.30 gave the best result with a final value of 78. However, 0.05 is still reliable at 77. The higher mutation rate maintains more population diversity, allowing the algorithm to explore a wider solution space and discover better packing combinations. Even though higher mutation rates typically introduce more randomness, in this problem the additional exploration allowed the algorithm to find packing with a better value.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | The algorithm converges quickly to a good solution and stabilizes with balanced mutation rates. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | Higher mutation rates provide better exploration of the solution space, enabling discovery of higher-value packing combinations. |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
```
The most important thing I learned is that Genetic Algorithms require careful tuning of parameters to balance exploration and exploitation. The mutation rate is crucial—too low causes premature convergence to suboptimal solutions due to loss of population diversity, while too high can make the algorithm act like random search. The elitism strategy (keeping the best solution) is essential to prevent regression and guarantee monotonic improvement over generations. Finally, small parameter changes can have significant impacts on both the final solution quality and the convergence behavior, demonstrating that GA tuning is both an art and a science requiring empirical validation.
```

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, packing list pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
