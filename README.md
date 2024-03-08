# ASSIGNMENT - LINEAR REGRESSION

#Q1. Create a scatter plot between cylinder vs Co2Emission (green color):

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
df = pd.read_csv("FuelConsumption.csv")
df = pd.read_csv("FuelConsumption.csv")
plt.scatter(df['CYLINDERS'], df['CO2EMISSIONS'], color='green')
plt.xlabel('CYLINDERS')
plt.ylabel('CO2EMISSIONS')
plt.title('CYLINDER vs CO2EMISSION')
plt.show()

```
# OUTPUT:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/d7f29014-a036-4744-bd8b-8569eaf3ba56)

#Q2Using scatter plot compare data   cylinder vs Co2Emission and Enginesize Vs Co2Emission using different colors:
```
# Scatter plot for cylinder vs Co2Emission (green color)
plt.scatter(df['CYLINDERS'], df['CO2EMISSIONS'], color='green', label='CYLINDERS vs CO2EMISSIONS')

# Scatter plot for Enginesize vs Co2Emission (blue color)
plt.scatter(df['ENGINESIZE'], df['CO2EMISSIONS'], color='blue', label='ENGINESIZE vs CO2EMISSIONS')

plt.xlabel('FEATURE')
plt.ylabel('CO2EMISSIONS')
plt.title('Comparison between Cylinder and Enginesize vs Co2Emission')
plt.legend()
plt.show()

```
# ouput:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/f5c324db-3210-4fd2-82e5-e3b6b99f8cdb)

#Q3Using scatter plot compare data   cylinder vs Co2Emission and Enginesize Vs Co2Emission and FuelConsumption_comb Co2Emission using different colors

```
# Scatter plot for cylinder vs Co2Emission (green color)
plt.scatter(df['CYLINDERS'], df['CO2EMISSIONS'], color='green', label='Cylinder vs Co2Emission')
plt.scatter(df['ENGINESIZE'], df['CO2EMISSIONS'], color='blue', label='Enginesize vs Co2Emission')

# Scatter plot for FuelConsumption_comb vs Co2Emission (red color)
plt.scatter(df['FUELCONSUMPTION_COMB'], df['CO2EMISSIONS'], color='red', label='FuelConsumption_comb vs Co2Emission')
plt.xlabel('Feature')
plt.ylabel('Co2Emission')
plt.title('Comparison between Cylinder, Enginesize, and FuelConsumption_comb vs Co2Emission')
plt.legend()
plt.show()

```
# output:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/91e3d89d-8499-47d0-b110-d34c5415a97b)

#Q4 Train your model with independent variable as cylinder and dependent variable as Co2Emission:

```
# Extracting independent and dependent variables
X = df[['CYLINDERS']]
y = df['CO2EMISSIONS']

# Splitting the dataset into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Training the linear regression model
model = LinearRegression()
model.fit(X_train, y_train)

```
# ouput:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/90e3cb05-f563-4c0a-90a0-3ac0deb5f1d7)

#Q5 Train another model with independent variable as FuelConsumption_comb and dependent variable as Co2Emission:

```
# Extracting independent and dependent variables
X = df[['FUELCONSUMPTION_COMB']]
y = df['CO2EMISSIONS']

# Splitting the dataset into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Training the linear regression model
model = LinearRegression()
model.fit(X_train, y_train)


```
# ouput:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/90e3cb05-f563-4c0a-90a0-3ac0deb5f1d7)

#Q6 Train models with different train-test ratios and note down accuracies:

```
# Train models with different train-test ratios and note down accuracies
ratios = [0.2, 0.3, 0.4, 0.5]

for ratio in ratios:
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=ratio, random_state=42)
    model = LinearRegression()
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)
    mse = mean_squared_error(y_test, y_pred)
    r2 = r2_score(y_test, y_pred)
    print(f"Train-Test Ratio: {1-ratio}:{ratio}, MSE: {mse}, R^2 Score: {r2}")

```
#ouput:
![image](https://github.com/Gokulanbazhagan/ML-ASSIGNMENT1/assets/119518996/78b81368-9f07-4cc8-adda-e4dedc5c8f26)




