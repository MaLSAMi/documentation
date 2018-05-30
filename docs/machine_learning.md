### Machine Learning 

Machine Learning is a useful tool for *[pattern matching](https://en.wikipedia.org/wiki/Machine_learning)* and curve fitting to make predictions based on data itself. Given the recent breakthroughs and ease of use, it is worthwhile to try to analyze our problem in the lens of machine learning and analyze how our analysis changes. Since we are using real-time systems, we must also analyze the efficiency and cost of the algorithms and understand the tradeoffs among different techniques. Certain algorithms may be more suitable for the offline training phase while others on the online training phase. All of these are factors that will be considered when analyzing the models. 

The models will be evaluated loosely on their time of execution but more on their classification ability. As with all machine learning tasks, the goal is for high precision and high recall. This ensures that our models can not only correctly classify data to its appropriate labels, but that it is able to do so without overfitting. 

We are pursuing both routes with *[Deep Learning](Deep_Learning.md)* and *[Shallow_Learning](Shallow_Learning.md)* to compare the approaches. Although deep learning models are more flexible and advanced than its shallow learning counterparts, it is important to analyze both to see the strenghts of both approaches. Since resources and time of execution are a factor in the online phase, it is important to see whether a heavyweight network is worth the cost. Furthermore, this analysis will provide insight into the underlying patterns and general structure of the data. This will pave the way for further research to be done in both schedulability and data analysis. 

However, to get a more complete analysis, it is important to investigate as many viable choices as we can get. Furthermore, different data-mining 

