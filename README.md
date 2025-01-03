# Balanced News Recommendation Algorithm

Objective Statement: _This project aimed to develop a recommendation algorithm that curates a balanced newsfeed by delivering articles users are less than 75% likely to engage with 50% of the time, while the remaining 50% features content aligned with their preferences. The goal was to retain user engagement while mitigating polarization, reducing media bias, and promote exposure to diverse perspectives._

__1. Data__

I decided to use the Microsoft News Dataset (MIND) which is a large-scale benchmark for news recommendation research, collected from anonymized behavior logs of the Microsoft News website. It includes around 160k English news articles and over 15 million impression logs from 1 million users. Each article contains detailed content, including title, abstract, and category, while impression logs record click events, non-clicked events, and a user's historical interactions with news.

https://msnews.github.io/

__2. Data Wrangling__

The Microsoft News Recommendation Dataset (MIND) initially contained over two million rows. For model training, a random sample of 5,000 rows was selected, focusing on three features: User ID, Article ID, and an interaction column. The Article ID was created by merging two columns, and the interaction column was derived by extracting click behavior (1 for a click, 0 for no click). After removing null values, the final dataset consisted of 346,635 rows and three columns.

__3. EDA__

Before fitting the data to the model, I first assessed class balance to ensure the predictions wouldn’t be skewed by imbalanced data. A bar plot

![image](https://github.com/user-attachments/assets/f70ec5bb-ee30-4fd6-8e7c-fb8bef39a189)

confirmed that the dataset had a relatively balanced distribution of clicks and non-clicks, with slightly fewer clicks than non-clicks. I then explored user engagement, visualized through a histogram

![image](https://github.com/user-attachments/assets/58608cf0-f09f-4dcb-a3db-1edfc692d5ef)

which showed a positively skewed distribution with a mean of 54 interactions per user over the 6-week period. Next, I examined article popularity with a scatter plot

![image](https://github.com/user-attachments/assets/da1ff6d2-9569-41cb-a565-113ace946849)

revealing that the average number of clicks per article was around nine, with higher click counts becoming increasingly sparse. These visualizations confirmed expected engagement patterns and prepared the data for modeling.

__4. Modeling__

I considered data preprocessing options such as one-hot encoding and standardization but found them unnecessary due to the high cardinality of the Article ID and User ID columns. I split the data into 80% training and 20% testing using sklearn's train_test_split. Initially, I tested a logistic regression model but achieved a low accuracy of 0.51. After experimenting with an XGBoost model, I improved the accuracy to 62%. However, the best results came from a Random Forest Classifier, which I optimized using Bayesian grid search, achieving an accuracy of over 80%. A performance comparison of all three models is shown in the following figure

![image](https://github.com/user-attachments/assets/85822e93-4f6e-4eaa-8678-a3716fcbd6de)

which highlights the Random Forest Classifier's superior performance across multiple metrics. To generate recommendations with reduced bias, I used the predict_proba() method to calculate interaction probabilities and created a balanced set of recommendations, where 50% were less than 75% likely to be interacted with, providing a more diverse newsfeed while maintaining engagement.

__Application & Future Work__

A variation of this recommendation algorithm could be applied to news aggregation platforms like Google News, Apple News, or Microsoft News, providing users with a more balanced newsfeed while retaining engagement. While this project does not implement the algorithm directly into any of these applications, it demonstrates the potential for a more diverse approach to news recommendations. The algorithm follows a simple methodology, but future iterations could train on additional features, allowing the model to predict interactions with a broader range of articles. Future work could also involve experimenting with different predicted interaction cutoffs to further optimize the balance between engagement and diversity in newsfeeds.
