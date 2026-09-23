# Taxi-Data-Analysis-Visualization-Using-Python


## 📌 Project Overview

This project is part of the **Data Analytics (DA) Module-End 5 – Python DA Assignment 2: Data Visualization**.

The project focuses on analyzing and visualizing taxi trip data using **Python, Pandas, Matplotlib, and Seaborn**.

The taxi dataset contains information about trip distance, fare, tips, tolls, total amount, payment methods, pickup zones, and pickup boroughs.

The project demonstrates how data cleaning and visualization can be used to identify patterns, distributions, and relationships within taxi trip data.

---

## 🎯 Objectives

The main objectives of this project are:

- Load the Seaborn Taxis dataset.
- Explore the structure and characteristics of the dataset.
- Identify and handle missing values.
- Apply appropriate missing-value imputation techniques.
- Analyze taxi fare and distance patterns.
- Study customer payment behavior.
- Compare trips across pickup boroughs.
- Analyze relationships between numerical variables.
- Create meaningful visualizations using Matplotlib and Seaborn.
- Interpret the visualizations and identify useful insights.

---

## 🛠️ Technologies Used

- **Python**
- **Pandas**
- **Matplotlib**
- **Seaborn**
- **Jupyter Notebook / Google Colab**

---

## 📊 Dataset

The project uses the built-in **Taxis dataset provided by Seaborn**.

The dataset contains information such as:

| Column | Description |
|---|---|
| `pickup` | Pickup date and time |
| `dropoff` | Drop-off date and time |
| `passengers` | Number of passengers |
| `distance` | Trip distance |
| `fare` | Fare amount |
| `tip` | Tip amount |
| `tolls` | Toll amount |
| `total` | Total trip amount |
| `payment` | Payment method |
| `pickup_zone` | Pickup zone |
| `dropoff_zone` | Drop-off zone |
| `pickup_borough` | Pickup borough |
| `dropoff_borough` | Drop-off borough |

### Dataset Loading

```python
import seaborn as sns

df = sns.load_dataset("taxis")
```

---

# 🧹 Data Cleaning

Before performing visualization, missing values were checked and handled appropriately.

### Check Missing Values

```python
df.isnull().sum()
```

### Numerical Columns

Missing values in numerical columns such as `distance`, `fare`, `tip`, `tolls`, and `total` can be handled using the median.

```python
numerical_columns = ['distance', 'fare', 'tip', 'tolls', 'total']

for col in numerical_columns:
    df[col] = df[col].fillna(df[col].median())
```

### Categorical Columns

Missing values in categorical columns were handled using the mode.

```python
categorical_columns = [
    'payment',
    'pickup_zone',
    'dropoff_zone',
    'pickup_borough',
    'dropoff_borough'
]

for col in categorical_columns:
    df[col] = df[col].fillna(df[col].mode()[0])
```

---

# 📈 Visualizations

## 1. Line Chart – Fare Over Time

A line chart was created to visualize how taxi fares change over time.

**X-axis:** Pickup timestamp  
**Y-axis:** Fare

```python
df['pickup'] = pd.to_datetime(df['pickup'])

plt.plot(df['pickup'], df['fare'])
```

### Purpose

To identify fare fluctuations and patterns over the recorded time period.

---

## 2. Bar Chart – Total Fare by Pickup Borough

A bar chart was created to compare the total fare generated from different pickup boroughs.

```python
total_fare_by_borough = df.groupby(
    'pickup_borough'
)['fare'].sum().reset_index()

sns.barplot(
    x='pickup_borough',
    y='fare',
    data=total_fare_by_borough
)
```

### Purpose

To compare total fare across pickup boroughs.

---

## 3. Pie Chart – Trips by Payment Method

A pie chart was used to visualize the proportion of trips made using different payment methods.

```python
payment_counts = df['payment'].value_counts()

plt.pie(
    payment_counts.values,
    labels=payment_counts.index,
    autopct='%1.1f%%'
)
```

### Purpose

To understand customer payment preferences.

---

## 4. Histogram – Distribution of Trip Distance

A histogram was created to visualize the distribution of taxi trip distances.

```python
plt.hist(
    df['distance'],
    bins=30,
    edgecolor='black'
)
```

### Purpose

To understand common trip-distance ranges and the overall spread of distances.

---

## 5. Box Plot – Tip Distribution by Pickup Borough

A box plot was created to compare tip amounts across pickup boroughs.

```python
sns.boxplot(
    x='pickup_borough',
    y='tip',
    data=df
)
```

### Purpose

To compare the distribution, spread, median, and potential outliers in tip amounts.

---

# 📊 Seaborn Visualizations

## 6. Count Plot – Number of Trips by Pickup Borough

A count plot was used to count the number of trips in each pickup borough.

```python
sns.countplot(
    x='pickup_borough',
    data=df
)
```

### Purpose

To identify the number of recorded trips from each pickup borough.

---

## 7. Scatter Plot – Distance vs Fare

A scatter plot was created to study the relationship between trip distance and fare.

```python
sns.scatterplot(
    x='distance',
    y='fare',
    hue='pickup_borough',
    data=df,
    alpha=0.6
)
```

### Purpose

To visualize the relationship between distance and fare and compare trips across pickup boroughs.

---

## 8. Heatmap – Correlation Matrix

A correlation heatmap was created for:

- Distance
- Fare
- Tip
- Tolls
- Total

```python
columns = ['distance', 'fare', 'tip', 'tolls', 'total']

correlation_matrix = df[columns].corr()

sns.heatmap(
    correlation_matrix,
    annot=True,
    cmap='coolwarm',
    fmt='.2f'
)
```

### Purpose

To identify the strength and direction of relationships between numerical variables.

---

## 9. Pair Plot – Pairwise Relationships

A pair plot was created to analyze relationships between:

- Distance
- Fare
- Tip
- Total

The data points were colored according to `pickup_zone`.

```python
pair_columns = [
    'distance',
    'fare',
    'tip',
    'total',
    'pickup_zone'
]

sns.pairplot(
    df[pair_columns].dropna(),
    hue='pickup_zone'
)
```

### Purpose

To visualize multiple pairwise relationships and compare patterns across pickup zones.

---

## 10. Violin Plot – Fare Distribution by Payment Method

A violin plot was created to visualize the distribution of fares for different payment methods.

```python
sns.violinplot(
    x='payment',
    y='fare',
    data=df
)
```

### Purpose

To compare the distribution, density, and spread of fare values across payment methods.

---

# 🔍 Key Analysis Areas

The project focuses on the following analytical areas:

### 💰 Fare Analysis
- Fare trends over time
- Total fare by pickup borough
- Fare distribution by payment method

### 🚕 Trip Analysis
- Number of trips by borough
- Distribution of trip distances
- Relationship between distance and fare

### 💳 Payment Analysis
- Distribution of payment methods
- Fare patterns across payment methods

### 📍 Location Analysis
- Pickup borough comparison
- Pickup zone comparison

### 📊 Statistical Analysis
- Correlation between distance, fare, tip, tolls, and total
- Pairwise relationships between numerical variables

---

# 💡 Insights

The visualizations provide a better understanding of:

- How taxi fares vary over time.
- How trip distance is distributed.
- How many trips originate from different pickup boroughs.
- How customers use different payment methods.
- How distance and fare are related.
- How tips vary across pickup boroughs.
- How numerical taxi variables are correlated.
- How fare distributions differ between payment methods.

The exact findings depend on the values and patterns observed in the generated visualizations.

---

# 📁 Project Structure

```text
Taxi-Data-Visualization/
│
├── Taxi_Data_Visualization.ipynb
├── README.md
└── screenshots/
    ├── line_chart.png
    ├── bar_chart.png
    ├── pie_chart.png
    ├── histogram.png
    ├── box_plot.png
    ├── count_plot.png
    ├── scatter_plot.png
    ├── heatmap.png
    ├── pair_plot.png
    └── violin_plot.png
```

---

# 🚀 How to Run the Project

### Step 1 – Clone the Repository

```bash
git clone <your-github-repository-url>
```

### Step 2 – Install Required Libraries

```bash
pip install pandas matplotlib seaborn
```

### Step 3 – Open the Notebook

Open:

```text
Taxi_Data_Visualization.ipynb
`` **Google Colab**.

### Step 4 – Run the Cells

Run the notebook cells sequentially to:

1. Load the dataset
2. Explore the data
3. Handle missing values
4. Create visualizations
5. Analyze the results

---

# 🎓 Learning Outcomes

Through this project, I learned how to:

- Work with real-world-style taxi data.
- Identify and handle missing values.
- Use Pandas for data preparation.
- Convert timestamp columns into datetime format.
- Create charts using Matplotlib.
- Create statistical visualizations using Seaborn.
- Analyze categorical and numerical variables.
- Understand correlation between variables.
- Compare distributions across categories.
- Interpret visualizations and extract meaningful insights.

---

# 🏁 Conclusion

This project demonstrates the complete workflow of a basic **Data Visualization project using Python**.

The taxi dataset was loaded and cleaned before applying multiple visualization techniques. Matplotlib and Seaborn were used to explore fare, distance, tips, payment methods, and pickup locations.

The project demonstrates how visualizations can transform raw taxi data into understandable patterns and relationships, providing a foundation for further exploratory data analysis.

---

## 👩‍💻 Author

**Dhivya M**

**Data Analytics Learner | Python | Pandas | Matplotlib | Seaborn | Power BI | SQL**

---

## ⭐ Project Skills Demonstrated

`Python` `Pandas` `Matplotlib` `Seaborn` `Data Cleaning` `EDA` `Data Visualization` `Correlation Analysis` `Statistical Visualization` `Data Analysis`
