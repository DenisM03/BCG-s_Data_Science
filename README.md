# BCG's Data Science

## **Project Title : Customer Churn Analysis**

## **Methodology:**

1. Business understanding & problem framing:           
  what is the context of this problem and why are they trying to solve it?            
2. Exploratory data analysis & data cleaning:          
  what data are we working with, what does it look like and how can we make it better?        
3. Feature engineering:         
  can we enrich this dataset using our own expertise or third party information?          
4. Modeling and evaluation:           
  can we use this dataset to accurately make predictions? If so, are they reliable?            
5. Insights & Recommendations:          
  how we can communicate the value of these predictions by explaining them in a way that matters to the business?         

## **1.Business understanding & problem framing:**                 
PowerCo - a major gas and electricity utility that supplies to small and medium sized enterprises.
The energy market has had a lot of change in recent years and there are more options than ever for customers to choose from.
PowerCo are concerned about their customers leaving for better offers from other energy providers. 
This is becoming a big issue for PowerCo and they have engaged BCG to help diagnose the reason why their customers are churning.

**Business understanding**              
Objective: Identify the key factors contributing to customer churn at PowerCo and develop actionable insights to reduce churn rates.                      
Hypothesis: Customers are leaving PowerCo due to factors such as price, customer service quality, energy sources (e.g., clean energy), and competitor offerings.                        

**Data Collection**                
1.Customer data - which should include characteristics of each client, for example, industry, historical electricity consumption, date joined as customer etc.              
2.Churn data - which should indicate if customer has churned            
3.Historical price data – which should indicate the prices the client charges to each customer for both electricity and gas at granular time intervals              

**Work Plan**           
1. We need to define what price sensitivity is and calculate it               
2. We need to prepare the data and engineer features                 
3. Then, we can test our hypothesis using a binary classification model (e.g. Logistic Regression, Random Forest, Gradient Boosted Machines to name a few)                   
4. We would choose a model from one of the tested algorithms based on the model complexity, the explainability, and the accuracy of the models.                 
5. With the trained model, we would be able to extrapolate the extent to which price sensitivity influences churn               

## **2.Exploratory data analysis & data cleaning:** 
This task is focused on exploratory data analysis of the client and price data provided:

**Analysis**

1. We can see from the Visualisations that the churn rate is approximately 10%.This is actually a very good churn rate, the closer the rate is to 0%, the better.             
2. The next series of visualizations were created in an attempt to try and dive deeper into how churn changes based on other factors (using other columns). This is useful for us to investigate because it may help us to understand factors that drive churn.           
3. In the notebook we visualize churn vs. sales channel, contract type, number of products, number of years and origin/contract offer.              
   
    A. We see that for sales channel, there are some sales channels that yield customers churning but there are also other sales channels that have no customers churning.                            
    B. For contract type, we see quite an even split for customers churning. This is interesting because this may suggest that contract type is not a driving factor towards churn rate.  
   
4. Additionally, for some columns their distributions with churn rate included. This is useful for us to understand because based on the distribution of a column, this could affect our feature engineering later.  
5. We look at the distribution of consumption, subscribed power and forecast.                             
    
    A. We notice that the distribution of consumption is very skewed, this is called a positive skew since it is biased towards lower values on the x axis.                        
    B. This is interesting because you may decide to treat this column to reduce the skewness later on during feature engineering. But also because we may want to visualize if there are any outliers within this 
      column.                             
    C. To investigate outliers, we use a boxplot. From the boxplot we can see that with the column as it is there are definitely some outliers. Once again this is interesting because we may choose to remove some 
    of these outliers later.               

## **3.Feature engineering:**
Creating the new features           
"Difference between off-peak prices in December and January the preceding year could be a significant feature when predicting churn”       

**Here is some context around the additional features that have been engineered**    

1. Firstly we have the average price changes across periods. This is a measure of the average price change by company between peak, mid-peak and off peak periods.              
2. We then take this idea one step further by creating another similar feature but instead of looking at the average price difference, we look at the maximum price difference across periods and months. This gives another way to look at the price changes across months.              
3. The reason why these 2 features could be useful is because they are another way of representing the variance of prices throughout the year. Imagine, if your utilities bill massively increased over winter, as a consumer you’d be annoyed and want to find a better deal!             
4. After this we continue feature engineering with some more concepts, including transformation of columns.               
5. To make predictions with a statistical or machine learning algorithm, all of the data must be converted to numeric data types.              
Therefore, we convert date into months and remove the raw date column, as we cannot use it in its original form.                 
6. We also convert boolean columns into binary values.             
And we convert categorical columns into dummy variables. A dummy variable is a binary flag that indicates when a row matches the value from the categorical column that it was created from.                
7. As we saw during exploratory data analysis, the distribution of some columns was skewed. This is important to identify because when modeling data for prediction, based on the technique or algorithm that we use, there are sometimes assumptions within the data that we should follow.               

    A.One common assumption is that the columns within the data are normally distributed. Hence, if we find that columns are not normally distributed, we should treat these columns to try and transform them into 
    a distribution that is more normal.            
8. Therefore, the next thing we do is transform some columns to have a closer to normal distribution. We do this using the logarithm function. As you can see from the visualisations, the newly transformed columns are much closer to a normal distribution than what they were earlier.            
9. Finally, we plot correlations of all the columns to see if we can identify any columns to remove. Columns that have very high correlations indicate an area to look out for. In this case, you may want to remove one of the columns, since they are likely both holding very similar information.               
 
## **4.Modeling and evaluation:**
In our example, we are trying to predict whether or not a client will churn, so it will only ever been 1 of 2 values (True/False, 1/0, etc…).   

If the outcome that we are trying to predict has a fixed number of discrete values, this is a classification problem, as we are trying to “classify” the observations in the data.We used Random Forest classifier.

1.Create train and test samples of the data.     
2.It is important to split the data into train and test samples so then we can measure how well the trained model performs on an unseen set of data.           
3.This is a massively important thing to do when building a predictive model, otherwise we will have no way of measuring how well our model is able to predict churn for new customers!       
4.By adding in values for parameters within the random forest and by fitting the model on the training data, we will have a trained model to predict churn!   

Accuracy: 0.9036144578313253             
Precision: 0.8181818181818182         
Recall: 0.04918032786885246          

## **5.Insights & Recommendations:**

Churn is indeed high in the SME division           
 • 9.7% across 14606 customers     
 
Predictive model is able to predict churn but the main driver is not customer price sensitivity            
 • Yearly consumption, forecasted consumption and net margin are the 3 largest drivers         
 
Discount strategy of 20% is effective but only if targeted appropriately           
 • Offer discount to only to high -value customers with high churn probability       

