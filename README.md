# DNSC6301-Group-23
### Basic Information

* **Person or organization developing model**: Charles Bloomer, `charlesbloomer@gwu.edu`, Rui Cheng, `ruicheng@gwu.edu`, Manu Sharma, `manusharma@gwu.edu`
* **Model date**: August 23, 2021
* **Model version**: 1.0
* **License**: MIT
* **Model implementation code**: [DNSC_6301_Group_23_Project_fin.ipynb](DNSC_6301_Group_23_Project_fin.ipynb) 

### Intended Use
* **Primary intended uses**: This model is an *example* probability of default classifier, with an *example* use case for determining eligibility for a credit line increase.
* **Primary intended users**: Students in GWU DNSC 6301 bootcamp.
* **Out-of-scope use cases**: Any use beyond an educational example is out-of-scope.

### Training Data

* Data dictionary: 

| Name | Modeling Role | Measurement Level| Description|
| ---- | ------------- | ---------------- | ---------- |
|**ID**| ID | int | unique row indentifier |
| **LIMIT_BAL** | input | float | amount of previously awarded credit |
| **SEX** | demographic information | int | 1 = male; 2 = female
| **RACE** | demographic information | int | 1 = hispanic; 2 = black; 3 = white; 4 = asian |
| **EDUCATION** | demographic information | int | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| **MARRIAGE** | demographic information | int | 1 = married; 2 = single; 3 = others |
| **AGE** | demographic information | int | age in years |
| **PAY_0, PAY_2 - PAY_6** | inputs | int | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| **BILL_AMT1 - BILL_AMT6** | inputs | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005 |
| **PAY_AMT1 - PAY_AMT6** | inputs | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005 |
| **DELINQ_NEXT**| target | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time |

### Evaluation Data:
* **Source of training data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **How training data was divided into training and validation data**: 50% training, 25% validation, 25% test
* **Number of rows in training and validation data**:
  * Training rows: 15,000
  * Validation rows: 7,500

### Test Data:
* **Source of test data**: GWU Blackboard, email `jphall@gwu.edu` for more information
* **Number of rows in test data**: 7,500
* **State any differences in columns between training and test data**: None

### Model details:
* **Describe potential uncertainties relating to the impacts of using your model**:
* **Columns used as inputs in the final model**: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'
* **Column(s) used as target(s) in the final model**: 'DELINQ_NEXT' 
* **Type of model**: Decision tree
* **Software used to implement the model**: Google Colab
* **Version of the modeling software**: 0.22.2.post1
* **Hyperparameters or other settings of your model**: ccp_alpha=0.0, class_weight=None, criterion='gini',
                       max_depth=6, max_features=None, max_leaf_nodes=None,
                       min_impurity_decrease=0.0, min_impurity_split=None,
                       min_samples_leaf=1, min_samples_split=2,
                       min_weight_fraction_leaf=0.0, presort='deprecated',
                       random_state=13579, splitter='best' 

### Quantitative analysis:
* **Metrics used to evaluate your final model**: AUC 
* **State the final values of the metrics for all data: training, validation, and test data**: 
  * Training value: 0.78230
  * Validation value: 0.757357
  * Test value: 0.7407
* **Provide any plots related to your data or final model -- be sure to label the plots!**:
#### histograms
<br />![image](https://user-images.githubusercontent.com/89318472/131156406-969f2612-a75a-41ce-b256-310cacc1e829.png)
#### Correlation Heatmap
<br />![image](https://user-images.githubusercontent.com/89318472/131156470-80afc3b9-2bfd-42db-891f-1a891cfa12aa.png)
#### Tree depth vs. training and validation AUC 
<br />![image](https://user-images.githubusercontent.com/89318472/131156632-acb5b072-7ec8-4047-afe8-7dc6c40c813d.png)
#### Variable importances
<br />![image](https://user-images.githubusercontent.com/89318472/131156689-05385ae6-1f37-44e6-a144-1f137fc696ec.png)
#### Graph: Tree depth vs. training and validation AUC and AIR
<br />![image](https://user-images.githubusercontent.com/89318472/131156712-1b68b411-ae05-4b42-bc6d-a59d0070e23a.png)
#### Table: Tree depth vs. training and validation AUC and AIR
<br />![image](https://user-images.githubusercontent.com/89318472/132133974-60ff2616-f66c-472d-b6ec-85528e27aed9.png)



### Ethical considerations:
* **Describe potential negative impacts of using your model**:
  * Math or software problems: The model is "underspecified" and is likely to underperform in real-world practice. Changing the random seed of the model strongly affects the performance and results of an AIR higher than 0.8.
  * Real-world risks: The hispanic-to-white AIR could jump to more generalized conclusions about race or exclude other races from the model. The data in the model could show that race is tied too closely with other variables like sex, marriage, etc., and may not be as considerate of any outlier data that would show a different conclusion.
* **Describe potential uncertainties relating to the impacts of using your model**:
  * Math or software problems: The data set used for the model is an example of a poor data set for building models. The model is created as a project submission on the provided data and should not be used for practice. It only has a small number of customers and, all of the signal is in one variable, PAY_0.
  * Real-world risks: A major uncertainty regarding the impact of using the model is how it can display whether or not Hispanic people in the data set would be able to get a loan. This data model can’t be used as an all-inclusive way to show correlation between Hispanic and/or white people getting a loan.
* **Describe any unexpected or results**:
  * This model cannot fix the bias. It can only remediate it, or to be specific, increase the tolerance with a higher estimated probability. Only by fixing the calculation of "phat" can we fix the bias problem of the model.
  * The model results can be significantly different with different seeds. This is probably because the dataset is not big enough and the importance of "PAY_0" is way higher than the rest of 18 variables. Below are some examples:

| **Seed** | 13579 | 24680| 12345|
| ---- | ------------- | ---------------- | ---------- |
|**hispanic-to-white AIR**| 0.75 | 0.88 | 0.76 |
| **black-to-white AIR** | 0.79 | 0.85 | 0.82 |
| **better cutoff** | 0.16 | 0.19 | 0.18
