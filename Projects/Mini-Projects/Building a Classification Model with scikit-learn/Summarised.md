Mini-Project 2:Building a Classification Model with scikit-learn
- Objective:The objectiveof this assignment is to build a classification model using scikit-learn to predict a binary outcome based on a dataset and evaluate the model's performance.
Instructions:
- Dataset:You can choose a dataset from sklearn'sbuilt-in datasets, or you can select a dataset of your choice from a reliable source. Ensure that the dataset contains both features and a binary target variable (e.g., 0 or 1, Yes or No, etc.). (This step is very very important for learning and hands on.Give students liberty to search and choose the data, it is important for students to find dataset on their own. They will be doing it on a monthly basis in their real job.)
- Using this dataset: https://www.kaggle.com/datasets/uciml/iris/data

Tasks:
- Data Loading:Load the dataset into a pandas DataFrame (if not using a built-in sklearn dataset). Display the first few rows to get a sense of the data.
```
import pandas as pd
Load the dataset
df = pd.read_csv('Iris.csv')

Display the first few rows
print(df.head())
```
This code reads the Iris.csv file into a pandas DataFrame and then prints the first five rows using df.head(). Make sure the Iris.csv file is in the same directory as your script, or provide the full path to the file.

- Data Preprocessing: Perform necessary data preprocessing steps such as handling missing values, encoding categorical variables (if any), and scaling/normalizing numerical features.
```
# Check for missing values
print("\nMissing values in the dataset:")
print(df.isnull().sum())

# Encode the categorical 'Species' column
label_encoder = LabelEncoder()
df['Species'] = label_encoder.fit_transform(df['Species'])

print("\nEncoded 'Species' column:")
print(df['Species'].head())

# Scale the numerical features
scaler = StandardScaler()
df[['SepalLengthCm', 'SepalWidthCm', 'PetalLengthCm', 'PetalWidthCm']] = scaler.fit_transform(
    df[['SepalLengthCm', 'SepalWidthCm', 'PetalLengthCm', 'PetalWidthCm']]
)

print("\nScaled numerical features:")
print(df.head())

# Dropping the 'Id' column as it's not useful for modeling
df.drop(columns=['Id'], inplace=True)

print("\nFinal preprocessed dataset:")
print(df.head())
```
Missing Values: We first check for missing values using df.isnull().sum(), which will give us a count of missing values for each column.\n
Encoding Categorical Variables: The Species column is encoded using LabelEncoder, converting species names into numerical labels.\n
Feature Scaling: We use StandardScaler to scale the numerical features, ensuring they have a mean of 0 and a standard deviation of 1. This is often beneficial for algorithms like k-NN or SVM.
Dropping the Id Column: The Id column is just an identifier and doesn't contain useful information for modeling, so it's dropped.

- Data Splitting:Split the dataset into two parts: a training set (70-80% of the data) and a testing set (20-30% of the data).
```
```  

- Model Selection:Choose at least two classification algorithms from sklearn (e.g., Logistic Regression, Decision Trees, Random Forest, Support Vector Machines, etc.). Train each model on the training data.
```
```  

- Model Evaluation:Evaluate the performance of each model on the testing set using appropriate classification metrics such as accuracy, precision, recall, F1-score, and ROC AUC. Compare the performance of the models and discuss which one performs better.
```
```  

Cross-Validation: Imp

- Hyperparameter Tuning (Optional):If time permits, you can perform hyperparameter tuning on one of the models to see if you can improve its performance. Usetechniques like GridSearchCV or RandomizedSearchCV for this.Conclusion:Summarize your findings. Discuss the strengths and weaknesses of the models you tested. Reflect on the importance of data preprocessing in model performance.
