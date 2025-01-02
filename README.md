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




