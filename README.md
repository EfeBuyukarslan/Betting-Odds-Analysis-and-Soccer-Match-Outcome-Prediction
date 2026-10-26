# Betting Odds Analysis and Soccer Match Outcome Prediction

How good are bookmakers at pricing soccer matches, and where does the market get it wrong?

Course project, Boğaziçi University.

## The problem

A bookmaker's odds imply a probability for each outcome. If those implied probabilities are well calibrated, they should match how often the outcome actually happens. Where they don't, there is either noise in the data or an exploitable bias. This project tests which.

## Approach

**From odds to probabilities.** Implied probabilities are the inverse of the decimal odds, then normalised to remove the bookmaker's margin, so the three outcomes sum to one.

**Calibration test.** Matches are binned by the difference between implied home-win and away-win probability. Within each bin, the realised draw frequency is compared against the implied draw probability, separately for the first and second half. A systematic gap between the two is evidence of bias rather than noise.

**Noise filtering.** Two scenarios that distort late-match state were removed and the analysis re-run:
- matches whose result changed after the 85th minute, since a late goal rewrites the outcome without reflecting the state the odds were priced on
- matches with a red card inside the first 15 minutes, which changes the game drastically from the start

**Findings.** Across the full dataset the implied and realised draw probabilities track each other closely, with no consistent direction of bias. After removing late-goal noise, a pattern appears: in the first half the bookmaker tends to overestimate draw probability when the away team is seen as stronger, while in the second half implied probabilities sit below realised ones in certain probability bins. Removing early red card matches changed little — only two matches qualified out of 648.

**Outcome models.** Two decision trees were fitted to predict the result: one using all features including odds, one using match statistics only. Comparing them indicates how much of the predictable signal the odds already contain, which is a direct read on market efficiency. Features were built as home-minus-away differences for possession, dangerous attacks, goal attempts and goals, with missing values forward- and backward-filled within each match.

## Files

- `Report-Code Combined.ipynb` — analysis and write-up in one notebook
- `Report-Code Combined.html` — rendered version

## Tools

Python · pandas · NumPy · scikit-learn · Matplotlib · Seaborn
