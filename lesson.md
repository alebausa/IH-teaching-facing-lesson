# Lesson 1: Objects and Arrays in JavaScript

### Lesson Duration: 3 hours

> Purpose: The purpose of this lesson is to go into detail of arrays and objects, understand the basic concepts of array and object manipulation and data access and introduce some of JavaScript most common array and object methods.

---

### Setup

- All previous set up: VSC with LiveServer extension.

### Learning Objectives

After this lesson, students will be able to:

- Understand how <code>push()</code>, <code>unshift()</code>, <code>pop()</code>, <code>splice()</code> and <code>forEach()</code> work
- Understand how to access the data in nested object and arrays
- Understand the difference between what a method does and what a method returns
- Read official documentation before starting to code

---

### Lesson 0: Review of what we already know

> :clock10: 5 min

- How can we declare a new array
- Property .length of iterable elements
- Access its elements with braket notation and index

<details>
  <summary> Code examples </summary>

```javascript
// Name should be written in plural
const fruits = []

// We can access data with bracket notation
console.log(fruits[0])

// Check length property
console.log(fruits.length)
```

</details>

---

### Lesson 1: Data manipulation in arrays

> :clock10: 20 min

⚠️ Before using any method one should ask themselves first:

1. Does the method modify the original array?
2. What is its return value?
3. Check official documentation for each method before using them: [MDN Web docs](https://developer.mozilla.org/en-US/)

Most common methods to add and retrieve data from arrays:

- <code>arr.push()</code> method: adds at the end of the original array, but returns the length of the array
- <code>arr.unshift()</code> method: adds at the beggining of the original array, but returns the length of the array
- <code>arr.pop()</code> method: retrieves the last element of the original array, and returns the deleted element
- <code>arr.shift()</code> method: retrieves the first element of the original array, and returns the deleted element
- <code>arr.splice()</code> method: add and retrieve as many elements of the original array as you wish. It returns the deleted elements.

<details>
  <summary> Code example 1: simple methods </summary>

```javascript
const students = ['Elisa', 'Guillem']

function updateStudentDatabase() {
  let student = prompt("What's your name?")
  students.push(student)
  return students
}

updateStudentDatabase() // Call the function
students.unshift('Marina')
console.log(students) // Check what happened
students.pop()
console.log(students) // Check what happened
students.shift()
console.log(students) // Check what happened
```

</details>
<details>
  <summary> Code example 2: splice() </summary>

```javascript
const favFoods = ['pizza', 'icecream', 'pasta', 'avocado']

// Two parameters: where do I start deleting (index), how many I delete
favFoods.splice(1, 1)

// Three parameters: where do I start deleting, how many I delete, what I add instead
favFoods.splice(0, 1, 'salad')

// I can access the last element with length -1
favFoods.splice(favFoods.length - 1, 1, 'apple')

// What If I don't know the index of the element I want to retrieve?
let index = favFoods.indexOf('pasta')
console.log(index)
favFoods.splice(index, 1)
```

</details>

---

#### :pencil2: Time to practice!

> :clock10: 20 min (+ 10 min Review)

<details>
  <summary> Click for Instructions: Activity 1 </summary>

- Link to [activity 1](https://github.com/ironhack-edu/data_3.08_activities/blob/master/3.08_activity_1.md).

</details>

<details>
  <summary> Click for Solution: Activity 1 solutions </summary>

- Link to [activity 1 solution](https://gist.github.com/ironhack-edu/253270833e1716fca5d7273469ea757d).

</details>

---

:coffee: **BREAK**

---

### Lesson 2 key concepts

> :clock10: 20 min

Revisit Data Analysis work flow for modeling - 1

- Data acquisition (already performed)
- Exploratory data analysis
- Data Cleaning/wrangling

<details>
  <summary> Click for Code Sample </summary>

```python
data['status'].value_counts()

data.shape

data.dtypes

data.isna().sum()
data = data[data['duration'].isna() == False]

data.describe()

data['duration'] = data['duration'].astype('object') # This will be treated as categorical
data.describe()
data.isna().sum()
```

</details>

<details>
  <summary> Click for Code Sample:  Cleaning Categorical Columns</summary>

```python
data['operation'].value_counts()
def cleanOperation(x):
    x = x.lower()
    if 'vyber' in x:
        return "vyber"
    elif 'prevod' in x:
        return "prevod"
    elif 'vklad' in x:
        return 'vklad'
    else:
        return 'unknown'

data['operation'] = list(map(cleanOperation, data['operation']))
```

```python
data['k_symbol'].value_counts()
data['k_symbol'].value_counts().index
def cleankSymbol(x):
    if x in ['', ' ']:
        return 'unknown'
    else:
        return x

data['k_symbol'] = list(map(cleankSymbol, data['k_symbol']))
data = data[~data['k_symbol'].isin(['POJISTINE', 'SANKC. UROK', 'UVER'])]
```

```python
def clean_type(x):
    if 'PRI' in x:
        return 'PRIJEM'
    else:
        return x

data['type'] = list(map(clean_type, data['type']))
```

</details>

---

#### :pencil2: Check for Understanding - Class activity/quick quiz

> :clock10: 10 min (+ 10 min Review)

<details>
  <summary> Click for Instructions: Activity 2 </summary>

- Link to [activity 2](https://github.com/ironhack-edu/data_3.08_activities/blob/master/3.08_activity_2.md).

</details>

<details>
  <summary> Click for Solution: Activity 2 solutions </summary>

- Link to [activity 2 solutions](https://gist.github.com/ironhack-edu/2946a99a19aa1f86c066e7dd1ffec7fc).

</details>

---

:coffee: **BREAK**

---

### Lesson 3 key concepts

> :clock10: 20 min

Revisit Data Analysis work flow for modeling - 2

- More EDA/data cleaning
- Data pre processing

<details>
  <summary> Click for Code Sample: EDA / Data Cleaning </summary>

```python
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
```

```python
corr_matrix=data.corr(method='pearson')  # default
fig, ax = plt.subplots(figsize=(10, 8))
ax = sns.heatmap(corr_matrix, annot=True)
plt.show()
```

```python
sns.distplot(data['t_amount'])
plt.show()

sns.distplot(data['l_amount'])
plt.show()

sns.distplot(data['balance'])
plt.show()

sns.distplot(data['payments'])
plt.show()
```

</details>

<details>
  <summary> Click for Code Sample: Data preprocessing </summary>

```python
import numpy as np
from sklearn.preprocessing import Normalizer
# from sklearn.preprocessing import StandardScaler

X = data.select_dtypes(include = np.number)

# Normalizing data
transformer = Normalizer().fit(X)
x_normalized = transformer.transform(X)
x = pd.DataFrame(x_normalized)
```

```python
cat = data.select_dtypes(include = np.object)
cat = cat.drop(['status'], axis=1)
categorical = pd.get_dummies(cat, columns=['type', 'operation', 'k_symbol', 'duration'])
```

</details>

---

### :pencil2: Check for Understanding - Class activity/quick quiz

> :clock10: 30 min

<details>
  <summary> Click for Instructions: Activity 3 </summary>

- Link to [activity 3](https://github.com/ironhack-edu/data_3.08_activities/blob/master/3.08_activity_3.md).

</details>

<details>
  <summary>Click for Solution: Activity 3 solutions</summary>

- Link to [activity 3 solution](https://gist.github.com/ironhack-edu/9ca2052231cc1802096e2f0c4eb7e9a9).

</details>

---

### Lesson 4 key concepts

> :clock10: 20 min

Revisit Data Analysis work flow for modeling - 2

- Fitting the model
- Making predictions on the test data
- Check model accuracy

:exclamation: Note to instructor: When we work with multi class classification problem and use Logistic Regression method from `sklearn`, the argument "multi_class" can take different arguments. Discuss the one versus rest method and multinomial mehtod briefly, how they are different.

<details>
  <summary> Click for Code Sample: Train test split </summary>

```python
y = data['status']
X = np.concatenate((x, categorical), axis=1)
```

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.4, random_state=100)
```

</details>

<details>
  <summary> Click for Code Sample: Fitting the model </summary>

- Refer to the documentation
  [https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html]

```python
from sklearn.linear_model import LogisticRegression
classification = LogisticRegression(random_state=0, solver='lbfgs',
                  multi_class='multinomial').fit(X_train, y_train)
```

```python
predictions = classification.predict(X_test)
classification.score(X_test, y_test)
```

```python
print(y_test.value_counts())
# As you would notice here, there is a huge imbalance in the data among the different classes. We will talk more about imbalance and how to resolve it later

pd.Series(predictions).value_counts()
# This shows that the disparity in the numbers are amplified by the model
```

```python
from sklearn.metrics import confusion_matrix
confusion_matrix(y_test, predictions)
```

</details>

---

:coffee: **BREAK**

---

### :pencil2: Practice on key concepts - Lab

> :clock10: 30 min

<details>
  <summary> Click for Instructions: Lab </summary>

- Link to the lab: [https://github.com/ironhack-labs/lab-predictions-logistic-regression](https://github.com/ironhack-labs/lab-predictions-logistic-regression)

</details>

<details>
  <summary> Click for Solution: Lab solutions </summary>

- Link to the [lab solution](https://gist.github.com/ironhack-edu/c3e7fba417de11bcf152ba6329acbbb4).

</details>

---
