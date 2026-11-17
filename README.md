# Classification: When 90% Accurate Is Worthless

## Objective
I wanted to show why accuracy is a poor measure when one class is rare, and to choose a decision threshold based on the cost of each type of error instead.

## Methodology
- I worked with 6,000 simulated loan applications with a default rate of 9.6%. On this data, a rule that approves everyone is 90.4% accurate.
- I fitted a logistic regression and evaluated it at the usual 0.5 threshold.
- I read the coefficients as log-odds and as odds ratios, and showed that one odds ratio (1.63 for one more prior default) means different changes in probability at different starting points.
- I traced precision and recall across six thresholds.
- I chose a threshold by minimising the expected cost of false positives and false negatives, and compared it with the closed-form threshold.
- I wrote a small function, `precision_recall_at()`, that returns a classifier's precision and recall at any threshold.

## Key Findings
- At the 0.5 threshold, the logistic regression was 90.4% accurate and predicted 0 defaults. This is the same accuracy as approving everyone.
- The same odds ratio of 1.63 per prior default changes the probability of default by different amounts depending on where the applicant starts.
- The cost-minimising threshold was 0.121. The closed-form threshold was 0.118.
- Expected cost was 944 per applicant at the cost-minimising threshold, against 1,147 at 0.5.
- At the closed-form threshold, precision was 0.181 and recall was 0.477.
