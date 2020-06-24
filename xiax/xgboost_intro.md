### What?

[XGBoost](https://xgboost.ai/) is a decision-tree-based ensemble Machine Learning algorithm that uses a [gradient boosting](https://en.wikipedia.org/wiki/Gradient_boosting) framework.

- In prediction problems involving **unstructured data (images, text, etc.)** artificial neural networks tend to outperform all other algorithms or frameworks. However, when it comes to **small-to-medium structured/tabular** data, decision tree based algorithms are considered best-in-class right now.

- Differences between decision tree algorithms

  ![img](https://miro.medium.com/max/1850/1*QJZ6W-Pck_W7RlIDwUIN9Q.jpeg)

  1. **Decision Tree**: Every hiring manager has a set of criteria such as education level, number of years of experience, interview performance. A decision tree is analogous to a hiring manager interviewing candidates based on his or her own criteria.
  2. **Bagging**: Now imagine instead of a single interviewer, now there is an interview panel where each interviewer has a vote. Bagging or bootstrap aggregating involves combining inputs from all interviewers for the final decision through a democratic voting process.
  3. **Random Forest**: It is a bagging-based algorithm with a key difference wherein only a subset of features is selected at random. In other words, every interviewer will only test the interviewee on certain randomly selected qualifications (e.g. a technical interview for testing programming skills and a behavioral interview for evaluating non-technical skills).
  4. **Boosting**: This is an alternative approach where each interviewer alters the evaluation criteria based on feedback from the previous interviewer. This ‘boosts’ the efficiency of the interview process by deploying a more dynamic evaluation process.
  5. **Gradient Boosting**: A special case of boosting where errors are minimized by gradient descent algorithm e.g. the strategy consulting firms leverage by using case interviews to weed out less qualified candidates.
  6. **XGBoost**: Think of XGBoost as gradient boosting on ‘steroids’ (well it is called ‘Extreme Gradient Boosting’ for a reason!). It is a perfect combination of software and hardware optimization techniques to yield superior results using less computing resources in the shortest amount of time.
     ![img](https://miro.medium.com/max/1554/1*FLshv-wVDfu-i54OqvZdHg.png)

### Xgboost Optimizations

**System Optimization:**

1. **Parallelization**: XGBoost approaches the process of sequential tree building using [parallelized](http://zhanpengfang.github.io/418home.html) implementation. This is possible due to the interchangeable nature of loops used for building base learners; the outer loop that enumerates the leaf nodes of a tree, and the second inner loop that calculates the features. This nesting of loops limits parallelization because without completing the inner loop (more computationally demanding of the two), the outer loop cannot be started. Therefore, to improve run time, the order of loops is interchanged using initialization through a global scan of all instances and sorting using parallel threads. This switch improves algorithmic performance by offsetting any parallelization overheads in computation.
2. **Tree Pruning:** The stopping criterion for tree splitting within GBM framework is greedy in nature and depends on the negative loss criterion at the point of split. XGBoost uses ‘max_depth’ parameter as specified instead of criterion first, and starts pruning trees backward. This ‘depth-first’ approach improves computational performance significantly.
3. **Hardware Optimization**: This algorithm has been designed to make efficient use of hardware resources. This is accomplished by cache awareness by allocating internal buffers in each thread to store gradient statistics. Further enhancements such as ‘out-of-core’ computing optimize available disk space while handling big data-frames that do not fit into memory.

**Algorithmic Enhancements:**

1. **Regularization**: It penalizes more complex models through both LASSO (L1) and Ridge (L2) [regularization](https://towardsdatascience.com/l1-and-l2-regularization-methods-ce25e7fc831c) to prevent overfitting.
   - L1 and L2 regularization diff:
     - L 1 **Lasso shrinks the less important feature’s coefficient to zero** thus, removing some feature altogether. So, this works well for **feature selection** in case we have a huge number of features. **(abosolute magnitude penalty term in loss function)**
     - L2 works well to avoid overfitting. **(squared magnitude penalty term in loss function)**
2. **Sparsity Awareness**: XGBoost naturally admits sparse features for inputs by automatically ‘learning’ best missing value depending on training loss and handles different types of [sparsity patterns](https://www.kdnuggets.com/2017/10/xgboost-concise-technical-overview.html) in the data more efficiently.
3. **Weighted Quantile Sketch:** XGBoost employs the distributed [weighted Quantile Sketch algorithm](https://arxiv.org/pdf/1603.02754.pdf) to effectively find the optimal split points among weighted datasets.
4. **Cross-validation**: The algorithm comes with built-in [cross-validation](https://towardsdatascience.com/cross-validation-in-machine-learning-72924a69872f) method at each iteration, taking away the need to explicitly program this search and to specify the exact number of boosting iterations required in a single run.

### Performance

![img](https://miro.medium.com/max/1920/1*U72CpSTnJ-XTjCisJqCqLg.jpeg)

### Xgboost VS Logistic Regression

- [Out of box performance xgboost vs logistic regression](https://www.kaggle.com/tahuichimiguel/fraud-detection-logit-regression-vs-gbm)
  
- Xgboost better recall worse precision
  
- Both algorithms are really fast. There isn't much to distinguish them in terms of run-time.
- Logistic regression will work better if there's a **single** decision boundary, not necessarily parallel to the axis.
- Decision trees can be applied to situations where there's not just one underlying decision boundary, but many, and will work best if the class labels roughly lie in hyper-rectangular regions.
- Logistic regression is intrinsically simple, it has low variance and so is less prone to over-fitting. Decision trees can be scaled up to be very complex, are are more liable to over-fit. Pruning is applied to avoid this.
- Maybe you'll be left thinking, "I wish decision trees didn't have to create rules that are parallel to the axis." This motivates **support vector machines**.

- Decision Trees and logistic regression are two of the most widely used classification algorithms. These algorithms use different logic to create the decision boundaries for classification.

  Depending on how the data is distributed, one of these algorithm will give better classification results compared to the other :

  Logistic Regression fits a single line to divide the space into two and so performs better than a decision tree **when the data is distributed** in a fashion such that it can be **linearly classified.**

  Although a **single linear boundary can sometimes be limiting factor** for Logistic Regression.

  **When the data is distributed in a Non-Linear fashion or for higher dimensional data,** the decision tree algorithm will beat the logistic regression as it is better able to divide the space into smaller sub-spaces.

  However, when the **classes are not well separated** trees can overfit the data , also called the ***data snooping bias.\*** In that case again, the **logistic regression will perform better**

- training speed: logistic regression
- interpretability: logistic regression
- model stability: logistic regression
- model prediction execution time: logistic regression
- tasks where the output is know to be a logistic function of the input: most definitely logistic regression (probably, provably, nothing better)
- AUC: where when the input variables are truly independent and mostly continuous (i.e. tasks that regression in general excels at): logistic regression - sometimes marginal improvements over XGBoost because a continuous function is fit.
- OTOH: XGBoost wins tons of Kaggle contests and beats out logistic regression, and boosted decision trees (some years ago) frequently won bake-offs in ML literature. So, in most scenarios, unless your don’t have the time to tune parameters AND perform n training folds on the whole process, XGBoost.

![image-20200528020044985](/Users/xingfanxia/Documents/bear_notes/image-20200528020044985.png)

![image-20200528020102798](/Users/xingfanxia/Documents/bear_notes/image-20200528020102798.png)