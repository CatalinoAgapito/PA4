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

````
mean_by_track    = df.groupby('Track')['Average'].mean()
mean_by_gender   = df.groupby('Gender')['Average'].mean()
mean_by_hometown = df.groupby('Hometown')['Average'].mean()

display("Mean Average by Track:");    display(mean_by_track)
display("Mean Average by Gender:");   display(mean_by_gender)
display("Mean Average by Hometown:"); display(mean_by_hometown)
````

In this part, the mean of the Average column is computed for every category of Track, Gender, and Hometown. This is done using groupby, which splits the rows into groups based on each unique value in a feature column, followed by mean, which averages the Average column within each group. The three results are stored in mean_by_track, mean_by_gender, and mean_by_hometown, then displayed as tables. The Track summary shows Microelectronics highest at 64.4 and Instrumentation lowest at 57.3. The Gender summary shows Female at 63.53 and Male at 60.40. The Hometown summary shows Visayas highest at 64.18, Mindanao at 61.57, and Luzon lowest at 60.17. These numbers are used in the bar charts and interpretation that follow.

## Problem C: Category-Average Visualization

In this problem, the mean of the Average score is computed for every category of three features — Track, Gender, and Hometown — and the results are displayed as three bar charts in a single figure. The goal is to demonstrate how a categorical feature can be summarized against a numerical variable and how the comparison can be communicated through a clearly labeled plot.

````
# Part C-a: mean of Average per category, kept as DataFrames for indexing
mean_by_track    = df.groupby('Track',    as_index=False)['Average'].mean()
mean_by_gender   = df.groupby('Gender',   as_index=False)['Average'].mean()
mean_by_hometown = df.groupby('Hometown', as_index=False)['Average'].mean()
````

````
# C. CATEGORY-AVERAGE VISUALIZATION
#This creates a figure with 3 different subplots
fig, axes = plt.subplots(1, 3, figsize=(16, 5), sharey=True)

#Track
axes[0].bar(mean_by_track['Track'], mean_by_track['Average']) 
axes[0].set_title('Mean Average by Track') #This sets the title
axes[0].set_xlabel('Track') #This sets the label for the x-axis
axes[0].set_ylabel('Mean Average Score') #This sets the label for the y-axis
axes[0].set_ylim(0, 100)

#Gender
axes[1].bar(mean_by_gender['Gender'], mean_by_gender['Average'])
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylim(0, 100)

# Plot 3: Hometown
axes[2].bar(mean_by_hometown['Hometown'], mean_by_hometown['Average'])
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylim(0, 100)

plt.show()
````

In this part, the mean Average score is computed for every category of the three features Track, Gender, and Hometown using groupby combined with mean. The as_index=False option is added so the category labels stay as regular columns and can be accessed by name in the plot. A single figure is then created with three side-by-side subplots using plt.subplots, with sharey=True so all three charts use the same y-axis scale for a consistent comparison. Inside each subplot, the bar function draws a bar per category, using the feature values as x-labels and the computed means as bar heights. Each subplot is labeled with a title, an x-axis label, a shared y-axis label, and a fixed range of 0 to 100 to match the grading scale. Finally, plt.show renders the completed figure.

````
# D. Interpretation: category with highest sample mean per feature
print("Track with highest mean Average:   ",
      mean_by_track.idxmax(), f"({mean_by_track.max():.2f})")
print("Gender with highest mean Average:  ",
      mean_by_gender.idxmax(), f"({mean_by_gender.max():.2f})")
print("Hometown with highest mean Average:",
      mean_by_hometown.idxmax(), f"({mean_by_hometown.max():.2f})")
````

In this part, the category with the highest sample mean is identified for each of the three features. For each summary, idxmax returns the label of the category with the highest mean and max returns that mean value, which are then printed together using an f-string so the value is shown rounded to two decimal places. The output reports that Microelectronics has the highest mean Average among tracks at 64.40, Female has the highest among genders at 63.53, and Visayas has the highest among hometowns at 64.18. These three values describe the observed dataset only, since a difference in group means on its own does not establish that a feature causes a higher board exam score.

