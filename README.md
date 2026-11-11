**What shapes national compliance with girls’ education rights?**
/A machine learning analysis of UNESCO’s HerAtlas legal dataset, built to understand which factors line up with stronger or weaker legal protection for girls’ education.

The question:
What factors best explain variation in national compliance with UNESCO education rights indicators across regions and time?

About the data:
-The data comes from UNESCO’s HerAtlas, which tracks whether countries’ constitutions and laws protect girls’ education using 12 legal indicators. Examples include whether the legal age of marriage is at least 18 and whether the country has ratified CEDAW. Each row is one country’s answer to one question in one year.
-Raw file has 3,582 rows and 34 columns
-After cleaning, 3,236 records remain, covering 196 countries, 12 questions, 5 regions and the years 2019 to 2025

What I did:
-Cleaned the data. I removed 298 website layout rows (“Header” and “Footer”) that were all marked “Yes” and would have inflated compliance. I also removed 48 rows with no answer. I grouped answers into three labels, Compliant, Partial and Non-compliant, and treated “Yes, with reservations” as Partial.
-Explored it with charts by question, region and year.
-Split the data 60/20/20 into training, validation and test sets. Settings were chosen on the validation set, and the test set was used once at the end.
-Prevented data leakage by putting the encoder and scaler inside scikit-learn pipelines, so each cross-validation fold fits its own.
-Compared three models against a baseline that always guesses the most common label: Logistic Regression, Random Forest and a small neural network (MLP).
-Measured what matters using permutation importance and Cramér’s V.

Results:
Model (test set)	      Accuracy	Macro F1
Baseline	                 0.452	0.208
Logistic Regression	       0.593	0.582
Random Forest	             0.625	0.610
Neural network (MLP)	     0.617	0.604

All three models beat the baseline by a wide margin, but they are close to each other, so I do not claim one is clearly best. The type of legal question was by far the strongest factor, followed by region, with year only weak.

Limitations:
-Almost all countries were assessed in 2019. Later years cover only 5 to 24 countries each, so this is not a global trend over time.
-The data shows laws on paper, not whether they are enforced.
-Results are associations, not causes.
-The same country appears in many rows, so records are not fully independent.
-The models only know the question, region and year, so a lot stays unexplained.

Author

Ayesha Jawed, Habib University
