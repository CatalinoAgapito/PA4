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
