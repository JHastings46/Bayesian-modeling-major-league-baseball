# BayesBall Forecasting: Baseball Player HR and Strikeout Predictions

By Joel Hastings

## Project Overview

This project uses Bayesian modeling to estimate a baseball player’s true skill level instead of relying only on raw stats. I focused on two important rates:

- Home runs per plate appearance (HR/PA)
- Strikeouts per plate appearance (SO/PA)

The goal was to build a model that gives both an expected outcome and a realistic uncertainty range. In simple terms, this helps answer questions like:

- How much real power does this player have?
- How likely is this player to keep striking out at a high rate?
- What might happen over the next 200 plate appearances?

## Why Bayesian Modeling?

Raw baseball stats can be misleading, especially when a player has a small sample size. A hitter might look elite or terrible in a short stretch just because of randomness.

Bayesian modeling helps by:

- Estimating a player’s underlying true rate
- Pulling extreme small-sample results closer to a league baseline
- Showing uncertainty instead of only giving one number

This makes the results more realistic and more useful for decision-making.

## Dataset

The data came from a Baseball Reference batting table export.

### Raw Data
- 500 rows x 34 columns
- One row per player record
- Includes batting stats such as PA, HR, SO, BB, AVG, OPS, and more

### Final Modeling Data
After cleaning and filtering:
- 347 players
- Players with at least 200 plate appearances
- One row per player in the final dataset

## Data Cleaning and Preparation

The main cleaning steps included:

- Flattening and cleaning column names
- Dropping extra unnamed columns
- Removing repeated header rows inside the dataset
- Fixing player name encoding issues
- Removing Baseball Reference symbols like `*` and `#`
- Converting key columns such as `PA`, `HR`, and `SO` to numeric
- Keeping combined team rows for traded players when available
- Removing duplicate player records

## Modeling Approach

This project uses a Bayesian Beta-Binomial model built in PyMC.

For each player:

- The observed event count, such as HR or SO, is modeled as a binomial outcome
- The player’s true rate is treated as unknown
- The model learns a shared league-wide baseline from the data
- Player estimates are partially pooled toward that baseline

This means:

- Players with fewer plate appearances get more shrinkage
- Players with larger samples stay closer to their observed performance
- Every player gets both a best estimate and an uncertainty interval

## What the Model Produces

For each player, the model estimates:

- Posterior mean HR rate
- Posterior mean strikeout rate
- 90 percent credible interval
- Forecasted home runs over the next 200 plate appearances
- Forecasted strikeouts over the next 200 plate appearances

So instead of saying only “here is the average,” the model says:

- Here is the expected rate
- Here is the likely range
- Here is the forecast over a future sample

## Tools Used

- Python
- PyMC
- ArviZ
- NumPy
- pandas
- Matplotlib
- Google Colab

## Key Results

The project produced:

- Ranked player estimates for HR/PA
- Ranked player estimates for SO/PA
- 90 percent uncertainty intervals for each player
- Forecast distributions for the next 200 plate appearances
- Visualizations showing both expected value and uncertainty

## Why This Matters

This project shows why small-sample stats can be misleading. Bayesian modeling gives a more balanced estimate by combining individual player performance with overall league information.

That makes the results:

- More stable
- More realistic
- More honest about uncertainty
- More useful for forecasting and player evaluation

## Example Business Use

A baseball front office could use this type of model to:

- Avoid overreacting to hot streaks or slumps
- Compare players using both expected value and risk
- Forecast likely outcomes over future opportunities
- Support roster, scouting, and lineup decisions

## Future Improvements

Next steps for this project would include:

- Adding multiple seasons of data
- Including player context such as age, park effects, or handedness
- Building more advanced hierarchical structures
- Adding posterior predictive checks and calibration
- Creating a dashboard for live updates

## Final Takeaway

This project demonstrates how Bayesian statistics can turn noisy baseball stats into more useful forecasts. Instead of overreacting to raw numbers, the model gives a better estimate of true player skill along with the uncertainty around that estimate.

That makes the analysis more practical for real decision-making.

## Author

Joel Hastings
