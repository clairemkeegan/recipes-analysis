# Recipe Analysis of Food.com Dataset
By: Claire Keegan (clairemk@umich.edu)

## Introduction:
The Recipes and Ratings Dataset is JAM-packed (see what I did there 😉) with delicious recipes ranging from chicken and sun-dried tomato orzo to honeyed fig topping with vanilla and cinnamon. The dataset contains over 80,000 recipes, including more than 50 recipes for different types of jam. We also have over 700,000 ratings for said recipes, which provide more context for each recipe and how popular they are. These datasets, which were
merged together, provide a plethora of information that can be used in a variety of different analyses, which makes it difficult to narrow down which question to focus on. There are factors included in these sets, such as the ingredients, cook time, nutritional values, the number of steps, what the said steps are, and more. The ratings add another layer of information and data to discover. 

The central question this analysis will focus on is: What is the relationship between the number of ingredients and steps and the number of minutes it takes to cook the recipe?

This was the focus of the analysis because our current culture is all about saving time and money while remaining healthy. As people become busier with their work and social life, they have less time to cook healthy and delicious meals. For some, cooking is difficult because of both access to healthy ingredients and a working kitchen with all of the tools necessary to make the meal. Others have not grown up with knowledge in the kitchen, maybe because they had working parents or caregivers who did not know how to cook and often took them to restaurants instead.  It is important to have a variety of healthy, easy meals that can be made with minimal/ inexpensive ingredients.

Knowing that there are more recipes than only in this dataset, the idea that there are practically unlimited meals to cook makes planning meals quite a daunting task. With this analysis alone, we have access to a dataset with over 80,000 recipes. I aim to make narrowing down your weekly menu easier with this analysis. I do this by finding if there is a correlation between the number of ingredients and the number of minutes it takes to cook a recipe, acknowledging that the recipes with fewer ingredients and or less cook time are the most convenient and plausible for the majority of people. 

After looking into the correlation between the number of ingredients and steps with the cook time, I dug deeper by applying a regression analysis to predict the length of cooking time given a variety of factors. This can help calculate recipes that may not be included in the dataset that has been provided. 

While a variety of factors can contribute to the number of minutes it takes to cook a recipe, for this analysis, these are the columns I am using:
- Name: The name of the dish or item that is being cooked
- Minutes: The number of Minutes it takes to cook the recipe.
- Number of Steps: The number of steps required to make the recipe.
- Steps: The actual description of what each individual step is.
- Ingredients: The foods necessary to make the recipe.
- Number of Ingredients: The number of ingredients needed to make the recipe.

The other columns I could have used were:
- ID: The numerical ID given to the recipe.
- Contributor ID: The ID number of the person who posted the recipe to the internet.
- Submitted: The date at which the recipe was posted on the internet.
- Tags: The important words or phrases included in the recipe that help differentiate them from one another. Example tags include ‘easy’, ‘for 1 or 2’, and  ‘vegan’
- Nutrition: This column contains the list of the recipes' values for calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), and carbohydrates (PDV).
- Description: The full description of the meal or item that can be made with the recipe.
- Date: The date that the review was posted to a recipe
- Rating: The rank out of 5 stars that the reviewer gave to the recipe after trying it.
- Review: The actual written review of a user who made the recipe.
- Average rating: Taking into account all ratings given to a recipe, the average rating out of five stars that was given to the recipe.
Some of these factors are included in the regression analysis in later parts. 



## Data Cleaning:

When starting this analysis, a variety of data cleaning techniques had to be used to have a dataset reflective of what I wanted to analyze and eventually predict. First, I merged the two data sets (the recipes and the reviews), where I created a new column with the average rating for each recipe. This was important because it added a new layer of information, although I did not take it into account in my initial analyses, it was helpful knowing I could look at this information when needed. All missing values for the ratings were filled with NaN because we still wanted to include recipes that did not have ratings, either because they were new or just not as common.  I did, though, remove any recipes that did not have a cook time or number of steps associated with them because I needed to ensure I only included recipes that had the data I was interested in analyzing. Next, I noticed a few recipes that took many hours to cook or that took a large number of ingredients or steps. Knowing that this is a deterrent for many, I decided to only keep the recipes that came within two standard deviations away from the mean of cook time, and then applied this again for the number of steps, and then again for the number of ingredients. I then decided to apply this to the minutes two more times because I wanted recipes that were all less than 4 hours to cook. All of these steps were completed to be sure that only the most important and practical recipes were being analyzed for the average person. This analysis is not for those interested in making something that takes more than 4 hours to cook, we want quick, easy meals that can save time and promote nutritional values.


| name                                  |   minutes |   n_steps |   n_ingredients |
|:--------------------------------------|----------:|----------:|----------------:|
| impossible macaroni and cheese pie    |        50 |        11 |               7 |
| impossible rhubarb pie                |        55 |         6 |               8 |
| impossible seafood pie                |        45 |         7 |               9 |
| paula deen s caramel apple cheesecake |        45 |        11 |               9 |
| midori poached pears                  |        25 |         8 |               9 |
| penne with bacon  spinach   mushrooms |        30 |        15 |               8 |
| peanut butter logs                    |         5 |         5 |               7 |



### Univariate Analysis: 

 <iframe
 src="assets/file-name.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 
Include the Boxplot of the number of minutes

This boxplot shows the distribution of the number of minutes the remaining recipes take to make. After the data cleaning, we have recipes with cook times ranging from 0 to 205 minutes. Interestingly, it shows that all of the recipes from 108 minutes onwards are outliers, so the majority of recipes take less than 108 minutes.

### Bivariate Analysis:

 <iframe
 src="assets/file-name.html"
 width="800"
 height="600"
 frameborder="0"
 ></iframe>
 
Include the scatterplot of the ratio of ingredients/steps vs minutes 

This scatterplot shows a slightly negative relationship between the ingredients-steps ratio and the number of minutes it takes to cook the recipe. When there are overwhelmingly more ingredients than steps, the plot shows that the recipes do not take very long. Most of the longest recipes have very small ratios where the number of steps and ingredients are more even.

### Interesting Aggregates:

| n_ingredients |   minutes |
|:--------------|----------:|
|             1 |   20.6579 |
|             2 |   21.4975 |
|             3 |   24.4471 |
|             4 |   29.2526 |
|             5 |   33.6591 |
|             6 |   38.0988 |
|             7 |   41.4827 |
|             8 |   43.4311 |
|             9 |   47.3024 |
|            10 |   48.3165 |
|            11 |   50.3348 |
|            12 |   53.161  |
|            13 |   56.2245 |
|            14 |   57.1234 |
|            15 |   59.2052 |

The table I included was grouped by the number of ingredients, with the corresponding column containing the mean cook time for that number of ingredients. This is useful because we have an easier way of seeing if there is an increase or decrease when the number of ingredients increases. When looking at this table, we can see a clear increase in cook time for every ingredient increase, which helps to show that there is a clear relationship between cook time and the number of ingredients in the recipe.

### Imputation:

I did not fill in any missing values because the values were so important to my initial analysis. I really did not want to mess with anything that was not a part of the dataset because I wanted a dataset that was very reflective of the population. I felt safer just removing the values that had NaN in the number of steps, ingredients, and minutes. 

## Framing a Prediction Problem:

**What factors help predict the number of minutes it takes to cook a recipe?**

I picked the response variable to be cook time because that is one of the most important factors when it comes to deciding what meal to cook. In some cases, people come up with their own recipes and have no way of predicting how long it will take for them to cook it, with this analysis, they may be able to get an estimated cook time to know how much time they need to alot in their busy schedule to make the recipe. I picked a regression analysis since it was a quantitative variable with many factors that influenced it. Using MSE, we can evaluate the model. Since we are not certain whether or not the data is linear, we use MSE instead of R^2. We are using the number of ingredients and steps to conduct this prediction problem, which are known before the meal is cooked. 


## Baseline Model:

I made a model using a linear regression to predict the number of minutes it takes to cook the recipe. The features I included were the number of steps and the number of ingredients because I believed they were the two most important features when determining the number of minutes that the recipe takes. The two features were quantitative, predicting a quantitative feature. The performance of the model was not very good, I had an MSE of almost 1000, it was 999.20599, and an R^2 value of 0.1314002. These values do not reflect a good prediction for the training data since the MSE is so large and the R^2 is so low. This can be very much improved, which will be done in the final model. 


## Final Model:

I added the feature number of ingredients divided by steps because that makes a more standardized version of the factors, which helps gather more information from the same data. For example, a ratio of more ingredients than steps is likely shorter than one with more steps and fewer ingredients. I also added the interaction between steps and ingredients because I thought that would potentially change the model a bit, since the number of steps and ingredients do have a significant impact on the time it takes to cook a recipe. A larger value would contribute to a likely longer recipe.

I started with a RandomTreeRegressor with n_estimators = 100 and the maximum depth = 22 after conducting a grid CV search, but after further trials, I found other models that worked better. 


The final model was a slight improvement over my baseline performance because I had a smaller MSE of 985.985327429368 and a higher R^2 of 0.33 (when the minutes were log transformed). This shows an improvement since we have fewer errors between the predicted and the actual number of minutes it took to cook. While this was not as large of an improvement as I would have wanted, it still did improve some. I tried a variety of different models, and the one that ended up working the best was the HistGradientBoostingRegressor, where I was able to get my MSE down by about 15 minutes. Since I have such a vastly variable data set, it is difficult to get a low MSE.
