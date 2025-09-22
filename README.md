# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
~~~
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import PolynomialFeatures

df = pd.read_csv(r"C:\Users\admin\Downloads\asiacup.csv")

YEAR_COL = "Year"
WICKETS_COL = "Wicket Lost"

df[YEAR_COL] = pd.to_numeric(df[YEAR_COL], errors="coerce")
yearly_wickets = df.groupby(YEAR_COL)[WICKETS_COL].mean().reset_index()
yearly_wickets.rename(columns={YEAR_COL: 'year', WICKETS_COL: 'avg_wickets_lost'}, inplace=True)
yearly_wickets = yearly_wickets[yearly_wickets['year'] >= yearly_wickets['year'].max() - 50]

X = yearly_wickets["year"].values.reshape(-1, 1)
y = yearly_wickets["avg_wickets_lost"].values
X_norm = X - X.min()

linear_model = LinearRegression()
linear_model.fit(X_norm, y)
y_pred_linear = linear_model.predict(X_norm)

poly = PolynomialFeatures(degree=3)
X_poly = poly.fit_transform(X_norm)
poly_model = LinearRegression()
poly_model.fit(X_poly, y)

X_range = np.linspace(X_norm.min(), X_norm.max(), 300).reshape(-1, 1)
X_range_poly = poly.transform(X_range)
y_pred_poly_smooth = poly_model.predict(X_range_poly)

plt.figure(figsize=(10,5))
plt.scatter(X, y, color="blue", label="Actual Data")
plt.plot(X, y_pred_linear, color="red", label="Linear Trend")
plt.xlabel("Year")
plt.ylabel("Average Wickets Lost")
plt.legend()
plt.grid(True)
plt.show()

plt.figure(figsize=(10,5))
plt.scatter(X, y, color="blue", label="Actual Data")
plt.plot(X_range + X.min(), y_pred_poly_smooth, color="green", linestyle="--", label="Polynomial Trend")
plt.xlabel("Year")
plt.ylabel("Average Wickets Lost")
plt.legend()
plt.grid(True)
plt.show()
~~~

### OUTPUT
<img width="572" height="568" alt="image" src="https://github.com/user-attachments/assets/cce038c9-6a40-43f0-b3b5-d5dd1722405b" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
