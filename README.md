# Deliberation Intensity

`delibtools` is a Python package for calculating deliberation intensity, primarily designed to process Reddit-like datasets or any conversation threads where the relationships between posts and their arguments need to be analyzed. The package calculates various discourse measures, including argument clustering and argumentativeness, and provides functionality to visualize the results using empirical cumulative distribution functions (ECDF).

## Features

- **Deliberation Intensity Calculation**: Measure the deliberation intensity based on argument clusters and speech patterns.
- **D_Cluster and D_Arg Calculation**: Analyze discourse quality by examining the density of arguments and clusters in conversational threads.
- **Reddit Thread ID Generator**: Assign unique thread IDs for posts based on parent-child relationships (e.g., Reddit's comment system).
- **Empirical Cumulative Distribution Function (ECDF) Plotting**: Visualize and compare deliberation intensity distributions across multiple datasets.

## Installation

You can install the `delibtools` package from PyPI using pip:

```bash
pip install delibtools
```

Or, install directly from the source:

```bash
git clone https://github.com/armaniii/delibtools
cd delibtools
pip install .
```

## Requirements

- Python 3.6+
- `pandas`
- `numpy`
- `tqdm`
- `sentence-transformers`
- `seaborn`
- `matplotlib`
- `scipy`
- `nltk`

## Usage

### 1. **Deliberation Intensity Calculation**

This example demonstrates how to use the `DeliberationIntensity` class to calculate deliberation intensity for a sample dataset.

```python
import pandas as pd
from delibtools import DeliberationIntensity

# Example data
data = {
    'id': ['1', '2', '3', '4'],
    'parent_id': [None, 't3_1', 't1_2', 't1_2'],
    'thread_id': ['1', '1', '1', '1'],
    'text': ['This is a post', 'This is a comment', 'Another comment', 'Yet another comment'],
    'argument': [1, 1, 0, 1],
    'author': ['user1', 'user2', 'user3', 'user2']
}

df = pd.DataFrame(data)

# Initialize the deliberation intensity class
di = DeliberationIntensity(verbose=True)

# Calculate deliberation intensity
dis_df = di.calculate_deliberation_intensity(df)

# View the result
print(dis_df)
```

### 2. **Generating Reddit Thread IDs**

If you're working with Reddit-like data where each post has an ID and a parent ID, you can use the `assign_reddit_threads` function to create thread IDs.

```python
from delibtools import DeliberationIntensity, utils

# Example data
data = {
    'id': ['1', '2', '3', '4'],
    'parent_id': [None, 't3_1', 't1_2', 't1_2']
}

df = pd.DataFrame(data)

# Generate thread IDs
df['thread_id'] = utils.assign_reddit_threads(df)

# View the result
print(df)
```

### 3. **Plotting ECDF for Deliberation Intensity**

The package includes functionality to plot empirical cumulative distribution functions (ECDFs) for comparing deliberation intensity across different datasets.

```python
import pandas as pd
from delibtools import DeliberationIntensity

# Sample data for two datasets
data1 = {'dis': [0.2, 0.3, 0.5, 0.7]}
data2 = {'dis': [0.1, 0.4, 0.6, 0.8]}

df1 = pd.DataFrame(data1)
df2 = pd.DataFrame(data2)

# Initialize the deliberation intensity class
deliberation = DeliberationIntensity(verbose=True)

# Plot ECDF for the two datasets
deliberation.plot_ecdf(df1, df2, labels=['Dataset 1', 'Dataset 2'])
```

## License

This project is licensed under the terms of the **Apache License 2.0**. See the [LICENSE](LICENSE) file for more details.
