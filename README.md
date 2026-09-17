# PA#4
### Name: AGAPITO, Catalino D.R.
### Section: 2ECE-C
### Date Submitted: September 17, 2026

In this experiment, three different data-wrangling and visualization tasks were performed on the ECE Board Exam 2 dataset to demonstrate the use of Pandas for filtering, selecting, and summarizing tabular data. Each part focuses on a different data operation — filtering rows by multiple categorical conditions, constructing focused DataFrames by selecting relevant columns, and summarizing the relationship between a categorical feature and a numerical variable. The activities also show how to organize and visualize specific information from a dataset while keeping the original DataFrame unchanged. Through these tasks, the ECE Board Exam 2 dataset can be examined more easily, and the required information can be selected and presented according to the given instructions.

## Problem A: Visayas Communication DataFrame
In this problem, the ECE Board Exam 2 dataset is filtered to keep only students whose Hometown is Visayas and whose Track is Communication. The goal is to demonstrate how multiple categorical conditions can be applied to a source dataset before selecting the relevant columns.

````
import pandas as pd
````

````
ece = pd.read_excel('board2.xlsx')
ece
````
This loads the Pandas library so its functions can be used. `pd.read_excel('board2.xlsx')` reads the Excel file and stores it in a variable called `ece`. The line `df = ece` creates a simple alias so the rest of the notebook can refer to the dataset as `df`, which matches the naming used in the lab manual. Displaying `df` shows the full table of 30 students with their Name, Gender, Track, Hometown, Math, Electronics, GEAS, and Communication (Average) scores.

````
# A. VISAYAS COMMUNICATION DATAFRAME
# Filter BOTH conditions first, THEN select columns
VisComm = df[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')][
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]

print("VisComm DataFrame:")
display(VisComm)

print(f"\nNumber of rows in VisComm: {VisComm.shape[0]}")
````

In this part, the dataset is filtered so that only students whose Hometown is Visayas and whose Track is Communication remain. Two conditions are applied together, one checking if the Hometown column equals "Visayas" and the other checking if the Track column equals "Communication", and they are joined with the ampersand operator so a row must satisfy both to be kept. The filtering is done on the source dataset first before any columns are chosen, which follows the manual. After filtering, only the five required columns, Name, Gender, Math, Electronics, and Average, are retained in that order. The result is stored in a variable called VisComm and displayed as a table, showing the five matching students (S11, S12, S18, S22, and S28) with their scores. Finally, the number of rows is printed using the first value of its shape attribute, which reports five rows.

## Problem B: Visayas Female DataFrame

In this problem, the dataset is filtered to keep only students whose Hometown is Visayas and whose Gender is Female. The goal is to demonstrate how a focused DataFrame can be built from two categorical conditions and then further filtered numerically without overwriting the original result.

````
# B. VISAYAS FEMALE DATAFRAME
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][
    ['Name', 'Track', 'GEAS', 'Electronics', 'Average']
]
display(VisFemale)
````

In this part, the dataset is filtered so that only students whose Hometown is Visayas and whose Gender is Female remain. Two conditions are applied together, one checking if the Hometown column equals "Visayas" and the other checking if the Gender column equals "Female", and they are joined with the ampersand operator so a row must satisfy both to be kept. After filtering, only the five required columns, Name, Track, GEAS, Electronics, and Average, are retained in that order. The result is stored in a variable called VisFemale and displayed as a table, showing the six matching students (S6, S11, S21, S22, S24, and S26) with their scores.

````
VisFemale_high = VisFemale[VisFemale['Average'] >= 60]
display(VisFemale_high)
````

A second filter is then applied to VisFemale, this time checking whether the Average column is greater than or equal to 60. This keeps only the students whose average score meets the threshold. The result is stored in a new variable called VisFemale_high instead of overwriting VisFemale, which follows the manual's instruction to keep the original DataFrame unchanged. The filtered DataFrame is then displayed, showing four remaining students (S6, S11, S21, and S26) after S22 and S24 are dropped because their averages are below 60.




## Problem C: Category-Average Visualization

In this problem, the mean of the Average score is computed for every category of three features — Track, Gender, and Hometown — and the results are displayed as three bar charts in a single figure. The goal is to demonstrate how a categorical feature can be summarized against a numerical variable and how the comparison can be communicated through a clearly labeled plot.
