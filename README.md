# econ3916-lab18-model-evaluation
# Model Evaluation: The Curve, and What It Cannot Tell You

## Objective

I compared two models for a rare outcome and looked at how the cost of mistakes affected which model and threshold I would choose.

## Methodology

- I simulated 8,000 cases, split them into training and test sets, and fit a logistic regression and a boosted-tree model.
- I plotted ROC and precision-recall curves for the logistic regression and compared the two models' ROC AUCs using a paired bootstrap with 500 resamples of the test set.
- I built an expected-cost curve where a missed positive cost ten times as much as a false alarm. I chose the cheapest threshold using the training rows and evaluated its cost once on the test rows.
- I repeated that process for both models at cost ratios from 2:1 to 50:1 to see whether the cheaper model changed.
- I wrote `roc_point()` to calculate the false positive rate and true positive rate at a given threshold.

## Key Findings

- Only 11.8% of the test rows were positive. The logistic regression had a ROC AUC of 0.8468 and an average precision of 0.4651.
- The boosted-tree model had a ROC AUC of 0.8431. The AUC difference, calculated as logistic minus boosted, was +0.0038. The 95% bootstrap interval was [-0.0020, +0.0094], so I couldn't tell from this test set which model had the higher AUC.
- The threshold I chose was 0.0905. It cost 0.4692 per case on the test set, compared with 0.9437 at the default threshold of 0.5.
- The cheaper model changed depending on the cost ratio. At my chosen threshold, the logistic regression had a false positive rate of 0.296 and a true positive rate of 0.823.
