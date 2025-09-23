# PA_04-Data-Wrangling---Data-Visualization

### ECE Board Exam Problem. 
This program analyzes the ECE Board Exam dataset from the .xlsx file  using pandas for data wrangling and matplotlib for visualization with the following aim:  <br />

(1) Create a filtered dataframes based on specific conditions. <br />
(2) Compute for mean average grades on Math, Electronics, & GEAS. <br />
(3) Visualize whether track, gender, or hometown contribute to higher average scores. <br />

#### Analysis
Based on the provided data, none of the factors (track, gender, or hometown) contribute to a significantly higher average score, as the averages across all groups are remarkably similar.

***

#### Functions Utilized in Pandas
```
pd.read_excel("file.xlsx")   - loads Excel file into a DataFrame
df[condition][columns]       - filters rows based on condition, selects specific columns
mean(axis=1)                 - computes row-wise average across given columns
groupby("column")["col2"]    - groups data by a feature and computes aggregate stats (e.g., mean)
```

#### Functions Utilized in MatPlotLib
```
groupby("Column")["Average"].mean()  - groups & computes average
plot(kind="bar")                     - creates bar plots
plt.subplots()                       - arranges graphs side by side
rot = 0                              - makes the label on x-axis in a horizontal orientation
plt.tight_layout()                   - prevents overlapping of visuals
```

---
## Code Overview

##### 1. Data Loading (Instru)

This code block import pandas to allow the utilisation of data wrangling and data visualization. Moreover, read_excel ensures that .xlsx file is fed directly in a Data Frame for data analyszation.
```
# Loads the pandas library
import pandas as pd

# Reads the Excel file "board2.xlsx"
df = pd.read_excel("board2.xlsx")
```

##### 2. Data Filtering (Instru)

This code block filters the .xlsx file to look for the following conditions: Instrumentation, Luzon, and Scores in Electoronics greater than 70. The selected data are then displayed as a separate table. This then is saved as "Instru.csv."
```
Instru = df[
(df["Track"] == "Instrumentation") &
(df["Hometown"] == "Luzon") &
(df["Electronics"] > 70)
][["Name", "GEAS", "Electronics"]]


# Save filtered results to CSV
Instru.to_csv("Instru.csv")
Instru
```

##### 3. Addition of 'Average' Column

This code block computes for the mean scores (Math, Electronics, GEAS, & Communications) of students and stores it to a separate column. This is done in preparation for another filtering of  data. <br>
axis=1 computes row-wise averages
```
# Create a new column 'Average' as the mean of Math, Electronics, GEAS, and Communication
df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)
```

##### 4. Data Filtering (Mindy)

This code block filters the .xlsx file to look for the following conditions: Mindanao, Female, an Average Score of atleast 55. The selected data are then displayed as a separate table. This then is saved as "Mindy.csv."
```
Mindy = df[
(df["Hometown"] == "Mindanao") &
(df["Gender"] == "Female") &
(df["Average"] >= 55)
][["Name", "Track", "Electronics", "Average"]]

# Save filtered results to CSV
Mindy.to_csv('Mindy.csv')
Mindy
```

##### 5. Groupby 

This codeblock imports matplotlib to allow the creation of graphs to have a visual representation of datas. This also finds the average scores of students but are grouped by Track, Gender, and Hometown. By doing this, it helps user compare categories.

```
# Loads the matplotlib library to this program
import matplotlib.pyplot as plt

# Compute the average scores then groups it by Track, Gender, & Hometown

avg_track = df.groupby("Track")["Average"].mean()
avg_gender = df.groupby("Gender")["Average"].mean()
avg_hometown = df.groupby("Hometown")["Average"].mean()
```

##### 6. Visualization

This codeblock creates a to show all three comparisons side by side. This then plot the averages with clear labels and three different colors to differentiate each chart.

```
# Create subplots (1 row, 3 columns)
fig, axes = plt.subplots(1, 3, figsize=(15, 5))


# Plot mean scores by Track
avg_track.plot(kind="bar", ax=axes[0], color="lightskyblue", rot=0)
axes[0].set_title("Average Scores by Track")
axes[0].set_ylabel("Average Score")


# Plot mean scores by Gender
avg_gender.plot(kind="bar", ax=axes[1], color="lightsalmon", rot=0)
axes[1].set_title("Average Scores by Gender")
axes[1].set_ylabel("Average Score")


# Plot mean scores by Hometown
avg_hometown.plot(kind="bar", ax=axes[2], color="lightgreen", rot=0)
axes[2].set_title("Average Scores by Hometown")
axes[2].set_ylabel("Average Score")


# Adjust layout to avoid overlap
plt.tight_layout()
plt.show()
```

Version 03
