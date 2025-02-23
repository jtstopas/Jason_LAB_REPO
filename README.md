# Jason_LAB_REPO
M 02 L 01


#python

import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

df = pd.read_csv("data.csv")
df.head()

df.info()

df.describe()

df.isnull().sum()

df.hist(column="Y", bins=20)
plt.xlabel("Y")
plt.ylabel("Frequency")
plt.title("Distribution of Y")
plt.show()

X = df[['X1']]
y = df['Y']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)

mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error: {mse}")

r2_score = model.score(X_test, y_test)
print(f"R² Score: {r2_score}")

df['Predicted_Y'] = model.predict(X)
df.to_csv("processed_data.csv", index=False)