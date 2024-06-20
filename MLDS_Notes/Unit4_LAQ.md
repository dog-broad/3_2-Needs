# Visualizing Data

## Visualizing Data: Bar Charts, Line Charts, and Scatterplots

### Bar Charts
**Description:** Bar charts represent categorical data with rectangular bars, where the length or height of each bar is proportional to the value it represents. They are used to compare different categories of data.

**Example:**
Suppose we have data on the number of products sold in different regions in a month.

| Region  | Products Sold |
|---------|---------------|
| North   | 150           |
| South   | 200           |
| East    | 180           |
| West    | 220           |

To visualize this data, a bar chart can be created where each bar's height represents the number of products sold in each region.

**Python Code:**
```python
import matplotlib.pyplot as plt

regions = ['North', 'South', 'East', 'West']
products_sold = [150, 200, 180, 220]

plt.bar(regions, products_sold, color='blue')
plt.xlabel('Region')
plt.ylabel('Products Sold')
plt.title('Products Sold in Different Regions')
plt.show()
```

![](img/2024-06-16-17-42-05.png)


### Line Charts
**Description:** Line charts display data points connected by straight lines. They are used to track changes over short and long periods.

**Example:**
Consider data showing the temperature changes over a week.

| Day       | Temperature (°C) |
|-----------|-------------------|
| Monday    | 20                |
| Tuesday   | 22                |
| Wednesday | 19                |
| Thursday  | 24                |
| Friday    | 23                |
| Saturday  | 25                |
| Sunday    | 22                |

A line chart can illustrate how the temperature changes throughout the week.

**Python Code:**
```python
import matplotlib.pyplot as plt

days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
temperature = [20, 22, 19, 24, 23, 25, 22]

plt.plot(days, temperature, marker='o', color='red')
plt.xlabel('Days')
plt.ylabel('Temperature (°C)')
plt.title('Temperature Changes Over a Week')
plt.show()
```

![](img/2024-06-16-17-42-35.png)

### Scatterplots
**Description:** Scatterplots show the relationship between two variables using dots. Each dot represents an observation in the dataset.

**Example:**
Suppose we have data on the height and weight of individuals.

| Height (cm) | Weight (kg) |
|-------------|-------------|
| 150         | 50          |
| 160         | 60          |
| 170         | 70          |
| 180         | 80          |
| 190         | 90          |

A scatterplot can be used to visualize the correlation between height and weight.

**Python Code:**
```python
import matplotlib.pyplot as plt

height = [150, 160, 170, 180, 190]
weight = [50, 60, 70, 80, 90]

plt.scatter(height, weight, color='green')
plt.xlabel('Height (cm)')
plt.ylabel('Weight (kg)')
plt.title('Height vs Weight')
plt.show()
```

![](img/2024-06-16-17-42-59.png)

<details>

<summary>Other Types of Charts</summary>

## Other Types of Charts


pie charts
```python
products_sold = [150, 200, 180, 220]
regions = ['North', 'South', 'East', 'West']
plt.pie(products_sold, labels=regions, autopct='%1.1f%%')
```

histograms
```python
temperature = [20, 22, 19, 24, 23, 25, 22]
plt.hist(temperature, bins=5)
```

box plots
```python
temperature = [20, 22, 19, 24, 23, 25, 22]
plt.boxplot(temperature)
```

</details>


# NumPy

**NumPy** is a powerful Python library essential for numerical computing. It provides support for large multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays.

## Key Features of NumPy

1. **N-Dimensional Array Object (ndarray)**
   - The core of NumPy is its ndarray, an n-dimensional array of homogeneous data types, which provides fast and efficient operations.

2. **Broadcasting**
   - NumPy's broadcasting allows arithmetic operations on arrays of different shapes, making array operations more intuitive and less verbose.

3. **Vectorization**
   - By eliminating the need for explicit loops, NumPy enables vectorized operations, which are faster and more readable.

4. **Mathematical Functions**
   - NumPy includes a wide array of mathematical functions, from basic operations like addition and multiplication to more complex functions like trigonometric operations and statistical methods.

5. **Linear Algebra**
   - It provides support for linear algebra, random number generation, and Fourier transforms, making it a versatile tool for scientific computing.

6. **Integration with Other Libraries**
   - NumPy serves as the foundation for many other scientific libraries, such as SciPy, pandas, and Matplotlib, enhancing its functionality and usability.

## Installation
You can install NumPy using pip:
```sh
pip install numpy
```

## Basic Examples of Using NumPy

**Creating Arrays**
```python
import numpy as np

# Creating a 1D array
arr1 = np.array([1, 2, 3, 4, 5])
print("1D Array:", arr1)

# Creating a 2D array
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print("2D Array:\n", arr2)
```
> **Output:**  
> 1D Array: [1 2 3 4 5]  
> 2D Array: [[1 2 3]  
>  [4 5 6]]

**Array Operations**
```python
# Element-wise addition
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
result = arr1 + arr2
print("Addition:", result)

# Scalar multiplication
result = arr1 * 3
print("Scalar Multiplication:", result)
```
> **Output:**  
> Addition: [5 7 9]  
> Scalar Multiplication: [3 6 9]  

**Mathematical Functions**
```python
# Trigonometric functions
arr = np.array([0, np.pi / 2, np.pi])
result = np.sin(arr)
print("Sine:", result)

# Statistical functions
arr = np.array([1, 2, 3, 4, 5])
mean = np.mean(arr)
std_dev = np.std(arr)
print("Mean:", mean)
print("Standard Deviation:", std_dev)
```
> **Output:**  
> Mean: 3.0  
> Standard Deviation: 1.41421356  

**Linear Algebra**
```python
# Matrix multiplication
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])
result = np.dot(arr1, arr2)
print("Matrix Multiplication:\n", result)

# Determinant
det = np.linalg.det(arr1)
print("Determinant:", det)
```
> **Output:**    
> Matrix Multiplication: [[19 22]  
>  [43 50]]   
>  Determinant: -2   

**Random Number Generation**
```python
# Generating random numbers
rand_arr = np.random.rand(3, 3)
print("Random Array:\n", rand_arr)

# Random integers
rand_ints = np.random.randint(1, 10, size=(3, 3))
print("Random Integers:\n", rand_ints)
```
> **Output:**  
> Random Array: [[0.69646919 0.28613933 0.22685145]   
>  [0.55131477 0.71946897 0.42310646]  
>  [0.9807642  0.68482974 0.4809319 ]]  
>  
>  Random Integers: [[6 5 4]  
>  [1 5 8]  
>  [1 7 8]]  


**Indexing and Slicing**
```python
arr = np.array([1, 2, 3, 4, 5])

# Slicing
print("Sliced Array:", arr[1:4])

# Advanced indexing
arr2 = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print("Element at (1,2):", arr2[1, 2])
```
> **Output:**  
> Sliced Array: [2 3 4]  
> Element at (1,2): 6  

### Use Cases of NumPy

1. **Data Analysis**: NumPy's array operations are useful for data preprocessing and transformation.
2. **Machine Learning**: Libraries like TensorFlow and PyTorch use NumPy arrays for handling data.
3. **Scientific Computing**: NumPy's support for complex mathematical operations makes it indispensable for researchers and scientists.
4. **Image Processing**: Images can be represented as NumPy arrays for processing and manipulation.


# Dimensionality Reduction

## What is Dimentionality?

**Dimensionality** refers to the number of features or variables in a dataset. High-dimensional data has many features, which can lead to challenges in analysis and interpretation. The more features in a dataset, the more complex the analysis will be. Hence, we need to reduce the dimensionality of the data to make it easier to analyze and interpret. 

## The curse of dimensionality

- Handling the high-dimensional data is very difficult in practice, commonly known as the curse of dimensionality. 
- If the dimensionality of the input dataset increases, any machine learning algorithm and model becomes more complex.
- As the number of features increases, the number of samples also gets increased proportionally, and the chance of overfitting also increases.
- If the machine learning model is trained on high-dimensional data, it becomes overfitted and results in poor performance.
- Hence, it is often required to reduce the number of features, which can be done with dimensionality reduction.

## Approaches to Dimensionality Reduction

Dimension reduction techniques like feature selection and feature extraction are crucial in data preprocessing to reduce the complexity of datasets while retaining relevant information. Here’s an overview of both approaches:


### Feature Selection

Feature selection involves choosing a subset of the most relevant features from the original dataset. This process helps in improving model accuracy, reducing training time, and avoiding overfitting. There are three main methods for feature selection:

1. **Filter method**: 
    In this method, the dataset is filtered, and a subset that contains only the relevant features is taken. Some common techniques of filters method are:

    - Correlation
    - Chi-Square test
    - ANOVA
    - Information gain, etc.

2. **Wrapper method**:
    The wrapper method has the same goal as the filter method, but it takes a machine learning model for its evaluation. In this method, some features are fed to the ML model, and evaluate the performance. The performance decides whether to add those features or remove to increase the accuracy of the model. This method is more accurate than the filtering method but complex to work. Some common techniques of wrapper methods are:

    - Forward Selection
    - Backward Selection
    - Bi-directional Elimination

3. **Embedded method**:
    Embedded methods check the different training iterations of the machine learning model and evaluate the importance of each feature. Some common techniques of Embedded methods are:

    - LASSO
    - Elastic Net
    - Ridge Regression, etc.

### Feature Extraction

Feature extraction involves transforming the original features into a lower-dimensional space. This process is useful when the original features are highly correlated or when the dataset has a large number of features. Some common techniques for feature extraction are:

- Principal Component Analysis
- Linear Discriminant Analysis
- Kernel PCA
- Quadratic Discriminant Analysis, etc.

<details>
<summary> Common Techniques of Dimensionality Reduction </summary>  

a. Principal Component Analysis (PCA)  
b. Backward Elimination  
c. Forward Selection  
d. Score Comparison  
e. Missing Value Ratio  
f. Low Variance Filter  
g. High Correlation Filter  
h. Random Forest  
i. Factor Analysis  
j. Auto-Encoder  

</details>




# NLTK

NLTK (Natural Language Toolkit) is a powerful tool for natural language processing written in Python, designed to help computers understand and interpret human language as it is spoken. It serves as an aid in enabling computers to comprehend and manipulate textual data efficiently.

### Key Features of NLTK:

1. **Installation**:
   - NLTK can be installed on Windows using the command `pip3 install nltk`. Once installed, additional datasets (corpora) need to be downloaded for full functionality.

2. **Tokenization**:
   - Tokenization is the process of breaking down a text into individual words. NLTK provides various tokenization methods, such as word tokenization and sentence tokenization.
   - **Example**: Using `word_tokenize` from `nltk.tokenize`, sentences can be broken into individual words:
     ```python
     from nltk.tokenize import word_tokenize
     word_tokenize('Tutorialspoint.com provides high quality technical tutorials for free.')
     ```
     Output: `['Tutorialspoint.com', 'provides', 'high', 'quality', 'technical', 'tutorials', 'for', 'free', '.']`

3. **Stemming**:
   - Stemming is the process of reducing inflected or derived words to their root form. Performing this process will help in reducing the number of words in a sentence or reducing the vocabulary.
   - **Example**: NLTK includes the `PorterStemmer` class for implementing the Porter Stemming algorithm:
     ```python
     from nltk.stem import PorterStemmer
     word_stemmer = PorterStemmer()
     word_stemmer.stem('writing')
     ```
     Output: `'write'`

4. **Part-of-Speech (POS) Tagging**:  
   - Parts-of-speech tagging is the process of assigning a part-of-speech (POS) tag to each word in a sentence. Thsi method is useful in determining the grammatical structure of a sentence.
   - **Example**: NLTK can automatically tag words in sentences:
     ```python
     import nltk
     from nltk import pos_tag, word_tokenize
     nltk.download('averaged_perceptron_tagger')
     pos_tag(word_tokenize('NLTK is a powerful tool for natural language processing.'))
     ```
     Output: `[('NLTK', 'NNP'), ('is', 'VBZ'), ('a', 'DT'), ('powerful', 'JJ'), ('tool', 'NN'), ('for', 'IN'), ('natural', 'JJ'), ('language', 'NN'), ('processing', 'NN'), ('.', '.')]`



# Rescaling, Python

Rescaling, or scaling of data, is a critical step in data preprocessing when preparing data for machine learning algorithms. It involves transforming numerical features to a common scale, which is essential because many machine learning algorithms make decisions based on the distances between data points. In simple terms, Rescaling data makes sure all numbers are on the same scale, helping algorithms compare them accurately for better predictions.  

Here’s a detailed explanation of rescaling using the Min-Max scaling technique:

## Theory of Rescaling:

### Why Rescale Data?
Machine learning algorithms often calculate distances between data points (e.g., Euclidean distance) as part of their operations. If features have different scales, those with larger ranges can disproportionately influence the learning process. Rescaling ensures that all features contribute equally to the analysis and improves the performance and convergence of the algorithms.

### Min-Max Scaling:
Min-Max scaling is one of the simplest methods for rescaling data. It transforms features to a specified range, typically between 0 and 1. The formula for Min-Max scaling is:

$$
X_{scaled} = \frac{X - X_{min}}{X_{max} - X_{min}}
$$

where:
- $X$ is the original feature value.
- $X_{min}$ is the minimum value of $X$ in the dataset.
- $X_{max}$ is the maximum value of $X$ in the dataset.

This transformation ensures that all values lie within the range [0, 1].

## Steps to Implement Min-Max Scaling:

### 1. Importing Libraries:
```python
from sklearn import preprocessing
import numpy as np
```
- `sklearn.preprocessing` provides utilities for scaling, transforming, and normalizing data.
- `numpy` (imported as `np`) is used for creating and manipulating arrays.

### 2. Creating the Data Array:
```python
x = np.array([[-500.5],
              [-100.1],
              [0],
              [100.1],
              [900.9]])
```
- `x` is a numpy array containing the data points we want to scale.

### 3. Scaling the Array:
```python
minmax_scale = preprocessing.MinMaxScaler(feature_range=(0, 1))
x_scale = minmax_scale.fit_transform(x)
```
- `preprocessing.MinMaxScaler` is initialized with `feature_range=(0, 1)`, specifying the desired range for scaled values.
- `.fit_transform(x)` fits the scaler to the data (`x`) and transforms it to the scaled version (`x_scale`).

### 4. Output:
```python
print("Original Data:")
print(x)
print("\nScaled Data:")
print(x_scale)
```
- The original data (`x`) and the scaled data (`x_scale`) are printed for comparison.


# Data Cleaning and Munging

Data cleaning and munging are critical steps in data preprocessing, ensuring that the data used for analysis and modeling is accurate, complete, and consistent. Let's explore the details of these processes based on the provided notes.

## Data Cleaning

Data cleaning, also known as data cleansing, involves finding and correcting inaccuracies in the data. The primary goal is to identify and remove inconsistencies without deleting necessary data, thereby increasing the data's validity and ensuring high-quality insights. Here are some key activities involved in data cleaning:

1. **Identifying Duplicate Records**: Duplicate data can skew analysis and lead to erroneous conclusions. Removing duplicates ensures that each record is unique.
2. **Filling Empty Fields**: Missing values can be handled by imputing data through various techniques such as mean, median, mode, or using predictive models.
3. **Fixing Structural Errors**: This includes correcting typos, inconsistent capitalization, and formatting issues.
4. **Removing Errors**: Eliminating incorrect or irrelevant data to improve overall data quality.

**Benefits of Data Cleaning**:
- Eliminates errors, reducing costs associated with them.
- Improves data integrity.
- Ensures the highest quality of information for decision-making.

## Data Munging

Data munging, also known as data wrangling, is the process of transforming and mapping data from its raw form into another format to make it more suitable for analysis. It involves a series of steps to clean, structure, and enrich the raw data into a desired format for better usability.

**Steps in Data Munging**:
1. **Converting Data Formats**: Changing data from one format to another to ensure compatibility and ease of use.
2. **Combining Data Sets**: Merging multiple data sources to create a comprehensive dataset.
3. **Rescaling Features**: Standardizing or normalizing data to ensure that it fits a specific range, which is crucial for many machine learning algorithms.

## Data Cleaning and Munging Techniques

1. **Make Text Lowercase**: Converting all text data to lowercase to avoid case sensitivity issues.
   ```python
   text = "This is a Demo Text for NLP using NLTK. Full form of NLTK is Natural Language Toolkit"
   lower_text = text.lower()
   ```
2. **Word Tokenization**: Breaking down sentences into individual words.
   ```python
   import nltk
   text = "This is a Demo Text for NLP using NLTK. Full form of NLTK is Natural Language Toolkit"
   word_tokens = nltk.word_tokenize(text)
   ```
3. **Sentence Tokenization**: Splitting text into individual sentences.
   ```python
   sent_token = nltk.sent_tokenize(text)
   ```
4. **Remove Punctuation**: Eliminating punctuation to clean the text data.
   ```python
   sentence = "Think and wonder, wonder and think."
   words = nltk.word_tokenize(sentence)
   new_words = [word for word in words if word.isalnum()]
   ```
5. **Remove Stopwords**: Filtering out common words that do not carry significant meaning, such as 'is', 'the', 'a', etc.
   ```python
   from nltk.corpus import stopwords
   stopword = stopwords.words('english')
   word_tokens = nltk.word_tokenize(text)
   filtered_words = [word for word in word_tokens if word.lower() not in stopword]
   ```

### Importance of Data Cleaning and Munging

Proper data cleaning and munging are essential for several reasons:
- They enhance the accuracy and integrity of the data.
- They improve the efficiency of data-driven decision-making.
- Clean and well-structured data lead to better analytical outcomes and insights.


# Data Manipulation

Manipulating data involves various techniques to change, alter, and prepare data for analysis and interpretation. The primary goal of data manipulation is to make the data more readable, organized, and useful for decision-making.

## Data Manipulation Techniques

1. **Format Consistency**:
   - Ensuring that data is organized in a unified, orderly manner helps business users make better decisions. Consistent data formats make it easier to compare and analyze information across different datasets.

2. **Historical Overview**:
   - Accessing historical data quickly can assist an organization in making decisions related to deadline projections, team productivity, budget allocations, etc. Historical data analysis can reveal trends and patterns that are crucial for strategic planning.

3. **Improved Efficiency**:
   - By having more organized data, a business can isolate and reduce external variables that may affect overall efficiency. This leads to more accurate and efficient data-driven decision-making.

4. **Rescaling Data**:
   - Scaling data is a crucial step in data preprocessing, especially for machine learning algorithms. Rescaling involves adjusting the range of data features to a specific scale, usually between 0 and 1. This can be done using libraries like `sklearn` in Python. For example, using `MinMaxScaler` to scale a numpy array ensures that the data points are within a consistent range, which is important for algorithms that rely on distance calculations.

5. **Handling High-Dimensional Data**:
   - High-dimensional data can be challenging due to the "curse of dimensionality," where the complexity of the model increases with the number of features. This often leads to overfitting, resulting in poor performance. Techniques such as dimensionality reduction can help manage and simplify high-dimensional data.

### Importance of Data Manipulation

- **Consistent and Organized Data**: Well-organized data ensures that companies have access to reliable and actionable insights. This organization helps in maintaining databases that are easier to query and analyze.
  
- **Data Projection and Interpretation**: Data manipulation allows businesses to project future trends based on historical data. This is vital for business intelligence and strategic planning. It also aids in interpreting complex data, making it possible to derive meaningful insights from diverse and unstructured data sources.

- **Tailored Insights**: By manipulating data, companies can customize their analysis to focus on specific insights. For example, analyzing website traffic data to track the number of visitors over time can help in understanding user behavior and improving website performance.

### Example: Rescaling Features in Python

Here’s a practical example of rescaling features in Python using the `MinMaxScaler` from the `sklearn` library:

```python
from sklearn import preprocessing
import numpy as np

# Creating an array with values
x = np.array([[-500.5], [-100.1], [0], [100.1], [900.9]])

# Initializing the MinMaxScaler
minmax_scale = preprocessing.MinMaxScaler(feature_range=(0, 1))

# Fitting and transforming the data
x_scale = minmax_scale.fit_transform(x)

print("Original Data:\n", x)
print("Scaled Data:\n", x_scale)
```




# Splitting a Dataset Using Scikit-Learn

Splitting a dataset into training and testing sets is a fundamental step in building machine learning models. This allows you to evaluate the performance of your model on a separate set of data that it has never seen before, ensuring that your model generalizes well to new, unseen data. Scikit-Learn, a popular Python library for machine learning, provides an easy way to split datasets. Here’s a detailed explanation using the provided content:

### Step-by-Step Process

1. **Import the Necessary Libraries:**
   First, you need to import the required libraries. Specifically, you need `train_test_split` from `sklearn.model_selection`.

    ```python
    from sklearn.model_selection import train_test_split
    ```

2. **Load the Dataset:**
   Load your dataset into features (X) and labels (y). For instance, if you're using the Iris dataset, you can load it as follows:

    ```python
    from sklearn.datasets import load_iris

    iris = load_iris()
    X = iris.data
    y = iris.target
    ```

3. **Split the Dataset:**
   Use the `train_test_split` function to split your dataset. This function shuffles and splits the data into training and testing sets. You can specify the size of the test set using the `test_size` parameter. The `random_state` parameter ensures reproducibility.

    ```python
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=1)
    ```

    Here, `test_size=0.3` means that 30% of the data will be used for testing, and 70% will be used for training.

4. **Check the Shapes of the Splits:**
   It is a good practice to check the shapes of the resulting splits to ensure that the data has been split correctly.

    ```python
    print(X_train.shape)
    print(X_test.shape)
    print(y_train.shape)
    print(y_test.shape)
    ```

    The output should show that the data has been split according to the specified `test_size`. For example:

    ```
    (105, 4)
    (45, 4)
    (105,)
    (45,)
    ```

### Explanation of Parameters

- **`test_size`:** This parameter determines the proportion of the dataset to include in the test split. It can be a float (between 0.0 and 1.0), an integer (the number of test samples), or `None` (default is 0.25).
- **`random_state`:** This parameter controls the shuffling applied to the data before applying the split. Passing an integer ensures that the split is reproducible.

### Applications

Splitting the dataset is crucial in various applications, such as:

- **Model Evaluation:** Assessing the performance of a machine learning model.
- **Hyperparameter Tuning:** Optimizing the parameters of a model.
- **Cross-Validation:** Enhancing model validation techniques by repeatedly splitting the dataset into different training and testing sets.



