# Ratings & Recipes: Food Clash-Off!

## Introduction

<hr>

Being the big foodie that I am, I love trying various food and enjoying new cuisines! From my mother's food to American food, I've seen how food differs from culture to culture -- it's one of the most fun experiences I'll always treasure. When I saw how Icould analyze data about food in many ways, I immediately knew that I was entering a flavorful world! I went to look into the dataset and I found that there are ***so*** many factors to consider when determining how ratings/cost are calculated. The further I looked into the dataset and each recipe's ratings, I found that cooking times are influential to how well a recipe truly is but I wasn't fully sure. The question that I researched furthered into is: "**Do characteristics like minutes (cooking times) lead to highly-rated recipes (e.g., rating >= 4.0)?**" I always though that the more time somoene puts into making a dish, the better it will be -- how about we put it to the test? Understanding the answer to this question will make us care about the recipes in various perspectives. For example, from the mind of home cooks and recipe developers, they might want to take the findings from this study so that they can prioritize specific factors (e.g., fewer steps or ingredients) to make appealing recipes. There's also the food platforms like food.com who publish recipes that might be tailored to specific user preferences, boosting their user engagement as a result. Before diving deeper into the analysis, let's breakdown the various components of the dataset:

The relevant columns in **RAW_recipes.csv**:

| Column      | Description                                                                                                                                                                                       |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 'name'      | Recipe name                                                                                                                                                                                       |
| 'id'        | Recipe ID                                                                                                                                                                                         |
| 'minutes'   | Minutes to prepare recipe                                                                                                                                                                         |
| 'nutrition' | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| 'n_steps'   | Number of steps in recipe                                                                                                                                                                         |
| 'n_ingredients' | The number of ingredients in each recipe
                          

Here are why these columns are important:
- '**name**': The name of the recipe -- without the name, how could we classify recipes!
- '**id**': The ID of each recipe so that we can merge with the 'RAW_interactions.csv' dataset!
- '**minutes**': The cooking time for each recipe.
- '**nutrition**': The nutrition information that is connected to each recipe.
- '**n_steps**': The number of steps in every recipe.
- '**steps**': The steps for recipe in text.
- '**ingredients**': The different ingredients for recipe in text.
- '**n_ingredients**': The number of ingredients for recipe.

In total, there are about **83782** rows and **12** columns in this dataset! 

The relevant columns in **RAW_interactions.csv**:

| Column      | Description  |
|-------------|--------------|
| 'recipe_id' | Recipe ID    |
| 'rating'    | Rating given |

Here are why these columns are important:
- '**recipe_id**': The ID of each recipe so that we can merge with the 'RAW_recipe.csv' dataset!
- '**rating**': The ratings of each recipe so that we can see how well people like it.

In total, there are about **731927** rows and **5** columns in this dataset! By analyzing both datasets, we'll find answers to not only mine but some other ones as well!

## Data Cleaning and Exploratory Data Analysis

<hr>

### &#8594; Data Cleaning:

|    | name                                 |     id |   minutes |   n_steps |   n_ingredients |   rating |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |
|---:|:-------------------------------------|-------:|----------:|----------:|----------------:|---------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        10 |               9 |        4 |          138.4 |                10 |            50 |              3 |               3 |                    19 |                     6 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        12 |              11 |        5 |          595.1 |                46 |           211 |             22 |              13 |                    51 |                    26 |
|  2 | 412 broccoli casserole               | 306168 |        40 |         6 |               9 |        5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |
|  3 | millionaire pound cake               | 286009 |       120 |         7 |               7 |        5 |          878.3 |                63 |           326 |             13 |              20 |                   123 |                    39 |
|  4 | 2000 meatloaf                        | 475785 |        90 |        17 |              13 |        5 |          267   |                30 |            12 |             12 |              29 |                    48 |                     2 |

Cleaning up the dataset was pretty straightforward; I filled all the missing values in 'rating' and also split some data up into their own seperate columns. I first started by merging the **RAW_interactions.csv** with the **RAW_recipes.csv** where the `rating` column will join the other factors that I need to analyze. I then replaced all the missing values with `np.NaN` in order to clean the data up and give us a true analysis of the dataset. After that, I grouped by the 'recipe' column and extracted every recipe's ratings in order to change them with the average of their ratings. To get it into my merged dataset, I then left merged the average ratings with the bigger merged file based on the 'id' column and then I split up 'nutrition' column into their own seperate columns and the right datatype. I made a DataFrame with the columns that contains all the proper nutrition information that was provided (`[calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), and carbohydrates (PDV)]`) and then set the rows to be the values in the list of 'nutrition'. I finished up the data generating process by merging this new created DataFrame with the most updated merged DataFrame and then dropping all the unnecessary columns like `['contributor_id', 'submitted', 'tags', 'nutrition', 'steps', 'description', 'ingredients']` since I'm not particularly interested in these. 

### &#8594; Univariate Analysis:

<iframe
  src="assets/univariate_graph_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

To see the distirbution of the `minutes` columsn, the graph above illustrates the distribution of cooking times measured in minutes. The distribution appears to be right-skewed, with most values concentrated in the lower range, indicating that shorter cooking times are more common. Because it is right-skewed, it suggests that the mean cooking time might be higher than the median. There seems to be a peak around common values which suggests a central tendency, or the average time it takes for meal preparation.  The long tail toward the right highlights a few instances of extremely long cooking times, which could be outliers or special cases like slow-cooked recipes (there's a recipe that takes more than 1 **million** minutes). By understanding this trend, it will be helpful in planning meal preparation or designing recipe categories based on average cooking times.


### &#8594; Bivariate Analysis:

<iframe
  src="assets/bivariate_graph_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

To see the surface level of influence of `minutes`, the graph illustrates the relationship between `minutes` on the y-axis and `rating` (rounded) on the x-axis. It also indicates a downward trend, which shows that as the rounded rating increases, the average preparation time tends to decrease. This could imply that highly-rated recipes are generally quicker to prepare, possibly due to their simplicity or popularity. There also seems to be clusters around lower ratings which show wider variability in cooking times. The dense concentration of points near the upper-middle section suggests a common preparation duration regardless of rating. The overall trend suggests that higher ratings are associated with longer times, though there is considerable spread within each rating group. As for the negative slope, it suggests an inverse relationship which means that users might prefer recipes that balance quality and time efficiency. Understanding this trend can help optimize recipe recommendations based on user preferences for quick and highly-rated meals. The linear pattern suggests potential predictive modeling applications. I would say that the graph effectively visualizes how perceived quality (rating) relates to preparation effort (minutes)!

### &#8594; Interesting Aggregates:

|   n_steps |         1 |       2 |       3 |       4 |       5 |       6 |       7 |       8 |       9 |      10 |      11 |      12 |      13 |      14 |        15 |      16 |        17 |        18 |     19 |        20 |       21 |      22 |   23 |    24 |   25 |   26 |   27 |   28 |   29 |   30 |   31 |   32 |   33 |   37 |
|----------:|----------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|--------:|----------:|--------:|----------:|----------:|-------:|----------:|---------:|--------:|-----:|------:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|
|         1 | nan       | 4.64071 | 4.7733  | 4.69127 | 4.67418 | 4.64172 | 4.5456  | 4.56062 | 4.56667 | 4.56598 | 4.55    | 4.59259 | 4.16667 | 4.68333 | nan       | 4.6     |   4.88889 | nan       | nan    | nan       | nan      | nan     |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|         2 |   5       | 4.72059 | 4.68695 | 4.68823 | 4.65714 | 4.64529 | 4.70391 | 4.66105 | 4.58803 | 4.67843 | 4.67839 | 4.56513 | 4.82926 | 4.64583 |   4.375   | 4.13141 | nan       | nan       | nan    |   3       | nan      | nan     |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|         3 |   5       | 4.71517 | 4.66226 | 4.64924 | 4.6654  | 4.64271 | 4.65801 | 4.65914 | 4.62165 | 4.67618 | 4.65346 | 4.68069 | 4.6275  | 4.37168 |   4.76908 | 4.7381  |   4.85714 |   4.55556 |   5    |   4.46429 |   5      | nan     |  nan | nan   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|         4 |   4.83333 | 4.72326 | 4.6613  | 4.63692 | 4.67729 | 4.67225 | 4.60177 | 4.61056 | 4.6427  | 4.56961 | 4.59457 | 4.64688 | 4.7083  | 4.65029 |   4.63537 | 4.56695 |   4.75    |   4.75564 |   4.75 |   4.33333 |   4.9375 |   5     |  nan |   5   |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |  nan |
|         5 |   4.25    | 4.58198 | 4.64923 | 4.64822 | 4.64328 | 4.61548 | 4.60445 | 4.60963 | 4.54944 | 4.57725 | 4.61091 | 4.60648 | 4.6117  | 4.50497 |   4.57825 | 4.66775 |   4.8373  |   4.77579 |   4.75 |   4.91667 | nan      |   4.925 |    5 |   4.5 |  nan |    5 |  nan |    5 |  nan |  nan |  nan |  nan |  nan |  nan |

In this pivot table, I wanted to see the general average of ratings given `'n_steps'` (number of steps) and `'n_ingredients'` (number of ingredients). To do this, I wanted to find aggregate statistics like mean for the recipe's 'rating' that are grouped by `n_steps` and `'n_ingredients'`. While only the first five rows are showing, each cell shows the mean rating for recipes with specific combinations of steps and ingredients. This is an interesting pivot table as it shows how recipes with fewer steps (`'n_steps'` <= 2) generally have slightly higher mean ratings across various ingredient counts. Not to mention, it shows how higher numbers of ingredients (`'n_ingredients'` > 10) tend to show more sparse data, with some combinations not represented, likely due to fewer such recipes in the dataset. I also feel like it's important to mention all the `nans` in the table as well. To explain, there are some dataset limitations like when some combinations may not make sense or are unlikely to occur/don't even exist. For instance, recipes with n_steps = 1 but n_ingredients = 30 would require extremely efficient instructions. This explains how both of these two factors (`'n_steps'` and `'n_ingredients'`) are so interconnected in this dataset as that makes sense in this context.

## Assessment of Missingness

<hr>

### &#8594; NMAR Analysis:

Based on the analysis of the dataset, I believe the `'rating'` column is a strong candidate for being Not Missing At Random (NMAR). I think that it is NMAR for multiple reasons such as users might be less likely to leave ratings if they had a negative experience with a recipe but don't want to share that feedback publicly (I'm a victim of this, admittedly). On another hand, users might only rate recipes they really liked or disliked, skipping neutral experiences. There's also the case where if the dataset primarily contains highly rated recipes, recipes with poor performance might be missing due to being unpublished or underrepresented. If we wanted to make the `rating` column MAR, additional info such as how often users view recipes without rating them or even showing when recipes were published versus when interactions occurred (this could reveal whether newer recipes are more likely to have missing ratings!).

### &#8594; Missingness Dependency:

Given that I think that `rating` column is NMAR, I need to conduct several missingness permutation tests and evaluate whether the missingness of the `rating` column is dependent on specific features of the dataset. To pick the right columns, I thought that the `sodium (PDV)` column shouldn't influence whether `rating` is missing or not while `calories (#)` should as it might make people not leave a rating if a recipe isn't worth the calories. As a result, I tested if `sodium (PDV)` is independent of `rating` and `calories (#)` is dependent to `rating`. 

<iframe
  src="assets/dependent_missingness_graph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

For **calories (#)**, the observed test statistic that I picked was the absolute difference in means between missing and non-missing groups which evaluted to **53.83**. A permutation test was performed by randomly shuffling the `missing_indicator` labels 1,000 times to create a null distribution of test statistics, assuming no relationship between `rating` missingness and `calories (#)`. The resulting p-value was **0.0**, indicating that none of the permuted test statistics were as extreme as the observed statistic. This provides strong evidence to reject the null hypothesis, supporting the conclusion that the missingness of `rating` is **dependent** on `calories (#)`. The histogram proves this relationship as it shows the distribution of permuted test statistics under the null hypothesis, centered around zero, with the observed statistic (red dashed line) falling far outside the range of the null distribution. In contrast, the histogram for `sodium (PDV)` displays the observed statistic within the range of the permuted test statistics, consistent with the null hypothesis of independence.

<iframe
  src="assets/independent_missingness_graph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

For **sodium (PDV)**, the observed test statistic was **1.44**, and the p-value was **0.502**, indicating that the observed difference in means between the missing and non-missing groups is consistent with the null hypothesis. The histogram of permuted test statistics showed that the observed statistic lies near the center of the null distribution, further supporting the conclusion that the missingness of `rating` is **independent** of `sodium (PDV)`. These results suggest that calorie levels may influence whether a rating is missing, while sodium levels do not.

## Hypothesis Testing

<hr>

<iframe
  src="assets/hypothesis_testing_graph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Seeing how `calories (#)` influences the missingness of `rating`, I wanted to see the distribution without the missing values. The **histogram** (represented by blue bars) shows the distribution of permuted test statistics, specifically the absolute differences in means for `calories (#)` between recipes with missing and non-missing `rating` values. This distribution represents the null hypothesis, assuming that there is **no relationship** between the missingness of `rating` and `calories (#)`. After the permutation tests, The **observed test statistic**, represented by the red dashed line, is **53.83**, which lies far outside the range of the permuted distribution. This indicates that the observed difference in means is **significantly larger** than what would be expected under the null hypothesis, suggesting a strong deviation from the assumption of independence. The corresponding **p-value** is reported as **0.0**, meaning that **none** of the permuted test statistics were as extreme as the observed statistic. This provides **strong evidence** to **reject the null hypothesis**, supporting the conclusion that the missingness of `rating` is **dependent** on `calories (#)`. In **conclusion**, the results suggest that recipes with missing `rating` values **likely have significantly different calorie levels** compared to those with recorded ratings. This finding highlights that **calorie information may influence** whether a recipe’s rating is recorded, emphasizing the importance of accounting for this dependency in any further analysis of the dataset.

## Framing a Prediction Problem

<hr>

The goal of this prediction task is to determine whether a recipe will receive a high rating (≥ 4.0) based on specific features. These features include cooking time (`minutes`) and the number of ingredients (`n_ingredients`). To achieve this, the target variable, `high_rating`, was defined as a binary variable: `1` for recipes with a `rating` >= 4.0 , and `0` for recipes with a `rating` < 4.0. The prediction task will involve a baseline model of random forest in order to train and classify `high_rating`. The evaluation of the model's performance relied on metrics such as accuracy, precision, recall, and F1-score as it will provid a comprehensive view of the model's ability to classify recipes correctly. This prediction problem is particularly valuable for recipe creators aiming to design recipes likely to achieve high ratings and for platforms that recommend recipes to users based on historical preferences. By leveraging these insights, the task supports better decision-making in recipe creation and recommendation systems. Understanding these factors helps identify what makes a recipe appealing to users and provides insights into which features most influence recipe ratings.

## Baseline Model

<hr>

For my baseline model, it will include two quantitative features: `minutes` and `n_ingredients`. Because they are quantitative features, both features are continuous/discrete and required no special encoding so I transformed them using `StandardScaler` to ensure they were on the same scale. The model and preprocessor itself is a Random Forest Classifier, which is perfect for binary tasks like this one. Right off the gate, the performance metrics indicate strong overall performance as it scored an accuracy of **90.02%**. The model performs exceptionally well in predicting high ratings (`1`), achieving a precision of **0.90**, recall of **1.00**, and an F1-score of **0.95** for this class. However, the same could not be said about the performance for low ratings (`0`). My model scored poor with a precision of **0.13**, recall of **0.00**, and an F1-score of **0.01**. This contrast is attributed to the fact that there is significant class imbalance in the dataset, where high ratings are much more present than the low ratings. The weighted F1-score of **0.86** which indicates strong overall performance. It should also be noted that the macro-average F1-score of **0.48** highlights the model's struggle to generalize to both classes. While the model is very effective at predicting high ratings, it fails to identify low ratings effectively. This suggests that the model is biased towards the majority class (`1`), which is common in imbalanced datasets. Despite this limitation, the model is considered "good" for predicting high ratings, which aligns with the primary objective of the task. To improve its performance, I considered techniques such as resampling, adjusting class weights, and hypertuning. If I could succesfully implement these adjustments, it would significantly enhance the model's ability to generalize to unseen data while maintaining its strong predictive power for high ratings!

## Final Model

<hr>

To improve the prediction task, two additional features were engineered and added to the model: `log_minutes` and `ingredients_steps_ratio`. The `log_minutes` feature is a log-transformed version of the original `minutes` column. This transformation helps reduce the skewness of the `minutes` distribution, which is often highly right-skewed due to recipes with extremely long cooking times. By applying a log transformation, the feature becomes more normally distributed, making it more suitable for machine learning models and allowing the algorithm to better differentiate between recipes with moderate and long cooking times. The `ingredients_steps_ratio` is another engineered feature, calculated as the ratio of the number of ingredients to the number of steps (plus one to avoid division by zero). This feature captures the relationship between recipe complexity (number of steps) and the richness of the recipe (number of ingredients). It provides insight into whether recipes with a high ingredient-to-step ratio, indicating simpler recipes, are more likely to receive high ratings. These features align well with the data generation process because they directly address the complexity and preparation characteristics of a recipe, which are key factors influencing user ratings. The chosen modeling algorithm was a Random Forest Classifier, which is well-suited for this task due to its ability to capture non-linear relationships and handle interactions between features. Hyperparameter tuning was conducted using GridSearchCV, a systematic approach to searching for the best combination of hyperparameters. The parameter grid included options for the number of estimators (`n_estimators`), the maximum depth of trees (`max_depth`), and the minimum number of samples required to split a node (`min_samples_split`). The best-performing hyperparameters were found to be `n_estimators=100`, `max_depth=10`, and `min_samples_split=10`. These parameters suggest that a moderately deep tree with more controlled splits helped balance model complexity and generalization, resulting in better performance. The Final Model’s performance, with an accuracy of **90.25%**, represents a slight improvement over the Baseline Model’s accuracy of **90.02%**. While the accuracy improvement appears marginal, the Final Model benefits from a more robust set of features and optimized hyperparameters. Additionally, the inclusion of engineered features provides a deeper understanding of the factors influencing recipe ratings, aligning better with the underlying data generation process. This makes the Final Model not only more accurate but also better aligned with the practical aspects of predicting user preferences.

## Fairness Analysis

<hr>

The fairness analysis of the final model was conducted by dividing the test set into two groups based on the feature `minutes`, representing the cooking time required for recipes. Group X consisted of recipes with cooking times less than or equal to the median value of `minutes`, while Group Y included recipes with cooking times greater than the median. This grouping was selected because cooking time is a critical characteristic that could affect how well the model predicts high ratings. The evaluation metric used for this fairness analysis was **precision**, which measures the proportion of correctly predicted high-rated recipes out of all recipes predicted as high-rated. Precision was chosen because it reflects how reliably the model identifies high-rated recipes, an essential consideration in this classification task. The null hypothesis (H₀) assumed that the model’s precision is equal for both Group X and Group Y, with any observed differences due to random chance. The alternative hypothesis (Hₐ) proposed that the model’s precision differs between the two groups, indicating potential unfairness. The test statistic used was the absolute difference in precision between the two groups. A standard significance level of **α = 0.05** was chosen, meaning that if the p-value fell below this threshold, the null hypothesis would be rejected. The results revealed an **observed precision difference** of **0.0169** between the two groups, with a **p-value** of **0.001**. Since the p-value is much lower than the significance level of 0.05, the null hypothesis was rejected, providing strong evidence that the observed difference in precision is statistically significant and unlikely to be due to random chance. In conclusion, the fairness analysis indicates that the model's performance differs significantly between recipes with short and long cooking times. This result suggests that the model demonstrates potential bias and may require fairness-aware adjustments, such as dataset rebalancing or more advanced fairness-oriented algorithms, to improve its performance across both groups.
