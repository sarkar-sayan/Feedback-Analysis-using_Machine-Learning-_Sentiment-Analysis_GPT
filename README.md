# Feedback-Analysis-using-Machine-Learning_NLP_GenerativeAI
Analysis of any survey feedback data obtained from client or customer and classifying it into Positive/Negative while determining which Negative feedback has greater importance.
Also generating a detailed feedback on the output with Employee's performance in focus and on the matters to improve. 

# Survey Feedback Analysis : Positive or Negative

## Overview
This project aims to classify survey feedbacks into two categories: positive and negative based on their feedback content. We'll use Python for the implementation.

## Table of Contents
1. Introduction
2. Dataset
3. Data Preprocessing
4. Model Building
5. Evaluation
6. Feedback Generation
7. Conclusion

## Introduction
When a company analyzes surveys for of productivity, it aims to distinguish between employees that contribute positively to work-related tasks and those that do not. Here’s why such classification is needed:

### 1. Quality Improvement:
__Insight into Employee Performance__: Customer feedback provides valuable insights into how employees interact with customers. It highlights areas where employees excel and areas needing improvement.  
__Identify Training Needs__: By analyzing feedback, you can identify specific training needs for employees. For instance, if customers consistently mention issues related to product knowledge, additional training sessions can address this gap.

### 2. Customer Satisfaction and Retention:
__Enhance Customer Experience__: Positive interactions lead to higher customer satisfaction. Analyzing feedback helps you understand what contributes to positive experiences.  
__Address Pain Points__: Negative feedback points out pain points in customer interactions. Addressing these issues can prevent customer churn and improve retention.

### 3. Employee Engagement and Morale:
__Recognize and Appreciate Employees__: Positive feedback allows you to recognize and appreciate employees who consistently provide excellent service. This boosts morale and engagement.  
__Address Employee Concerns__: Negative feedback may highlight employee dissatisfaction or challenges. Addressing these concerns improves overall employee well-being.

### 4. Business Reputation and Brand Image:
__Word of Mouth__: Satisfied customers share positive experiences, contributing to positive word-of-mouth marketing.  
__Mitigate Negative Impact__: Addressing negative feedback promptly helps mitigate any damage to your brand reputation.

### 5. Data-Driven Decision Making::
__Quantitative Metrics__: Metrics like Net Promoter Score (NPS), Customer Satisfaction Score (CSAT), and Customer Effort Score (CES) provide quantifiable data for decision-making.  
__Prioritize Actions__: Analyzing feedback helps prioritize actions based on impact and urgency.

In summary, analyzing customer feedback on employee interactions is essential for continuous improvement, customer satisfaction, employee engagement, and maintaining a positive brand image.

## Dataset
For this project, a self-created dataset is used, but you can procure any from Kaggle itself, just remember to replace the labels in the code accordingly.  
Sample dataset used:
![image](https://github.com/user-attachments/assets/807c3403-1a0d-4173-a8a9-8237d5feaf9a)


## Data Preprocessing
Read the [repo_logs](https://github.com/sarkar-sayan/feedback_analysis-using-machine_learning_nlp_generativeAI/blob/main/repo_logs) file first for better understanding.
##### 1. Data Cleaning:
First and foremost, basic EDA to drop unnecessary rows and columns and remove null values etc. Process differs according to different survey data.
##### 2. ```preprocess_text(text)```:
This function preprocesses text by:  
Converting it to lowercase.  
Removing punctuation.  
Splitting it into tokens (words).  
Filtering out stop words (common words like “the,” “and,” etc.).  
The cleaned text is returned.  
##### 3. ```translate_text_if_needed(text)```:
If the input text is not in English, this function attempts to translate it to English using the detect and translator libraries.  
If translation fails or the text is already in English, it returns the original text.  


## Model Building
#### 1. Train-Test Split:
The data is split into training and testing sets using train_test_split.  
The training set (X_train, y_train) will be used to train the model, and the testing set (X_test, y_test) will be used for evaluation.  
I've set a test size of 20% and a random seed for reproducibility.  
#### 2. Model:
Classifier used: __Logistic Regression__
* Define ```ColumnTransformer``` to separate numerical and text data processing.
* Use ```StandardScaler``` to scale the numerical data.
* Use ```Tf-IDf Vectorizer``` to tokenize the textual data.
Define a pipeline of both the ```ColumnTransformer``` and ```LogisticRegression```.
This pipeline will be our combined classifier for this data.
#### 3. Model Training:
I've chosen the ```LogisticRegression``` classifier for my model. //RandomForestClassifier is supposed to work but gives bad results//   
The model is trained using the training data (X_train, y_train).  

## Evaluation
I’ve made predictions on the test set using ```model.predict(X_test)```.  
The accuracy of the model is calculated using ```accuracy_score(y_test, y_pred)```.  
The printed output shows the accuracy, precision, recall, F1-score, and support for each class (positive and negative).  
#### Interpretation:
An accuracy of 1.0 indicates that the model perfectly predicts the test data.  
The precision, recall, and F1-score are also 1.0 for both classes, suggesting excellent performance.  

## Feedback Generation
First and foremost, define a function ```def predict_feedback_proba()``` to return both the positive and negative predicted probability of the survey data.  
The positive and negative predict probability of the survey data from the classifier is to influence the generated feedback from the GenAI model.
I leveraged an API Key from ```GroqCloud```, which is based on the model ```"llama3-8b-8192"```, but you can use OpenAI provided that there might be some compatibility issue with "httpx" version being outdated.
Define a function ```def generate_detailed_feedback()``` which will take in numerical & textual data and both the probabilities as input paramaters and return a generated chat feedback for the same.
Give appropriate prompt for your chat completion.

## Conclusion
In this project, we’ve explored survey data related to employee productivity, aiming to distinguish between positive contributors and those who are not. Here’s how this work can have real-world influence:  
__Employee Productivity Insights__:  
By analyzing survey responses, organizations can identify patterns and gain insights into employee productivity.  
Understanding which factors contribute positively or negatively allows companies to make informed decisions, improve work environments, and enhance overall performance.  
* Logistic Regression: It is a powerful classification algorithm commonly used in machine learning. It models the probability of a binary outcome (e.g., positive/negative sentiment, spam/not spam) based on input features. In our project, we leveraged Logistic Regression to classify survey responses, achieving excellent accuracy.  
* Generative AI (Gen AI): Generative AI models, like the one I used for feedback generation, creates new content based on existing data. Gen AI can be harnessed for various tasks, including text generation, image synthesis, and creative writing. In our case, we used Gen AI to generate chat feedback based on both numerical and textual data.


---

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
