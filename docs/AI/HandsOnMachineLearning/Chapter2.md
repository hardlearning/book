# Chapter 2. End-to-End Machine Learning Project

## Look at the Big Picture

### Select a Performance Measure

A typical performance measure for regression problems is the *root mean square error* (RMSE). It gives an idea of how much error the system typically makes in its predictions, with a higher weight given to large errors. 

$$
\mathrm{RMSE}(\mathbf{X},\boldsymbol{h})=\sqrt{\frac{1}{m}\sum_{i\operatorname{=}1}^{m}(\boldsymbol{h}(\mathbf{x}^{(i)})-y^{(i)})^{2}}
$$

- m is the number of instances in the dataset you are measuring the RMSE on.
- $\mathbf{x}^{(i)}$ is a vector of all the feature values (excluding the label) of the ith instance in the dataset, and $y^{(i)}$ is its label (the desired output value for that instance).
- $\mathbf{X}$ is a matrix containing all the feature values (excluding labels) of all instances in the dataset. There is one row per instance, and the $i^{th}$ row is equal to the transpose of $\mathbf{x}^{(i)}$, noted $(\mathbf{x}^{(i)})^T$.⁠
- h is your system’s prediction function, also called a hypothesis. When your system is given an instance’s feature vector $\mathbf{x}^{(i)}$, it outputs a predicted value $\hat y^{(i)}=h(\mathbf{x}^{(i)})$ for that instance.
- RMSE(X,h) is the cost function measured on the set of examples using your hypothesis h.

If there are many outlier districts. In that case, you may consider using the mean absolute error (MAE, also called the average absolute deviation).

$$
\mathrm{MAE}(\mathbf{x},\boldsymbol{h})=\frac1m\sum_{i=1}^m|h(\mathbf{x}^{(i)})-y^{(i)}|
$$

- Computing the root of a sum of squares (RMSE) corresponds to the Euclidean norm: this is the notion of distance we are all familiar with. It is also called the $l_2$ norm, noted $||\cdot||_2$
- Computing the sum of absolutes (MAE) corresponds to the $l_1$ norm, noted $||\cdot||_1$. This is sometimes called the Manhattan norm because it measures the distance between two points in a city if you can only travel along orthogonal city blocks.
- More generally, the ℓk norm of a vector v containing n elements is defined as $||\mathbf{v}||_k=(|v_1|^k+|v_2|^k+...+|v_n|^k)^{1/k}$. $l_0$ gives the number of nonzero elements in the vector, and $l_{\infty}$ gives the maximum absolute value in the vector.

The higher the norm index, the more it focuses on large values and neglects small ones. This is why the RMSE is more sensitive to outliers than the MAE. But when outliers are exponentially rare (like in a bell-shaped curve), the RMSE performs very well and is generally preferred.

## Get the Data

### Take a Quick Look at the Data Structure

The info() method is useful to get a quick description of the data.

You can find out what categories exist and how many districts belong to each category by using the value_counts() method.

```python
>>> housing["ocean_proximity"].value_counts()
<1H OCEAN     9136
INLAND        6551
NEAR OCEAN    2658
NEAR BAY      2290
ISLAND           5
Name: ocean_proximity, dtype: int64
```

The describe() method shows a summary of the numerical attributes.

The 25%, 50%, and 75% rows show the corresponding percentiles: a percentile indicates the value below which a given percentage of observations in a group of observations fall.

You can call the hist() method on the whole dataset, and it will plot a histogram for each numerical attribute:

```python
import matplotlib.pyplot as plt

housing.hist(bins=50, figsize=(12, 8))
plt.show()
```

## Create a Test Set

To have a stable train/test split even after updating the dataset, a common solution is to use each instance’s identifier to decide whether or not it should go in the test set (assuming instances have unique and immutable identifiers).

```python
from zlib import crc32

def is_id_in_test_set(identifier, test_ratio):
    return crc32(np.int64(identifier)) < test_ratio * 2**32

def split_data_with_id_hash(data, test_ratio, id_column):
    ids = data[id_column]
    in_test_set = ids.apply(lambda id_: is_id_in_test_set(id_, test_ratio))
    return data.loc[~in_test_set], data.loc[in_test_set]
```

Unfortunately, the housing dataset does not have an identifier column. The simplest solution is to use the row index as the ID:

```python
housing_with_id = housing.reset_index()  # adds an `index` column
train_set, test_set = split_data_with_id_hash(housing_with_id, 0.2, "index")
```

If you use the row index as a unique identifier, you need to make sure that new data gets appended to the end of the dataset and that no row ever gets deleted. If this is not possible, then you can try to use the most stable features to build a unique identifier.

```python
housing_with_id["id"] = housing["longitude"] * 1000 + housing["latitude"]
train_set, test_set = split_data_with_id_hash(housing_with_id, 0.2, "id")
```

Scikit-Learn provides a function train_test_split() to split datasets into multiple subsets in various ways. First, there is a random_state parameter that allows you to set the random generator seed. Second, you can pass it multiple datasets with an identical number of rows, and it will split them on the same indices:

```python
from sklearn.model_selection import train_test_split

train_set, test_set = train_test_split(housing, test_size=0.2, random_state=42)
```

This is called stratified sampling: the population is divided into homogeneous subgroups called strata, and the right number of instances are sampled from each stratum to guarantee that the test set is representative of the overall population.

The following code uses the pd.cut() function to create an income category attribute with five categories (labeled from 1 to 5); category 1 ranges from 0 to 1.5 (i.e., less than $15,000), category 2 from 1.5 to 3, and so on:

```python
housing["income_cat"] = pd.cut(housing["median_income"],
                               bins=[0., 1.5, 3.0, 4.5, 6., np.inf],
                               labels=[1, 2, 3, 4, 5])

housing["income_cat"].value_counts().sort_index().plot.bar(rot=0, grid=True)
plt.xlabel("Income category")
plt.ylabel("Number of districts")
plt.show()
```
