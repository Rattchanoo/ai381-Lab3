# Model selection

Fill this in after you have trained your candidates in MLflow. Short sentences are fine. Use numbers from your runs.

## The question
This model decides whether a customer will churn or stay, and a false negative hurts retention efforts by failing to identify a departing user.

## Candidates
| Candidate | Why I tried it | AUC | F1 | F1 per slice (lowest) | p95 latency (ms) | Size (KB) | MLflow run ID |
|---|---|---|---|---|---|---|---|
| logreg | Baseline linear model for binary classification | 0.781 | 0.495 | 0.420 | 3.5 | 12.4 | cdaebc12483b41dd84a7338fa3f948d0 |
| random_forest | Non-linear ensemble model for complex interactions | 0.776 | 0.482 | 0.405 | 18.2 | 1420 | bb31df6ab796488d8e58e3a020a5e4a1 |
| gradient_boosting | Sequential boosting ensemble for enhanced prediction | 0.774 | 0.479 | 0.400 | 22.5 | 850 | 5c33a0587827493180d2158b8e066a56 |

## The champion
I picked logreg because it achieved the highest AUC (0.781) and best F1 score while strictly meeting the latency budget with an exceptionally fast p95 latency of 3.5 ms and a tiny footprint of 12.4 KB. I accepted a minor loss in complex tree-based non-linear boundary fitting in favour of speed and stability.

## My promotion rules
- Latency budget (p95): 50 ms, because real-time inference requires fast response times.
- Minimum gain to replace the champion (F1 points): 0.01, because simpler models are favoured unless complexity provides a substantial performance boost.

## What I would check next
One thing that could make this choice wrong in production is data drift over time or shifts in minority customer behaviours and segments.
