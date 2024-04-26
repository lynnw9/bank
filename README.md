# Bank
## Understanding the data
The data used in the study represents a total of 17 marketing campaigns conducted by a Portuguese bank between May 2008 and November 2010. 

## Understanding the Features
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 41188 entries, 0 to 41187
Data columns (total 21 columns):
 #   Column          Non-Null Count  Dtype  
---  ------          --------------  -----  
 0   age             41188 non-null  int64  
 1   job             41188 non-null  object 
 2   marital         41188 non-null  object 
 3   education       41188 non-null  object 
 4   default         41188 non-null  object 
 5   housing         41188 non-null  object 
 6   loan            41188 non-null  object 
 7   contact         41188 non-null  object 
 8   month           41188 non-null  object 
 9   day_of_week     41188 non-null  object 
 10  duration        41188 non-null  int64  
 11  campaign        41188 non-null  int64  
 12  pdays           41188 non-null  int64  
 13  previous        41188 non-null  int64  
 14  poutcome        41188 non-null  object 
 15  emp.var.rate    41188 non-null  float64
 16  cons.price.idx  41188 non-null  float64
 17  cons.conf.idx   41188 non-null  float64
 18  euribor3m       41188 non-null  float64
 19  nr.employed     41188 non-null  float64
 20  y               41188 non-null  object 
dtypes: float64(5), int64(5), object(11)
memory usage: 6.6+ MB

Input variables:
### bank client data:
1 - age (numeric)
2 - job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed','services','student','technician','unemployed','unknown')
3 - marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
4 - education (categorical: 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown')
5 - default: has credit in default? (categorical: 'no','yes','unknown')
6 - housing: has housing loan? (categorical: 'no','yes','unknown')
7 - loan: has personal loan? (categorical: 'no','yes','unknown')
### related with the last contact of the current campaign:
8 - contact: contact communication type (categorical: 'cellular','telephone')
9 - month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')
10 - day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
11 - duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
### other attributes:
12 - campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact)
13 - pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)
14 - previous: number of contacts performed before this campaign and for this client (numeric)
15 - poutcome: outcome of the previous marketing campaign (categorical: 'failure','nonexistent','success')
### social and economic context attributes
16 - emp.var.rate: employment variation rate - quarterly indicator (numeric)
17 - cons.price.idx: consumer price index - monthly indicator (numeric)
18 - cons.conf.idx: consumer confidence index - monthly indicator (numeric)
19 - euribor3m: euribor 3 month rate - daily indicator (numeric)
20 - nr.employed: number of employees - quarterly indicator (numeric)

Output variable (desired target):
21 - y - has the client subscribed a term deposit? (binary: 'yes','no')


## Understanding the Task
The task is to build classification models, that takes the first 7 input features to predict output y, indicating whether any given client likely subscribes a term deposit.

## Engineering the Features
The categorical features need to be encoded. I encoded these features into natural numbers, and the output feature into a binary. 

## A Baseline Model
88.7% people did not subscribe the term deposit. Thus, if a model always predicts 0, it will have 88.7% accuracy. 

## Model Comparisons
	Model	                            Train Time	Train Accuracy	Test Accuracy
0	Logistic Regression	                0.145557	0.887054	    0.888220
1	Decision Tree	                    0.068202	0.917743	    0.866175
2	SVM	                                15.798431	0.887281	    0.888220
3	KNN5	                            0.060301	0.890615	    0.878023
4	Logic Regression without marital	0.103753	0.887119	    0.888026
5	Decision Tree without marital	    0.059554	0.908323	    0.872584
6	SVM without marital (prob= true)	105.895593	0.887152	    0.888123
7	KNN5 without marital	            0.061399	0.888026	    0.875886
8	Grid Search Decision Tree	        1.679557	0.887443	    0.887734
9	Grid Search Logistic Regression	    2.834345	0.887119	    0.888026
10	Grid Search KNN	                    305.567775	0.887346	    0.888220
11	Grid Search SVC	                    1739.865253	0.887572	    0.888317

The models' accuracies exhibit little improvement. It is conceivable that there is no apparent link between the input features and the output. Incrase the threshold may increase the likelihood of identifying positive candidate, but most of the positive candidates will still be missed by the models. 
