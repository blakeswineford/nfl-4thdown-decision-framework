# 🏈 NFL 4th Down Expected Points Model

> Data-driven decision support for 4th-down plays — no vibes, just math.

## 📋 Overview

This project builds a two-model decision engine that evaluates NFL 4th-down decisions by comparing:

-   Field goal attempt
-   Going for it

It uses historical play-by-play data from 2018–2024 to estimate:

-   $P(FG)$: Probability of making a field goal
-   $P(Go)$: Probability of converting on 4th down
-   Expected Points (EP) for each choice
    -   $EP(FG) = 3 \times P(FG)$
    -   $EP(Go) = 6.94 \times P(Go)$ (6.94 = league-average drive value after a successful conversion)

Whichever has higher EP is the recommended decision.

## ⚙️ Features

### Field Goal Model

-   Distance, indoor/outdoor roof, surface type
-   Kicker profiles (career by distance, overall accuracy, recent form)
-   Game context (time, score, home/away, pressure state)
-   Opponent defensive context (EPA allowed, red-zone stop rate)

### Go-for-it Model

-   Yards to go, field position, score/time
-   Offense strength, opponent defense
-   Short-yardage and goal-line flags
-   Team “go tendency” and 4th-down history

**Outputs:** Clean per-play tables with `qtr`, `time`, `situation`, `FG_dist`, `P(FG)`, `P(Go)`, `EP(FG)`, `EP(Go)`, and `actual result`.

## Performance (in-sample)

-   **FG model:** `Brier = 0.080`, `AUC = 0.943`
-   **Go model:** `Brier = 0.055`, `AUC = 0.948`
