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


**Comparative Model Performance**

The sigmoid model provided the best fit for SBP, showing smooth transitions and interpretable parameters.
For DBP, the Gaussian model with a baseline component produced the most accurate description of the midlife peak and later decline.
The polynomial model achieved moderate accuracy but exhibited instability and less biological interpretability at extreme ages.

**Relevance to Model-Based Machine Learning**

This work illustrates a parameter-based modeling approach, where the assumed functional form reflects underlying physiological mechanisms.
It exemplifies model-based machine learning, emphasizing interpretability and structure over purely data-driven fitting.
Model parameters correspond to meaningful biological features, such as inflection points and baseline blood pressure levels.

**Suggestions for Future Modeling Improvements**

In future applications to real-life datasets, data should be cleaned and normalized, key covariates included, and models validated through cross-validation. 

Disclaimer: No generative AI (in any form) has been used to complete this homework.
