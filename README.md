# summary of findings
Wenfeng He

wenfeng.he@emory.edu

I choose to answer HW3: Model-based Bias Removal in Machine Learning using Synthetic Blood Pressure Data

**Key Insights**

TaskA iv. **Interpret Model Parameters**

    For the polynomial model, `c1` determines the curvature of the blood pressure–age relationship, showing how quickly the rate of change itself changes with age, while `c2` represents the linear trend or overall slope. The unit of `c1` is `mmHg/year²`, and `c2` is `mmHg/year`, both expressing how blood pressure varies quantitatively with age.  

    In the sigmoidal–Gaussian model, `S_max` represents the maximum attainable SBP as age increases, and `a0` is the age when SBP reaches half of its maximum value, reflecting the inflection point of the rise. `D_max` indicates the maximum DBP value typically around middle age, `a_peak` gives the age when DBP reaches this peak, and `σ` controls the spread or width of the DBP curve, indicating how sharply or gradually it declines.  

v. **Discussion and Analysis**

  i. Which model captures age trends in SBP and DBP better?
  
      The sigmoidal–Gaussian model better captures the age-related patterns of SBP and DBP than the polynomial model. The sigmoid function reflects the gradual rise and plateau of SBP, while the Gaussian function accurately represents the midlife peak and decline in DBP. In contrast, the polynomial model fits the general trend but tends to oscillate or diverge at the data boundaries, reducing biological interpretability.  
      
  ii. How do model parameters reflect physiological blood pressure changes with age?
  
      Model parameters correspond closely to physiological processes. The sigmoid curve’s inflection point represents the age at which vascular stiffness accelerates SBP increase, while the Gaussian peak shows when DBP reaches its maximum due to arterial elasticity changes and then declines. Thus, the models capture how blood vessel properties evolve with aging.  
      
  iii. Discuss limitations in capturing demographic nuances.
  
      Applying the methods to larger and more diverse real-life datasets would improve generalizability and allow testing whether the same parameter trends hold across populations.

TaskB iii.) Discussion

  i. Reflect on the importance of balanced datasets in healthcare.
  
    Balanced datasets are essential in healthcare modeling because they ensure that predictive models learn patterns representative of all patient groups. When datasets are balanced, models can generalize better across sexes, ages, or conditions, avoiding bias toward the majority group.  
    
  ii. Discuss implications and challenges with real-world unbalanced datasets (by changing M and F ).
  
    In real-world healthcare data, imbalance is common — for instance, when the number of male (`M`) and female (`F`) samples differs significantly. Such imbalance can lead to biased model predictions, lower accuracy for minority groups, and misleading clinical conclusions.
    
  iii. Suggest and explore strategies to address these challenges in practice, based on the example provided in the class
  
    Based on the class example, I add an option for sex bias loss from Lecture11 ppt page24 to the Regression binary classifier. By explicitly penalizing the accuracy difference between males and females in its objective, this loss function compels the model to find a more equitable decision threshold that improves performance for the minority group, rather than naively maximizing overall accuracy.

### Comparative Model Performance  

  TaskA. Plot model curves for SBP and DBP against the plots in the preprint[1].

![Comparison](./Comparison%20of%20Fitted%20Models%20with%20Preprint%20Fig4.png)

    For the SBP models, both the polynomial and sigmoid fits achieved very high accuracy, with `MSE = 0.03862` and `R² = 0.99861` for the polynomial model, and `MSE = 0.03884` and `R² = 0.99860` for the sigmoid model. This indicates that both models describe the age–SBP relationship extremely well, though the sigmoid provides better physiological interpretability.  

    For the DBP models, the Gaussian fit significantly outperformed the polynomial model. The polynomial model had `MSE = 0.32148` and `R² = 0.95432`, whereas the Gaussian model achieved `MSE = 0.00829` and `R² = 0.99882`, effectively capturing the midlife peak and decline in DBP.  

    Overall, the sigmoidal–Gaussian combination best captures the nonlinear and physiologically meaningful trends of SBP and DBP across age groups.

TaskB. Analysis:

i. Discuss classifier performance changes with different male/female data ratios.

    As shown in the ROC Performance plot, accuracy is deceptively high at extreme data imbalances (e.g., 10% or 90% males) because the model simply predicts the majority class. The F1-score, a better metric, reveals poor performance in these cases and peaks only when data is balanced (50% ratio). 

![ROC Curves for Classifier](./ROC%20Curves%20for%20Classifier.png)  

ii. Identify and examine potential biases introduced by varying prevalences

    The logistic regression classifier, optimizing for overall accuracy, becomes biased towards the majority class in imbalanced datasets. This results in poor predictive power for the minority class, as evidenced by the low F1-scores. Such a model would be unfair and unreliable in a real-world setting.

![Performance (Without bias-penalized)](./Performance%20(Withoutbias-penalized).png) 

iv. Bias Mitigation in Training: Modify your training strategy (e.g., loss function) to systematically reduce sex bias. Explain the reasoning behind the chosen method.

    Bias Mitigation Strategy The mitigation strategy employed is a post-processing technique that systematically reduces sex bias by optimizing the decision threshold. the method minimizes sex bias loss (from Lecture11 ppt page24). This function penalizes the model for performance disparities between sexes, forcing it to find a threshold that balances overall accuracy with fairness. The without mitigation strategy uses a fixed threshold, which is blind to fairness and performs poorly on the minority group. The with mitigation strategy uses an adaptive threshold that is sensitive to fairness. This successfully corrects for the bias introduced by data imbalance, leading to a more equitable and reliable classifier, as confirmed by the stable F1-scores across all tested data ratios.
![Performance (With bias-penalized)](./Performance%20(With%20bias-penalized).png)  

**Relevance to Model-Based Machine Learning**

    This work illustrates a parameter-based modeling approach, where the assumed functional form reflects underlying physiological mechanisms. It exemplifies model-based machine learning, emphasizing interpretability and structure over purely data-driven fitting. Model parameters correspond to meaningful biological features, such as inflection points and baseline blood pressure levels.

**Suggestions for Future Modeling Improvements**

    In future applications to real-life datasets, data should be cleaned and normalized, key covariates included, and models validated through cross-validation. 

Disclaimer: ChatGPT was used for analysis HW11.Q3, Conversation is available at (./ChatGPT4Q3.pdf) 

### References

[1] [Learning from Two Decades of Blood Pressure Data: Demography-Specific Patterns Across 75 Million Patient Encounters](https://arxiv.org/pdf/2402.01598)
