# Abdominal-Trauma-Detection-Capstone-Project
GROUP 5 MEMBERS:

1. CATHERINE GAKII 
2. JOY KAMAU
3. WILFRED NJAGI
4. BRENDA KINYA
5. JOYCE MUTHIKE
6. LEE KIMAITA
7. DANIEL NDIRANGU
 ### Table of contents 
 - [Business Understanding](#Business-Understanding)
 - [Problem Statement](Problem-statement)
 - [Data Understanding](#Data-Understanding)
 - [Modelling](#Modelling)
 - [Results and Conclusion](#Results-and-Conclusion)
 - [Recommendations](#Recommendations)
 ![](.png)

# Business Understanding
With more than 5 million deaths caused by traumatic injury each year, it is the largest cause of early-life mortality and a major public health concern worldwide. Among these, blunt abdominal trauma is frequently sustained in car accidents and can cause serious internal bleeding and damage. In Kenya, a country of over 50 million people, this challenge is magnified by the severe shortage of healthcare infrastructure—only about 50 CT scanners and 200 trained radiologists are available nationwide. This shortage leads to misdiagnoses, delayed treatments due to average waiting times of several weeks, and a lack of access to vital healthcare services for many Kenyans. Despite government initiatives to invest in new CT scanners and train more radiologists, the need for rapid and accurate diagnosis remains critical. However, it is sometimes difficult and time-consuming for medical personnel to interpret CT scans for abdominal injuries. Therefore, there is an urgent need for automated, accurate, and rapid diagnostic solutions as any delay can be fatal.

# Problem Statement
With more than 5 million deaths caused by traumatic injury each year, it is the largest cause of early-life mortality and a major public health concern worldwide. Among these, blunt abdominal trauma is frequently sustained in car accidents and can cause serious internal bleeding and damage. In Kenya, a country of over 50 million people, this challenge is magnified by the severe shortage of healthcare infrastructure—only about 50 CT scanners and 200 trained radiologists are available nationwide. This shortage leads to misdiagnoses, delayed treatments due to average waiting times of several weeks, and a lack of access to vital healthcare services for many Kenyans. Despite government initiatives to invest in new CT scanners and train more radiologists, the need for rapid and accurate diagnosis remains critical. However, it is sometimes difficult and time-consuming for medical personnel to interpret CT scans for abdominal injuries. Therefore, there is an urgent need for automated, accurate, and rapid diagnostic solutions as any delay can be fatal.

# Data Understanding
**1. labels (image_level_labels.csv) Dataset:**

- Number of Rows: 12,029
- Number of Columns: 4
- Columns:
    - patient_id: Unique identifier of the patient.
    - series_id: An identifier for the series of images associated with each patient..
    - instance_number: Specific image instance number within the series.
    - injury_name: Type of injury detected in the image.
- Data Types: The data types are appropriate with integer types for identifiers and object (string) type for the injury name.
- Unique Values: There are 246 unique patients, 330 unique series, 925 unique instance numbers and **2 unique injury types;  Active_Extravasation and bowel.**
  "***Note:*** *Active extravasation in relation to abdominal trauma is the leakage of blood from a blood vessel in the abdomen into the surrounding tissue leading to organ failure or death."*

**2. train(train.csv) Dataset:**

- Number of Rows: 3,147
- Number of Columns: 15
- Columns:
    - patient_id: Unique identifier of the patient.
    - 'any_injury': It serves as a binary indicator representing the presence or absence of any abdominal injury for each patient. A binary variable like 'any_injury' is often used to simplify complex conditions into a format that machine learning algorithms can process.
    - The other 13 columns represent the health status and injury severity of various organs in the adnomen for each patient, namely; the bowel, extravasation, the kidney, the liver and the spleen. They are recorded as binary variables where 0 indicates the absence of a condition, and 1 indicates the presence of a condition.
- Data Types: All columns are of integer type.
- Unique Values: There are 3,147 unique patients. The injury-related columns have binary values (0 or 1), indicating the absence or presence of a specific injury type.

**3. train_meta (train_series_meta.csv) Dataset:**

- Number of Rows: 4,711
- Number of Columns: 4
- Columns:
    - patient_id: Unique identifier of the patient.
    - series_id: An identifier for the series of images associated with each patient..
    - aortic_hu: A quantitative measure of the aorta's radiodensity in  Hounsfield units(HU) on a CT scan. It is measured on a scale of -1000 to 1000 and normally ranges between 150 and 400 HU depending on the patient's age, sex, and other factors.
    - incomplete_organ: A feature in medical imaging representing the presence of an organ that is not fully formed. It's a binary feature where 0 signifies the absence of an incomplete organ, and 1 signifies the presence of an incomplete organ.
- Data Types: The data types are appropriate with integer and float types.
- Unique Values: There are 3,147 unique patients, 4,711 unique series and the incomplete_organ column has binary values (0 or 1) indicating the absence or presence of an incomplete organ in the imaging.

Columns
movieId: A unique identifier for each movie.
imdbId: The identifier of the movie in the IMDb system.
tmdbId: The identifier of the movie in the TMDB system.

# RESEARCH QUESTIONS

* How effective are AI algorithms in automatically detecting traumatic injuries to internal abdominal organs like the liver, kidneys, spleen, and bowel using CT scans?

* What features and patterns in CT scans are most indicative of different severities of abdominal injuries, and how can they be utilized for automated injury grading?

* What are the appropriate metrics for evaluating the performance of the developed AI algorithms in terms of both machine learning benchmarks and clinical utility?
# Univariate EDA
![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/c73c987f-4a13-4984-b97c-438d80739f36)
-  We used a countplot to get a clear and easy-to-understand visualization of the distribution of different injury types in the 'labels' dataset
- The data suggests that extravasation (active bleeding) is more frequently identified in the provided images as compared to bowel injuries.
![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/57857ce4-519a-4b47-b873-881521ff8f42)
- We plotted a countplot above to help illustrae the distribution of 'Any Injury' instances in the training dataset and get insights into the **class distribution of our potential target variable.** 
- This analysis revealed a notable prevalence of cases without injuries ('Any Injury'=0) compared to instances indicating the presence of injuries ('Any Injury'=1).
# Bivariate EDA
![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/f726df92-058d-470a-a07f-da287cf706d0)
We used a grouped bar chart to compare 'Bowel Injury' and 'Extravasation Injury' based on the presence or absence of any injury.
n cases with any injury ('any_injury=1'), 'Bowel Injury' is slightly more prevalent compared to cases without injury.
in cases with any injury, 'Extravasation Injury' is significantly more prevalent than cases without injury
![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/a154a14d-5cdd-4317-8cc0-aadfc949c56b)
- We also plotted **stacked bar charts,** to examine the distribution of different organ statuses ('Kidney Status,' 'Liver Status,' and 'Spleen Status') based on the presence of any injury.

     **1. Kidney Status Analysis:**

     In the presence of any injury, instances of healthy kidneys are notably predominant, while occurrences of low kidney function are slightly more frequent than high kidney function instances. **This observation underscores the prevalence of normal kidney status among patients with abdominal injuries, with a very small fraction displaying kidney abnormalities.**

     **2. Liver Status Analysis:**
     
     When any injury is present, healthy liver instances are the most prevalent, with cases of low liver attenuation surpassing those with high liver attenuation. **This suggests that among patients with abdominal injuries, the majority exhibit a healthy liver status. A smaller proportion demonstrates lower liver attenuation, and an even smaller fraction showcasing higher liver attenuation.**

     **3. Spleen Status Analysis:** 
     
     Similarly, in the presence of any injury, healthy spleen instances are predominant. Instances of low spleen attenuation are slightly more prevalent than those with high spleen attenuation. **This highlights the prominence of normal spleen status among patients with abdominal injuries, with a minor fraction showing lower and higher attenuation levels.**
  ![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/2d7291fa-59f7-4476-9b8f-075f9a126d6f)
  - We plotted **a heatmap** to help identify relationships between binary patient features and the severity of abdominal injuries (indicated by 'aortic_hu') as well as the presence of incomplete organs. Positive values indicate a positive correlation, while negative values indicate a negative correlation.
- Features like 'liver_healthy', 'extravasation_healthy', and 'bowel_injury' have noticeable correlations with 'aortic_hu' meaning they might be crucial indicators of injury severity.
- Correlation between 'kidney_low' and 'kidney_high' with incomplete organ suggest a positive relationship between kidney injuries and the incompleteness of the organ.
- The heatmap therefore helped to identify specific features strongly correlated with injury severity that would aid in refining our model.
- # Image Preprocessing
- ![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/6eab3f57-d50c-4dba-8c6e-2f49af1243aa)
- - We preprocessed the image above through rescaling, histogram equalization, smoothing and padding to get a clearer visual than the original image. 
- We rescaled the images to the range of (0, 1) to ensure that all of the images are in the same scale and that the model is not biased towards images with higher or lower pixel values.
- We also used histogram equalization to improve the contrast of the images and make the different shades of gray more distinct. 
- Gaussian smoothing was applied as a type of image filter to reduce noise in our images.
- We finally padded the images with zeros to ensure they had a consistent size for our model training. 
- **By preprocessing our images, we can help enhance the accuracy and robustness of our model. We also ensure that the model learns to identify the important features in the images, rather than being distracted by noise and other irrelevant details.**





# Modelling
- Our third model was the best performing
  ![image](https://github.com/Kinya01/Abdominal-Trauma-Detection-Capstone-Project/assets/128283613/3ba8d24f-d857-4e8c-bf8c-699e3d329def)
  75/75 [==============================] - 51s 682ms/step - loss: 3.4111 - output_0_loss: 0.6918 - output_1_loss: 0.6408 - output_2_loss: 0.5498 - output_3_loss: 0.6477 - output_4_loss: 0.8810 - output_0_accuracy: 0.5275 - output_0_precision: 0.5304 - output_1_accuracy: 0.6927 - output_1_precision: 0.6946 - output_2_accuracy: 0.8813 - output_2_precision: 0.8821 - output_3_accuracy: 0.8147 - output_3_precision: 0.8158 - output_4_accuracy: 0.6830 - output_4_precision: 0.6850
Bowel Accuracy: 0.5275 | Bowel Precision: 0.5304
Extra Accuracy: 0.6927 | Extra Precision: 0.6946
Liver Accuracy: 0.8813 | Liver Precision: 0.8821
Kidney Accuracy: 0.8147 | Kidney Precision: 0.8158
Spleen Accuracy: 0.6830 | Spleen Precision: 0.6850

**Best Hyperparameters:**
    - Learning Rate: 3.841017210511828e-05
    - Dropout Rate: 0.4
    - Weight Decay: 4.597469246271629e-05
- **Insights:**
    - General Trends: Model 3 showcases a trade-off between accuracy and precision. While accuracy dropped slightly in some organs, precision values increased, indicating a **reduction in false positives.**
    - Consistent Performance: Model 3 also demonstrates consistent accuracy and precision across both validation and test datasets. The accuracies and precisions for all classes are stable, indicating reliable predictions.
    - Bowel Performance: Significant drop in accuracy and precision. This might be due to the model becoming overly cautious, leading to more false negatives.
    - Liver and Kidney: Despite minor accuracy drops, precision increased, suggesting a decrease in false positives. This is crucial in medical imaging to avoid unnecessary interventions.
    - Spleen Improvement: Spleen accuracy improved, indicating better generalization. Precision increase is notable, potentially indicating fewer false positives, which is vital in critical diagnoses.


     
# Results and Conclusion
## **Conclusion**

- **Injury Presence in the presence of Any injury:** Our analysis highlighted the prevalence of specific injury in the presence of any abdominal injury. Bowel injury and extravasation injury tend to be more common when any abdominal injury is detected. This can help medical professionals identify common injury combinations for more targeted assessments.
- **Severity differences:** Liver low severity was prominent with liver high being least reccuring. Understanding these severity patterns will play a crucial pattern in the classification and priority cases for medical treatment.
- **Incomplete Organ Instances:** The presence of incomplete organs, though relatively rare, was noted. This underscores the importance of developing models that can accurately diagnose injuries even in cases where organ visibility might be compromised due to incomplete imaging data.
- **Class Relationships:** Our analysis showcased relationships between different injury types, highlighting, for instance, the completeness of organs in cases of bowel and extravasation injuries. Understanding these relationships can guide the model's focus on specific injury types and associated organ statuses.
- **Patterns in CT Scans:** The scan images revealed subtle differences in hyperdensity, potentially indicating injury severity. These insight suggests the importance of capturing intricate patterns in abdominal trauma, indicating the need for advanced image processing techniques.
- **Spleen Injury Complexity:** All models encountered challenges in spleen injury classification. Despite improvements, accurately detecting spleen injuries remained a significant hurdle, indicating a need for advanced approaches specific to this class.
- **Complexity of Aortic Hounsfield Units (HU):** The analysis of Aortic HU distributions provided insights into the variation in CT scan values. Though not used for our modelling in this project, understanding the complexity of these values, including outliers and skewed distributions, is essential for developing algorithms that can accurately interpret these variations, further aiding in injury severity assessment.
- **Class Imbalance Impact:** Addressing class imbalance significantly improved model performance, ensuring accurate predictions across various organ injuries.
- **Precision Over Accuracy:** Emphasizing precision, especially in a medical context, led to the reduction of false positives, crucial in avoiding unnecessary interventions and treatments.
- **Model Complexity:** While a more complex architecture like DenseNet121 was employed, careful attention to tuning and understanding the trade-offs between accuracy and false positives played a pivotal role in the model's success.
- **Consistency and Reliability:** Model 3 emerged as the optimal choice due to its balanced accuracy, enhanced precision, and consistent performance across various classes and datasets. It will provided a reliable tool for medical professionals in critical diagnoses.
- 

## **RECOMMENDATIONS**
- **Utilization of Injury Combinations for Targeted Assessments:** Leveraging the knowledge of common injury combinations, such as bowel and extravasation injuries in the presence of any abdominal injury is essential for more focused and efficient assessments.
- **Account for Incomplete Organ Instances:** To work closely with practitioners to enhance models that can accurately diagnose injuries even when organ visibility is compromised using additional imaging techniques or supplementary tests.
- **Focus on Addressing Spleen Injury Challenges:** Allocate research efforts specifically to address challenges in spleen injury classification. Experimenting with algorithms and considering multidisciplinary approaches for accurate spleen injury detection will be helpful.
- **Consider Aortic Hounsfield Unit Complexity:** Stay informed about the complexity of Aortic Hounsfield Units (HU). Understanding its variations and skewed distributions, will aid in the development of future, better performing algorithms.
- **Explainable AI:** Implementing techniques for explainable AI to provide insights into how the model arrives at its predictions. This transparency is vital to build trust and confidence with the medical practitioners.
