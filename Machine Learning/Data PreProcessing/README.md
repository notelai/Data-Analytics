# Setup

- This guideline is to get us starting with python.
- This includes installing pip package manager for python.
- Installation of libraries needed for data processing in python.

**Installing pip for python**

- Make sure that we have included python home in path variable of system, this will enable us to use intall pip using command.
- Download pip package from [pip](https://pip.pypa.io/en/stable/installing/)
- Go to the directory in which you have downloaded pip package.
- Execute command python get-pip.py

**You may get this error message**

```
Collecting pip
  Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000027E81D656D8>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/pip/
  Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000027E81D65D30>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/pip/
  Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000027E81D65FD0>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/pip/
  Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000027E81D8D160>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/pip/
  Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.VerifiedHTTPSConnection object at 0x0000027E81D652B0>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/pip/
  Could not find a version that satisfies the requirement pip (from versions: )
No matching distribution found for pip

```

In this case try adding proxy : 

````
D:\>python get-pip.py --proxy="http://url"
````

- Install required libraries

````
python -m pip install --user numpy pandas --proxy="url"
````
# Data PreProcessing

**1. Importing libraries and dataset**

````
import pandas as py
dataset = py.read_csv('Customers.csv')
# select all the rows and all columns except the last column
X = dataset.iloc[ : , :-1].values

# select all the rows data from 3rd column
Y = dataset.iloc[ : , 3].values

````
if we print X and Y, we get below results

````
print(X)
[['France' 44.0 72000.0]
 ['Spain' 27.0 48000.0]
 ['Germany' 30.0 54000.0]
 ['Spain' 38.0 61000.0]
 ['Germany' 40.0 nan]
 ['France' 35.0 58000.0]
 ['Spain' nan 52000.0]
 ['France' 48.0 79000.0]
 ['Germany' 50.0 83000.0]
 ['France' 37.0 67000.0]]
 
print(Y)
['No' 'Yes' 'No' 'No' 'Yes' 'Yes' 'No' 'Yes' 'No' 'Yes']

````
**2. Handling missing values**
 - Data can be missing due to various reasons.
 - Handle missing data so it does not impact the performance of machine learning model.
 - Missing values can be replaced by mean, median or mode of entire column
 - Can use Imputer class from sklearn.preprocessing
 - Getting warning as imputer is marked as deprecated.
 - SimpleImputer can be used in place of Imputer.

````
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
print(X)

output : 

D:\:DeprecationWarning: Class Imputer is deprecated; Imputer was deprecated in version 0.20 and will be removed in 0.22. Import impute.SimpleImputer from sklearn instead. warnings.warn(msg, category=DeprecationWarning)
[['France' 44.0 72000.0]
 ['Spain' 27.0 48000.0]
 ['Germany' 30.0 54000.0]
 ['Spain' 38.0 61000.0]
 ['Germany' 40.0 63777.77777777778]
 ['France' 35.0 58000.0]
 ['Spain' 38.77777777777778 52000.0]
 ['France' 48.0 79000.0]
 ['Germany' 50.0 83000.0]
 ['France' 37.0 67000.0]]
 
````
**3. Handling categorical data**
- Categorical data are variables that contains label values.
- Number of possible values are limited to fixed set.
- For example values like true, false can not be used in mathematical equations of the model, therefore we need to encode these values to numbers.
- To achieve this LabelEncoder class can be used from sklearn.preprocessing package.

````
# Encoding categorical data
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])

onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()

Output :
Our X
[['France' 44.0 72000.0]
 ['Spain' 27.0 48000.0]
 ['Germany' 30.0 54000.0]
 ['Spain' 38.0 61000.0]
 ['Germany' 40.0 nan]
 ['France' 35.0 58000.0]
 ['Spain' nan 52000.0]
 ['France' 48.0 79000.0]
 ['Germany' 50.0 83000.0]
 ['France' 37.0 67000.0]]

is transformed to :

[[1.00000000e+00 0.00000000e+00 0.00000000e+00 4.40000000e+01 7.20000000e+04], 
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 2.70000000e+01 4.80000000e+04],
 [0.00000000e+00 1.00000000e+00 0.00000000e+00 3.00000000e+01 5.40000000e+04],
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 3.80000000e+01 6.10000000e+04],
 [0.00000000e+00 1.00000000e+00 0.00000000e+00 4.00000000e+01 6.37777778e+04],
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 3.50000000e+01 5.80000000e+04],
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 3.87777778e+01 5.20000000e+04],
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 4.80000000e+01 7.90000000e+04],
 [0.00000000e+00 1.00000000e+00 0.00000000e+00 5.00000000e+01 8.30000000e+04],
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 3.70000000e+01 6.70000000e+04]]

````
transforming Y

````
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
print(Y)

Output: 

['No' 'Yes' 'No' 'No' 'Yes' 'Yes' 'No' 'Yes' 'No' 'Yes']

is transformed to:

[0 1 0 0 1 1 0 1 0 1]
````

**4. Splitting dataset in to training and test set**

- We will take partitions of dataset.
- One for training set and other for testing the performance of trained model called test set.
- Generally split is 80:20.
- train_test_split() method from sklearn.cross_validation can be used.

````
from sklearn.model_selection  import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)


Output Analysis : 

print(X_train)

[[0.00000000e+00 1.00000000e+00 0.00000000e+00 4.00000000e+01
  6.37777778e+04]
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 3.70000000e+01
  6.70000000e+04]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 2.70000000e+01
  4.80000000e+04]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 3.87777778e+01
  5.20000000e+04]
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 4.80000000e+01
  7.90000000e+04]
 [0.00000000e+00 0.00000000e+00 1.00000000e+00 3.80000000e+01
  6.10000000e+04]
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 4.40000000e+01
  7.20000000e+04]
 [1.00000000e+00 0.00000000e+00 0.00000000e+00 3.50000000e+01
  5.80000000e+04]]
  
print(X_test)

[[0.0e+00 1.0e+00 0.0e+00 3.0e+01 5.4e+04]
 [0.0e+00 1.0e+00 0.0e+00 5.0e+01 8.3e+04]]
 
print(Y_train)

[1 1 1 0 1 0 0 1]

print(Y_test)

[0 0]
````
**5. Feature Scaling**

````
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.fit_transform(X_test)

Output Analysis : 

print(X_train)
[[-1.          2.64575131 -0.77459667  0.26306757  0.12381479]
 [ 1.         -0.37796447 -0.77459667 -0.25350148  0.46175632]
 [-1.         -0.37796447  1.29099445 -1.97539832 -1.53093341]
 [-1.         -0.37796447  1.29099445  0.05261351 -1.11141978]
 [ 1.         -0.37796447 -0.77459667  1.64058505  1.7202972 ]
 [-1.         -0.37796447  1.29099445 -0.0813118  -0.16751412]
 [ 1.         -0.37796447 -0.77459667  0.95182631  0.98614835]
 [ 1.         -0.37796447 -0.77459667 -0.59788085 -0.48214934]]

print(X_test)

[[ 0.  0.  0. -1. -1.]
 [ 0.  0.  0.  1.  1.]]
````
