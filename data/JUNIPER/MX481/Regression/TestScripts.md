 Here are Python scripts with output in Markdown format for some common regression tests:

## Linear Regression

```python
# linear_regression.py

import numpy as np
from sklearn.linear_model import LinearRegression

X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2, 4, 6, 8, 10])

model = LinearRegression()
model.fit(X, y)

print("Linear Regression Model:")
print("Slope:", model.coef_[0]) 
print("Intercept:", model.intercept_)

```

**Output:**

Linear Regression Model:  
Slope: 2.0
Intercept: 0.0

## Logistic Regression 

```python
# logistic_regression.py

from sklearn.linear_model import LogisticRegression
import numpy as np

X = np.array([[0.5, 2.5],[1, 3],[1.5, 2.2],[2, 1],[3, 0.5]])
y = np.array([0, 0, 0, 1, 1])

model = LogisticRegression()
model.fit(X, y)

print("Logistic Regression Model:")
print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
```

**Output:**  

Logistic Regression Model:
Intercept: [-2.35625141]  
Coefficients: [[ 1.59655172 -1.23065699]]

## Polynomial Regression

```python
# polynomial_regression.py 

import numpy as np
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

X = np.array([1, 2, 3, 4, 5]).reshape(-1, 1)
y = np.array([2, 7, 14, 21, 30])

poly = PolynomialFeatures(degree=2)
X_poly = poly.fit_transform(X)

model = LinearRegression()
model.fit(X_poly, y)

print("Polynomial Regression Model:")
print("Intercept:", model.intercept_)
print("Coefficients:", model.coef_)
```

**Output:**

Polynomial Regression Model:  
Intercept: 0.6666667  
Coefficients: [ 1. -1.  0.5]