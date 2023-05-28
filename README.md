# MovieLens Recommender System

![Recommender](https://github.com/arunaabh95/movielens-recommender/blob/master/deliverables/recommender.png)

## Abstract
This paper discusses the development of a recommender system using collaborative filtering models to provide personalized recommendations to users based on their preferences and behavior. The study evaluates the performance of different collaborative filtering techniques using the MovieLens dataset to recommend movies to users. The paper presents a comparative analysis of the methodologies used in this study. The results of this research can be useful for improving user experience and engagement on e-commerce, online marketplaces, social media, and entertainment platforms that use recommender systems.

**View the report [here](https://github.com/arunaabh95/movielens-recommender/blob/master/deliverables/movielens_recommender_system.pdf).**

## Data Source
The dataset used in this study is the `ml-latest-small` dataset from MovieLens, and is available at https://grouplens.org/datasets/movielens/latest/.

## Results
In this study, we evaluated and compared various collaborative filtering models to find the most suitable one for our use case. We used the surprise library in Python, which provides a set of algorithms for building recommender systems. The models that we considered in this study are BaselineOnly, KNNBasic, KNNWithMeans, KNNWithZScore, KNNBaseline, SVD, SlopeOne, and CoClustering.

To determine the best performing model, we first trained all the models using 5-Fold cross-validation and evaluated their mean RMSE (root mean square error) and MAE (mean absolute error) for rating prediction.

|    Algorithm     |   Mean RMSE   |   Mean MAE   |
| ----------------:| :-----------: | :----------: |
| **BaselineOnly** | **0.872201**  | **0.672369** |
|      **SVD**     | **0.873066**  | **0.670550** |
|  **KNNBaseline** | **0.874612**  | **0.668504** |
|  KNNWithZScore   |   0.894428    |   0.678830   |
|   KNNWithMeans   |   0.897073    |   0.685302   |
|     SlopeOne     |   0.899393    |   0.687146   |
|   CoClustering   |   0.944743    |   0.731583   |
|     KNNBasic     |   0.945871    |   0.724686   |

Among the models evaluated, **BaselineOnly**, **SVD**, and **KNNBaseline** performed the best, with a mean RMSE of around **0.87** and a mean MAE of around **0.67**.

We then evaluated the models for recommender Precision@k, Recall@k, and F1 Score, using a rating threshold of 4 and a value of k set to 10.

The models were retrained using 5-Fold cross-validation. It was observed that while the BaselineOnly model had the best RMSE and MAE for rating prediction, it performed poorly in terms of Precision@k,  Recall@k, and F1 score for recommendation.

|   Algorithm   | Precision@10 |   Recall@10  |   F1 Score   |
| -------------:| :----------: | :----------: | :----------: |
| BaselineOnly  |   0.562327   |   0.256928   |   0.352679   |
|  **KNNBasic** | **0.813299** | **0.414142** | **0.548792** |
|  KNNWithMeans |   0.703773   |   0.397760   |   0.508226   |
| KNNWithZScore |   0.726752   |   0.409591   |   0.523872   |
|  KNNBaseline  |   0.759915   |   0.392979   |   0.518015   |
|      SVD      |   0.715530   |   0.350241   |   0.470264   |
|    SlopeOne   |   0.746035   |   0.386291   |   0.508984   |
|  CoClustering |   0.618293   |   0.354801   |   0.450861   |

In our evaluation of various models for the recommender system, we observed that each model has a different trade-off between evaluation metrics such as RMSE, MAE, Precision@k, Recall@k, and F1 score. In order to balance these metrics and obtain optimal results, we chose the **KNNBaseline** model as our final recommendation model.

To generate movie recommendations, the KNNBaseline model was retrained on the entire dataset, and predictions were made for unrated movies of each user. The predicted ratings were then sorted in descending order and the top 10 highest predictions were selected as the recommended movies.
