# TabPFNComparison
v1 vs v2 vs v3
哪个最好用？我要说服我上级，以及我的朋友。v3明显更好，但是他们守旧，又非常死板，必须要可复刻的以数据为基准的结果。

# Compare the efficiency of the different versions

Since v1 supports a context of 1000 rows and 100 features, while v3 supports 1,000,000 rows and 20,000 features, we expect v1 to plateau in performance when handling data > 1000 rows, and v2 to not experience plateauing, but to continue to grow in accuracy all the way until 1,000,000 rows. 

# Dataset

Yeh, I. (2009). Default of Credit Card Clients [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C55S3H.

This research aimed at the case of customers' default payments in Taiwan and compares the predictive accuracy of the probability of default among six data mining methods. TabPFN supports performing classification on this dataset. 

老也没问题，因为只是要做个demo。（实际上，如果要把所有数据集都用上，就是整个世界都装不下了。）

# Ways of Comparison 
routine
- Different sample sizes (contexts): We will vary the context size (training set size) over 200, 500, 1,000, 2,000, 5,000, 10,000, 20,000 samples to study its effect.
- For each context size, DO NOT perform k-fold validation.
- perf.counter() record efficacy
- (optional) if hit maximum capacity (v1 hits 1,000) (v2 hits 10,000) (v3 hits 1,000,000), would the inference speed be the same?
- (optional) What if unnecessary features are given to TabPFN, would its performance drop? 

# Expected Conclusion:
- v1 for > 1,000 sample size, v2 for 10,000, v3 for 1,000,000, accuracy, f1, etc. plateaus [paper reference]

# Code Structure: 
- introduction, EDA, fit models, create files, measurements, conclusion

# EDA
Explore the Yeh "Default of Credit Card Clients" dataset, with summary statistics (.describe()), find scale meanings and types of features (.info()), fit all predictors, select based on feature importance (coefficient > 0) and qualitative analysis (logical inference), use selected features (based on correlation matrix; high r among features means taking out all except 1)

# Fit Models
拟合模型，对于每个dataset。（如果无需训练就跳过）

# Infer and Create Files
对每个模型（没有hyperparameter tuning），喂入所有features，尝试得出target（原始结果保存在csv中）
包括cv，每个split得到一个dataset
k=10-fold cv * hyperparameter tuning （"3 * 8 * 5 * 5 * 4 * 3 * 5 = 36,000"）* 5个模型 = 1,800,000 个 csv

# Metrics and measurements
在每个csv上，与正确target做对比，得出1,800,000 * （10个metrics）= 18,000,000 metric数量。
5个模型，各自3,600,000个metrics做对比（需要hyperparameter tuning变种能够一一对应（但这是不可能的））
通过holistic evaluation全人测试，看看哪个模型最好

# Conclusion
使用已保存文件，写出结论

# Discussion 
TabPFN各版本显著好于传统机器学习，
v3显著好于v2显著好于v1
所以用TabPFN forever！
（反方登场：不行！"Is TabPFN the silver bullet for tabular data?" NO!）

# Actual Conclusion: 


