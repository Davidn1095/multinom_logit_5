# multinom_logit_5

Data Preparation:

presion, imc, and frecuencia vectors are defined, representing blood pressure categories, body mass index (BMI) categories, and their respective frequencies.
Chapman.Tabla.Frame <- data.frame(Presion = presion, IMC = imc, Frecuencia = frecuencia): A DataFrame Chapman.Tabla.Frame is created from these vectors.
print(Chapman.Tabla.Frame): This line prints the DataFrame to the console for inspection.
Converting Columns to Factors:

Chapman.Tabla.Frame$Presion and Chapman.Tabla.Frame$IMC are converted into factors with specific levels. This is essential for categorical analysis in logistic regression.
Fitting an Ordinal Logistic Regression Model:

Ajuste.Ordinal.Tab <- polr(Presion ~ IMC, data = Chapman.Tabla.Frame, weights = Frecuencia): Fits an ordinal logistic regression model with Presion as the dependent variable and IMC as the independent variable, using Frecuencia as weights.
summary(Ajuste.Ordinal.Tab): Provides a summary of the fitted model, including coefficients and their statistical significance.
summary(Ajuste.Ordinal.Tab)$coefficients: Extracts the coefficients from the model summary.
Interpreting Coefficients:

exp(-summary(Ajuste.Ordinal.Tab)$coefficients[1:2,1]): Exponentiates the negative coefficients for the first two predictors (IMC categories) to interpret them as odds ratios.
exp(summary(Ajuste.Ordinal.Tab)$coefficients[3:5,1]): Exponentiates the coefficients for the thresholds (cut-points between Presion categories) to understand the odds of moving from one category to the next.
Model Comparison Using ANOVA:

The script compares two ordinal logistic regression models using ANOVA: one with only an intercept and another with IMC as a predictor.
Predictions from the Model:

predict(Ajuste.Ordinal.Tab, type = "probs"): Predicts the probabilities of each category for each observation.
predict(Ajuste.Ordinal.Tab, type = "class"): Predicts the class (category of Presion) for each observation.
Evaluating Model Predictions:

A contingency table is created to compare the actual Presion categories with the predicted ones, accounting for the frequencies.
Custom Statistical Test Calculations:

frecuencias and probabilidades vectors are defined, representing observed frequencies and predicted probabilities, respectively.
The script calculates the log-likelihood for the valid (non-zero frequency and probability) cases.
deviance_saturado is calculated as -2 times the log-likelihood, representing the deviance of a saturated model.
Estadistico is the difference in deviance between the fitted model and the saturated model.
pchisq(Estadistico, 3, lower.tail = F): Calculates a p-value using a chi-square test for the Estadistico with 3 degrees of freedom. This tests the goodness-of-fit of the model.


