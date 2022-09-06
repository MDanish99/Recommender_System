# Recommender_System
This task was part of the assignment in the course SDSC 3002 (Data Mining) taught by Dr.Yu Yang at City University of Hong Kong. The task was as follows:

Download the files "training.txt", "testing.txt" and "item_tag.txt". In the file "training.txt", each line is in the form 

![CodeCogsEqn (1)](https://user-images.githubusercontent.com/60958440/188551499-a076e48a-6e92-49d3-9cc5-48252a4b02a6.gif)

which means the rating of user u, on the item i is ![CodeCogsEqn](https://user-images.githubusercontent.com/60958440/188551677-d7c6b1e5-e048-45c4-b046-976d3b0527a0.gif).

In the file "testing.txt", each line is represented by u,i,? which means you are required to predict the rating of user u on item i. Use the training dataset "training.txt" to build a recommender system and make predictions for the testing dataset "testing.txt" by replacing all the "?" with your predicted ratings. All the ratings are within the range [0,5].

You may also want to use the file "item_tag.txt", where each line ![CodeCogsEqn (2)](https://user-images.githubusercontent.com/60958440/188551961-75a67be2-f647-4e7b-885e-998d871a3597.gif) indicates that the item i has tags ![CodeCogsEqn (3)](https://user-images.githubusercontent.com/60958440/188552034-0519c725-53f7-41eb-80cc-f307f723893a.gif). Note that some items may not have any tags so it is normal if you cannot find some items in the file "item_tag.txt".


Solution Approach:

The approach of this recommendation system assumes users who liked the item in the past would still like the same in the future, which means, similar items would give similar ratings to a user.

In this recommendation system, singular value decomposition (SVD) is used, which is a collaborative filtering method. And the SVD constructs a matrix with users as row, and items as columns, and the elements are composed by the corresponding users’ rating on the item. And it decomposes a matrix into 3 other matrices and extracts the factors from the factorization of a high-level matrix. 

The SVD model of this recommendation system is built based on the users’ past behavior, that is the rating of items of each user. And the model finds the association between the users and the items. Then the model predicts the items or rating of the item by considering those features, that the user may be interested. However, to train the model, we are predicting the rating for the user on specific items. 

While for each prediction, a pair of (u,i) where u: user_id, i: item_id are required to input. To achieve this goal, the scikit “surprise” module is used for learning. At the same time, to reduce the error between the actual and predicted rating, the bias term is used. The bias term is shown below.

![CodeCogsEqn (4)](https://user-images.githubusercontent.com/60958440/188552521-f6f58c38-0729-4bd0-98ba-6f82f7d500b2.gif)

![image](https://user-images.githubusercontent.com/60958440/188552585-d1463b2e-305f-4772-99fb-a02255d2f149.png)

To estimate the unknowns, we minimized the following regularized error:

![image](https://user-images.githubusercontent.com/60958440/188552696-4ddbb9c8-b1a0-4a70-8ac7-84afaccd960a.png)

Stochastic Gradient Descent is used to minimize the error. n_epochs are the number of iterations in SGD which is a tunable parameter along with n_factors which is number of factors. Learning rate is set to 0.005 and regularization terms are set to 0.02 by default.







