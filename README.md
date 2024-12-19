---

# Nobel Prize Analysis

## Overview
The Nobel Prize is one of the most prestigious international accolades, established in 1901. It is awarded annually in the fields of Chemistry, Literature, Physics, Physiology or Medicine, Economics, and Peace. Winners receive a gold medal, a diploma, and a monetary reward. 

This project analyzes the Nobel Prize dataset, exploring trends, milestones, and historical insights about the laureates and their achievements from 1901 to 2023.

## Dataset Description
The dataset was sourced from the Nobel Prize API and includes detailed information about each laureate, including:
- **Year**: The year the Nobel Prize was awarded.
- **Category**: The field of the Nobel Prize (e.g., Physics, Chemistry).
- **Prize**: The name of the specific prize.
- **Motivation**: The official rationale for the award.
- **Prize Share**: The proportion of the prize shared by the laureate.
- **Laureate ID**: A unique identifier for the laureate.
- **Laureate Type**: Indicates whether the recipient is an individual or an organization.
- **Full Name**: The name of the laureate.
- **Birth Information**: Includes birth date, city, and country.
- **Sex**: Gender of the laureate.
- **Organization**: The name, city, and country of the laureate's affiliated institution.
- **Death Information**: Includes death date, city, and country, if applicable.

## Key Analyses
### 1. Most Commonly Awarded Gender and Birth Country
- The most commonly awarded gender is **Male**.
- The most frequent birth country among laureates is the **United States of America**.

### 2. Decade with the Highest Ratio of US-born Laureates
- The **2000s** had the highest ratio of US-born laureates across all categories.

### 3. Decade-Category Combination with the Highest Proportion of Female Laureates
- The **2020s** in the **Literature** category had the highest proportion of female laureates.

### 4. First Female Nobel Prize Laureate and Category
- **Marie Curie, née Sklodowska** was the first woman to win a Nobel Prize, awarded in **Physics**.

### 5. Multiple-Time Nobel Laureates
The following individuals and organizations have won the Nobel Prize more than once:
- **Marie Curie, née Sklodowska**
- **Comité international de la Croix Rouge (International Committee of the Red Cross)**
- **Linus Carl Pauling**
- **Office of the United Nations High Commissioner for Refugees (UNHCR)**
- **John Bardeen**
- **Frederick Sanger**

## Tools and Libraries
- **Python**: Core programming language for data analysis.
- **Pandas**: For data manipulation and cleaning.
- **NumPy**: For numerical calculations.
- **Seaborn**: For data visualization.

## Code Highlights
### Importing Libraries and Loading Data
```python
import pandas as pd
import seaborn as sns
import numpy as np

nobel_data = pd.read_csv('nobel.csv')
nobel_data.head()
```

### Determining Most Commonly Awarded Gender and Birth Country
```python
top_gender = nobel_data['sex'].mode()[0]
top_country = nobel_data['birth_country'].mode()[0]
print(f"Most Commonly Awarded Gender: {top_gender}")
print(f"Most Commonly Awarded Birth Country: {top_country}")
```

### Analyzing US-born Laureates by Decade
```python
nobel_data['decade'] = (np.floor(nobel_data['year']/10)*10).astype(int)
only_usa = nobel_data[nobel_data['birth_country'] == 'United States of America']
max_decade_usa = only_usa.value_counts('decade').idxmax()
print(f"Decade with Highest Ratio of US-born Laureates: {max_decade_usa}")
```

### Female Laureates by Decade and Category
```python
nobel_data['female_winner'] = nobel_data['sex'] == 'Female'
df_female = nobel_data.groupby(['decade', 'category'], as_index=False)['female_winner'].mean()
max_female_decade = df_female.loc[df_female['female_winner'].idxmax()]
print(f"Decade: {max_female_decade['decade']}, Category: {max_female_decade['category']}")
```

### Identifying First Female Laureate
```python
sort = nobel_data[nobel_data['female_winner']]
first_woman_name = sort.sort_values(by='year')['full_name'].values[0]
first_woman_category = sort.sort_values(by='year')['category'].values[0]
print(f"First Female Laureate: {first_woman_name}, Category: {first_woman_category}")
```

### Listing Multiple-Time Nobel Laureates
```python
repeat_list = []
for name in nobel_data['full_name']:
    if name in repeat_list:
        continue
    if nobel_data['full_name'].value_counts()[name] > 1:
        repeat_list.append(name)
print(f"Multiple-Time Laureates: {repeat_list}")
```

## Results and Insights
- **Gender Trends**: While most laureates are male, the proportion of female laureates has increased significantly in recent decades.
- **US Dominance**: The United States has been the most frequent birth country of laureates, especially in the 2000s.
- **Literature Leads for Women**: The 2020s have seen significant contributions by women in Literature.
- **Notable Achievements**: Figures like Marie Curie and Linus Pauling have set remarkable milestones by winning multiple Nobel Prizes.
