# Recommender_System

The approach of this recommendation system assumes users who liked the item in the past would still like the same in the future, which means, similar items would give similar ratings to a user.

In this recommendation system, singular value decomposition (SVD) is used, which is a collaborative filtering method. And the SVD constructs a matrix with users as row, and items as columns, and the elements are composed by the corresponding users’ rating on the item. And it decomposes a matrix into 3 other matrices and extracts the factors from the factorization of a high-level matrix. 

The SVD model of this recommendation system is built based on the users’ past behavior, that is the rating of items of each user. And the model finds the association between the users and the items. Then the model predicts the items or rating of the item by considering those features, that the user may be interested. However, to train the model, we are predicting the rating for the user on specific items. 

While for each prediction, a pair of (u,i) where u: user_id, i: item_id are required to input. To achieve this goal, the scikit “surprise” module is used for learning. At the same time, to reduce the error between the actual and predicted rating, the bias term is used. The bias term is shown below. 

r ̂_ui=μ+b_u+b_i+q_i^T p_u

If user u is unknown, bias b_u  and factor p_u  are assumed to be 0
If item i  is unknown, bias b_i and factor q_(i ) are assumed to be 0

To estimate the unknowns, we minimized the following regularized error:

∑_(r_ui∈R_train)▒〖〖(r_ui- r ̂_ui)〗^2+ λ(b_i^2+ b_u^2+|(|q_i |)|^2+ |(|p_u |)|^2 〗

Stochastic Gradient Descent is used to minimize the error. n_epochs are the number of iterations in SGD which is a tunable parameter along with n_factors which is number of factors. Learning rate is set to 0.005 and regularization terms are set to 0.02 by default.
![image](https://user-images.githubusercontent.com/60958440/188543023-cf5e3d07-5370-4f4a-afcf-8804c7eb5c67.png)

