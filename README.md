# Ratings & Recipes: Food Clash-Off!

### Introduction

Being the big foodie that I am, I love trying various food and enjoying new cuisines! From my mother's food to American food, I've seen how food differs from culture to culture -- it's one of the most fun experiences I'll always treasure. When I saw how Icould analyze data about food in many ways, I immediately knew that I was entering a flavorful world! I went to look into the dataset and I found that there are ***so*** many factors to consider when determining how ratings/cost are calculated. The further I looked into the dataset and each recipe's ratings, I found that cooking times are influential to how well a recipe truly is but I wasn't fully sure. The question that I researched furthered into is: "**Do characteristics like higher cooking times (minutes) lead to highly-rated recipes (e.g., rating >= 4.0)?**" Understanding the answer to this question will make us care about the recipes in various perspectives. For example, from the mind of home cooks and recipe developers, they might want to take the findings from this study so that they can prioritize specific factors (e.g., fewer steps or ingredients) to make appealing recipes. There's also the food platforms like food.com who publish recipes that might be tailored to specific user preferences, boosting their user engagement as a result. Before diving deeper into the analysis, let's breakdown the various components of the dataset:

The relevant columns in **RAW_recipes.csv**:

| Column      | Description                                                                                                                                                                                       |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 'name'      | Recipe name                                                                                                                                                                                       |
| 'id'        | Recipe ID                                                                                                                                                                                         |
| 'minutes'   | Minutes to prepare recipe                                                                                                                                                                         |
| 'tags'      | Food.com tags for recipe                                                                                                                                                                          |
| 'nutrition' | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| 'n_steps'   | Number of steps in recipe                                                                                                                                                                         |
| 'steps'     | Text for recipe steps, in order
| 'ingredients' | The ingredients in each recipe
| 'n_ingredients' | The number of ingredients in each recipe

Here are why these columns are important:
- '**name**': The name of the recipe -- without the name, how could we classify recipes!
- '**id**': The ID of each recipe so that we can merge with the 'RAW_interactions.csv' dataset!
- '**minutes**': The cooking time for each recipe.
- '**tags**': The various attributions for each recipe.
- '**nutrition**': The nutrition information that is connected to each recipe.
- '**n_steps**': The number of steps in every recipe.
- '**steps**': The steps for recipe in text.

In total, there are about **83782** rows and **12** columns in this dataset!


The relevant columns in **RAW_interactions.csv**:

| Column      | Description  |
|-------------|--------------|
| 'recipe_id' | Recipe ID    |
| 'rating'    | Rating given |
| 'review'    | Review text  |

Here are why these columns are important:
- '**recipe_id**': The ID of each recipe so that we can merge with the 'RAW_recipe.csv' dataset!
- '**rating**': The ratings of each recipe so that we can see how well people like it.
- '**review**': The review for each recipe in text.

In total, there are about **731927** rows and **5** columns in this dataset!


### Data Cleaning and Exploratory Data Analysis

### Assessment of Missingness

### Hypothesis Testing

### Framing a Prediction Problem

### Baseline Model

### Final Model

### Fairness Analysis
