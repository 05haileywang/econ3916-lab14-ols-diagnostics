# econ3916-lab14-ols-diagnostics

# Lab 14: OLS Diagnostics — When the Standard Error Is Lying

## Objective

The purpose of this lab was to examine how violations of OLS assumptions affect regression coefficients, standard errors, and confidence intervals. I also explored how regression diagnostics can identify potential problems with a model.

## Methodology

I used Python, NumPy, statsmodels, and the California Housing dataset to examine different regression diagnostics.

- Simulated heteroskedasticity and compared classical OLS standard errors with HC3 robust standard errors
- Ran 400 simulations to evaluate how often 95% confidence intervals contained the true coefficient
- Examined four residual plots to identify heteroskedasticity, missing curvature, and outliers
- Used Breusch-Pagan and Jarque-Bera tests to evaluate error variance and residual normality
- Calculated leverage, standardized residuals, and Cook's distance to identify influential observations
- Compared regression estimates before and after removing an influential observation
- Used the California Housing dataset to compare classical and robust standard errors
- Wrote an `hc3_se()` function to calculate HC3 robust standard errors for selected coefficients
- Simulated omitted variable bias in the take-home challenge

## Key Findings

### 1. Heteroskedasticity and Robust Standard Errors

The estimated slope was approximately 2.0147, compared to the true slope of 2.0. The coefficient remained unchanged when using robust standard errors, but the standard error increased from 0.0264 to 0.0290.

This demonstrated that heteroskedasticity does not necessarily bias OLS coefficients, but it can make classical standard errors unreliable.

### 2. Confidence Interval Coverage

Across 400 simulated samples, the classical 95% confidence interval contained the true slope in 91.8% of simulations, compared to 93.5% for the HC3 robust interval.

The Monte Carlo standard errors were 1.4% and 1.2%, respectively. The classical interval fell further below the nominal 95% coverage rate, suggesting that robust standard errors provided more reliable inference in this simulation.

### 3. Residual Diagnostics

I examined four residual patterns: well-behaved residuals, heteroskedasticity, missing curvature, and an outlier.

The Breusch-Pagan test helped identify nonconstant error variance, while the Jarque-Bera test examined whether residuals departed from normality. However, these tests did not detect every type of model problem, demonstrating why residual plots are also important.

### 4. Influential Observations

After removing one influential observation from a dataset of 600 observations, the estimated slope decreased from 2.0325 to 2.0142.

The slope changed by approximately 0.58 of its original standard error, while the standard error decreased by 33%.

This showed that an extreme observation can have a larger effect on estimated uncertainty than on the coefficient itself.

### 5. California Housing Regression

In the California Housing regression, the coefficient on average rooms per household (`AveRooms`) was approximately −0.0273.

The HC3 robust standard error was 0.0121, approximately 5.02 times the classical standard error.

The dataset also contained 965 districts with housing values recorded at the upper ceiling. After excluding these districts, the HC3 standard error decreased to approximately 0.0082.

However, removing observations simply to obtain smaller standard errors could introduce selection bias and change the population being studied.

### 6. Take-Home Challenge: Omitted Variable Bias

I simulated a regression where the true coefficient was 1.5, but the estimated coefficient was approximately 2.508 because an important confounding variable was omitted.

The regression passed the Breusch-Pagan test and had no observations with Cook's distance above 1, but it failed the Jarque-Bera test.

Although the simulation did not pass every diagnostic, it demonstrated that regression diagnostics cannot directly determine whether a confounding variable has been omitted.

## Conclusion

This lab helped me understand that a regression coefficient can appear reasonable even when its standard error is unreliable. I learned how to use robust standard errors, residual plots, and formal diagnostic tests to evaluate regression results.

The most important takeaway was that passing diagnostic tests does not necessarily mean a regression is correctly specified. We also need to consider omitted variables, causal relationships, and the assumptions behind the model before interpreting the results.
