# Reliability simulation exercises

Simulation exercises for **PSYC 201A** (UC San Diego), accompanying the
measurement chapter of [Experimentology](https://experimentology.io/) (Ch. 8).
You will simulate the same people taking the same measure twice and use the
simulations to see what test-retest reliability is and what drives it. When you
are done you will have:

- Simulated a second "session" for each participant and computed test-retest
  reliability with `cor.test()`
- Plotted reliability two ways: a scatterplot, and one line per person across
  sessions (`pivot_longer()` + `geom_line()`)
- Written a function that simulates reliability, then run it hundreds of times
  to see how between-person spread and session-to-session noise change it
- Seen why a bigger sample doesn't make a measure more reliable, and why a
  restricted range makes it look less reliable
- (Bonus) Used Spearman-Brown to predict what averaging more ratings buys you

The running example is the tea ratings from the inference simulations: the
same people rate the tea again, and nobody gives exactly the same rating twice.

> **Before you start:** finish
> [getting-started-with-r](https://github.com/psyc-201/getting-started-with-r)
> and [the inference simulations](https://github.com/psyc-201/inference_simulations_lab_2).
> This lab needs only the tidyverse, nothing else.

---

## Part 1. Make your own copy

Same steps as in getting-started-with-r:

1. At the top of [this repository's GitHub page](https://github.com/psyc-201/reliability_simulation_exercises),
   click the green **Use this template** button, then **Create a new repository**.
2. Owner: **your own account**. Name it `reliability_simulation_exercises`, leave
   it **Public**, and click **Create repository**.
3. On *your* copy, click **Code** → **Open with GitHub Desktop** → **Clone**.

Step-by-step version:
[github-desktop.md](https://github.com/psyc-201/getting-started-with-r/blob/main/docs/github-desktop.md).

## Part 2. Open the project

**Double-click `reliability_simulation_exercises.Rproj`** to open RStudio inside
the project, then open `ch8_reliability_simulations.qmd` from the Files pane
and put your name in the `author:` line.

## Part 3. Work through the lab

Run one chunk at a time with the green arrow, top to bottom. Later chunks use
objects that you create earlier (`tea_data`, `tea_retest`, `tea_retest_long`),
so if you skip one, the chunks after it fail. Fill in each `___`.

| Part | What you do |
|---|---|
| 1. Simulate the first experiment | Make tea ratings for 120 people, each with a `sub_num` so you can follow them |
| 2. Simulate the retest | Give each person their own random change between sessions with `rowwise()` and `sample()` |
| 3. Plot it and compute reliability | Scatterplot of session 1 vs. session 2, `cor.test()`, an inline-R sentence, and reliability within each condition |
| 4. Follow each person | `pivot_longer()`, then one line per participant across sessions |
| 5. What makes reliability go up or down? | Write `simulate_reliability()`, run it across between-person spread, retest noise, and sample size, and plot the results |
| 6. Restricted range | Keep only high scorers and watch reliability drop |
| Bonus | Predict reliability with more ratings per person (Spearman-Brown) |

`error: true` is set at the top of the file, so **Render works even while
chunks are unfinished**: the unfinished chunks show their error in red.

`ch8_reliability_simulations_solutions.qmd` is the answer key. Try each part
first.

## Part 4. Commit, push, and submit

Commit as you go. When you are finished, render once more, commit with a
message like `Finish reliability lab`, **Push origin**, and submit the link to
your repository however your instructor asks. Rendered `.html` files are
ignored by git, so only your `.qmd` is pushed.

## What is in this repository

```
reliability_simulation_exercises/
├── reliability_simulation_exercises.Rproj     open this to start work
├── ch8_reliability_simulations.qmd            the exercises
└── ch8_reliability_simulations_solutions.qmd  answer key
```

There is no `data/` folder: you make all the data yourself.

## Stuck?

1. **Setup errors** (package not found, RStudio not in the project): see
   [troubleshooting.md](https://github.com/psyc-201/getting-started-with-r/blob/main/docs/troubleshooting.md).
2. **Everyone got the same `difference`:** you called `sample()` inside
   `mutate()` without `rowwise()` first, so it drew one number for the whole
   column. Add `rowwise()` before that `mutate()` and `ungroup()` after.
3. **`object 'tea_retest' not found`** (or `tea_data`, `tea_retest_long`):
   the lab asks you to create that object in an earlier chunk. Fill in its
   blanks, then rerun from there.
4. **Your numbers differ from the solutions:** expected, unless you render from
   scratch. Every rerun of a chunk draws new random numbers.
5. **The simulations in Part 5 take a few seconds.** Let them finish.
6. Still stuck? Post the **exact** error message in the course forum.

## Resources

- [Experimentology, Ch. 8: Measurement](https://experimentology.io/): the course textbook
- [R for Data Science (2e)](https://r4ds.hadley.nz/): the tidyverse, chapter by chapter
- [Quarto: using R](https://quarto.org/docs/computations/r.html)
