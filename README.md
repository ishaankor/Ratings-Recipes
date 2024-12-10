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

The graph illustrates the distribution of cooking times measured in minutes. The distribution appears to be right-skewed, with most values concentrated in the lower range, indicating that shorter cooking times are more common. A peak around common values suggests a central tendency, possibly reflecting typical meal preparation durations. The long tail toward the right highlights a few instances of extremely long cooking times, which could be outliers or special cases like slow-cooked recipes. This skewness suggests that the mean cooking time might be higher than the median. Understanding this trend could be helpful in planning meal preparation or designing recipe categories based on average cooking times.


### &#8594; Bivariate Analysis:

<iframe
  src="assets/bivariate_graph_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The bivariate graph illustrates the relationship between "Minutes" on the y-axis and "Rounded Rating" on the x-axis. The graph indicates a downward trend, suggesting that as the rounded rating increases, the average preparation time tends to decrease. This could imply that highly-rated recipes are generally quicker to prepare, possibly due to their simplicity or popularity. Clusters around lower ratings show wider variability in cooking times, indicating inconsistency in preparation effort. The dense concentration of points near the upper-middle section suggests a common preparation duration regardless of rating. Outliers appear at both extremes, representing unusually quick or lengthy preparations for certain ratings. The overall trend suggests that higher ratings are associated with longer times, though there is considerable spread within each rating group. As for The negative slope suggests an inverse relationship, meaning users might prefer recipes that balance quality and time efficiency. Understanding this trend can help optimize recipe recommendations based on user preferences for quick and highly-rated meals. The linear pattern suggests potential predictive modeling applications. The visible spread highlights the need for more granular analysis by recipe type or complexity. Lastly, the graph effectively visualizes how perceived quality (rating) relates to preparation effort (minutes).

### &#8594; Interesting Aggregates:

| name                                 |   (40, 6, 9, '194.8') |   (40, 10, 9, '138.4') |   (45, 12, 11, '595.1') |   (90, 17, 13, '267.0') |   (120, 7, 7, '878.3') |
|:-------------------------------------|----------------------:|-----------------------:|------------------------:|------------------------:|-----------------------:|
| 1 brownies in the world    best ever |                   nan |                      4 |                     nan |                     nan |                    nan |
| 1 in canada chocolate chip cookies   |                   nan |                    nan |                       5 |                     nan |                    nan |
| 2000 meatloaf                        |                   nan |                    nan |                     nan |                       5 |                    nan |
| 412 broccoli casserole               |                     5 |                    nan |                     nan |                     nan |                    nan |
| millionaire pound cake               |                   nan |                    nan |                     nan |                     nan |                      5 |


## Assessment of Missingness

<hr>

### &#8594; NMAR Analysis:

### &#8594; Missingness Dependency:

## Hypothesis Testing

<hr>

## Framing a Prediction Problem

<hr>

## Baseline Model

<hr>

## Final Model

<hr>

## Fairness Analysis

<hr>

