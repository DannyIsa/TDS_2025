# Password Strength Prediction

This project uses Kaggle's **Password Strength Dataset** to predict the strength of a given password. Additionally, we employ feature engineering to extract meaningful patterns from the passwords, which help improve the accuracy of the machine learning model. Our goal is to classify passwords as **weak**, **average**, or **strong** based soley on their characteristics, which will be derived from the raw password. We also aim to determine which model performs best, based on what we've learned in the course ["Theory of Data Science"](https://aigner-horev.wixsite.com/eigen/tds) By Dr. Elad Aigner-Horev.
## Table of Contents

1. [Project Overview](#project-overview)
2. [Feature Engineering](#feature-engineering)
   - [Common Sequences](#common-sequences)
   - [Entropy](#entropy)
   - [Diversity](#diversity)
   - [Length](#length)
3. [Machine Learning Models](#machine-learning-models)
4. [Model Evaluation](#model-evaluation)
5. [Conclusion](#conclusion)

## Introduction

Password strength is a critical factor in ensuring security, but often users choose weak passwords that are easy to guess or crack. The Password Strength Dataset from Kaggle provides information on passwords and their corresponding strength labels, making it possible to train machine learning models to predict password strength based on certain features.

This project uses a variety of features derived from the password text to classify passwords as either "weak", "average" or "strong." We focus on extracting characteristics from the password text using feature engineering and then use machine learning models to make predictions.

## Feature Engineering

Feature engineering is an essential part of the project. We have chosen a few key features based on password patterns and characteristics that are correlated with password strength. Below are the features we use in this project:

### Common Sequences

Passwords that use common sequences (e.g., "123456", "qwerty", "password") are generally weak and easy to guess. Based on [research](https://www.codemotion.com/magazine/cybersecurity/the-most-common-passwords-of-2024-weve-all-used-them-at-least-oncecybersecurity) into the most common and vulnerable passwords, we identify certain sequences that are likely to appear in weak passwords.

In total, we create a new binary feature called **sequential**, which counts how many times a password includes any of the following common password sequences:

- `secret`
- `abc`
- `qwe`
- `asd`
- `zxc`
- `123`
- `456`
- `789`
- `pass`
- `111`
- `222`
- `333`
- `444`
- `555`
- `666`
- `777`
- `888`
- `999`

If a password contains atleast one of these sequences, the **sequential** feature is set to `1` (includes a common sequence). Otherwise, it is set to `0` (does not include a common sequence). 

### Entropy

**Entropy** measures the randomness or unpredictability of a password. The higher the entropy, the more complex and harder to guess the password. Entropy is calculated using Shannon's entropy formula.

For each password, we create a new feature called **entropy**, which quantifies the randomness of the password. Higher entropy values correlate with stronger passwords.

### Diversity

A stronger password generally uses a diverse set of characters, including lowercase letters, uppercase letters, digits, and special characters. For the **diversity** feature, we calculate:

- **Lowercase characters**: The number of lowercase letters in the password.
- **Uppercase characters**: The number of uppercase letters in the password.
- **Digits**: The number of numerical digits in the password.
- **Special characters**: The number of special characters (e.g., `@`, `#`, `$`, etc.) in the password.

These counts are used as separate features in the dataset, providing the model with an understanding of the diversity of characters used in the password.

### Length

The length of a password is an important factor in determining its strength. Longer passwords tend to be more secure because there are more possible combinations. We create a feature called **length**, which simply stores the number of characters in each password.

## Machine Learning Models

Once the feature engineering is complete, we use various machine learning algorithms including the ones seen in the course to classify passwords. We use `LazyClassifier`, which automatically trains and evaluates multiple machine learning models with minimal code. The models employed are:

- **LinearSVC**  
- **SGDClassifier**  
- **MLPClassifier**  
- **Perceptron**  
- **LogisticRegression**  
- **LogisticRegressionCV**  
- **SVC**  
- **CalibratedClassifierCV**  
- **PassiveAggressiveClassifier**  
- **LabelPropagation**  
- **LabelSpreading**  
- **RandomForestClassifier**  
- **GradientBoostingClassifier**  
- **QuadraticDiscriminantAnalysis**  
- **HistGradientBoostingClassifier**  
- **RidgeClassifierCV**  
- **RidgeClassifier**  
- **AdaBoostClassifier**  
- **ExtraTreesClassifier**  
- **KNeighborsClassifier**  
- **BaggingClassifier**  
- **BernoulliNB**  
- **LinearDiscriminantAnalysis**  
- **GaussianNB**  
- **NuSVC**  
- **DecisionTreeClassifier**  
- **NearestCentroid**  
- **ExtraTreeClassifier**  
- **CheckingClassifier**  
- **DummyClassifier**  

Each of these models is trained on the password features and evaluated using various performance metrics.


## Model Evaluation

After training the models, we evaluate their performance based on the following metrics:

- **Accuracy**: The proportion of correct predictions.
- **Confusion Matrix**: A matrix showing the performance of the classification model.
- **Classification Report**: Detailed metrics such as precision, recall, and F1-score for each class.

We will also use **cross-validation** to ensure that the models generalize well to new data.

## Conclusion

By applying feature engineering and training machine learning models, we can predict the strength of a given password. The project demonstrates how important features like common password sequences, entropy, character diversity, and length can help differentiate between weak and strong passwords. Using machine learning models, we aim to automate the classification of passwords to improve cybersecurity practices.

The next steps in this project might involve fine-tuning the models, explore additional features, and deploy the solution as a pet-project or even a product that helps users choose a more secure password.