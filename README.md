# PA_04-Data-Wrangling---Data-Visualization

#### ECE Board Exam Problem. 
This program analyzes the ECE Board Exam dataset from the .xlsx file  using pandas for data wrangling and matplotlib for visualization with the following aim:  <br />

(1) Create a filtered dataframes based on specific conditions. <br />
(2) Compute for mean average grades on Math, Electronics, & GEAS. <br />
(3) Visualize whether track, gender, or hometown contribute to higher average scores. <br />

#### Analysis
Based on the provided data, none of the factors (track, gender, or hometown) contribute to a significantly higher average score, as the averages across all groups are remarkably similar.

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

