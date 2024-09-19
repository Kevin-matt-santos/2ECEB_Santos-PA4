# EXPERIMENT 4 DATA WRANGLING AND DATA VISUALIZATION 

### Intended Learning Outcomes:
- To identify the codes and functions needed in cleaning and visualizing data
- To be able to apply and use the different codes and functions in creating a Python program that will be used in data wrangling and data visualization

#### Note: Before doing the experiment make sure you donwlaod the corresponding .xlsx also make sure that the file is in the same folder with your jupyternotebook. 

### ECE BOARD EXAM PROBLEM:
Using data wrangling and data visualization technique with 
storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.

1. Create the following data frames based on the format provided: Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas 


Output: 

<img width="370" alt="image" src="https://github.com/user-attachments/assets/c1fd442b-06af-4580-90ee-cdd15969bf71">


- Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon 

- Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female



2. Create a visualization that shows how the different features contributes to average grade. Does chosen track in college, gender, or hometown contributes to a higher average score?


# For Problem 1.A
### Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon 
1. Download the corresponding xlsx file (board2.xlsx) in order to us the data that is needed.
  
2. Create a jupyter notebook that is in the same location with the downloaded xlsx file.

3. Input 'import pandas as np' to access the Pandase library which is needed beacause Python Data Analysis functions will be used in creating data frame
``` python
import pandas as pd

```

4. Using the read function to load the xlsx files in phyton. 
```   python
#Loading the excel file in Phyton
board = pd.read_excel('board2.xlsx')
board

```


5. With the data frame loaded, using an function to filter the data frame which will only return the values of 'Instrumentation' for 'Track, 'Luzon' for 'Hometown' which will serve as the constants for the other values. Getting the values of 'GEAS' and 'Electronics' values that are greater than 70

``` python
# Creating an table that only loades students Name, GEAS, and Electronics Grade that is above 70
# With the condition that their Track is Instrumentation and Hometown is in Luzon
Instru = board[(board['Track'] == 'Instrumentation')
                &(board['Hometown'] == 'Luzon')
                &(board['Electronics'] >70)][['Name', 'GEAS', 'Electronics']]
Instru
```

6. Saving the file output
``` python

#saving the file
Instru.to_excel('Instru.xlsx', sheet_name='Sheet1')

```


## Expected Outputs
<img width="246" alt="image" src="https://github.com/user-attachments/assets/c113ae8a-2e7d-4d87-95d4-b97d2fce994e">

<img width="197" alt="image" src="https://github.com/user-attachments/assets/cc200435-08cb-43c8-bb89-b1f702acb4a1">


# For Problem 1.B
### Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female

1. Since an 'Average' value of the subjects is needed, we need to make a new coloumn that combines all the subject and use the function Data Wrangling. 
``` python
# Creating another Column that Averages the Grades of each student
board['Average'] = board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis = 1)

```

2. Same as Problem 1a however, we will be getting the values of those who are 'female' in 'Gender' and 'Mindanao' for 'Hometown' serving as constants. We will also include 'Name', 'Electronics' value, and 'Average' values that are equal or greater than 55.
``` python
# Creating an table that only loades students Name, Track, Grade in Electronics, and Average that is greater or equal to 55.
# With the Condition that they are Female and hometown is Mindanao
Mindy = board[(board['Hometown'] == 'Mindanao')
                &(board['Gender'] == 'Female')
                &(board['Average'] >= 55)][['Name', 'Track', 'Electronics', 'Average']]
Mindy

```

3.  Saving the file output
``` python

#save the file 
Mindy.to_excel('Mindy.xlsx', sheet_name='Sheet1')

```

## Expected Output
<img width="305" alt="image" src="https://github.com/user-attachments/assets/5377b146-fb00-4a7a-baa7-a886c23970f8">


# Problem 2
### Create a visualization that shows how the different features contributes to average grade. Does chosen track in college, gender, or hometown contributes to a higher average score? 

1. Start the code by opening the Pandas, Mathplotlib, and Seaborn libraries.
``` python
import pandas as np
import matplotlib.pyplot as plt
import seaborn as sns

```
2. Load the board2.xlsx file


3. Get the average grade for all students subjects since its needed for the data table
``` python
#getting the average grade for all students subjects
average = board[['Math','Electronics','GEAS','Communication']].mean(axis=1)
average

```
4. Getting the average of the four factors for each student in the data frame uisng the mean function axis=1.
``` Python
#Getting the average of all different features (Gender, Hometown, Track)
average2 = board.groupby(['Gender','Track','Hometown'])['average'].mean()
average2

```

5. Make an data frame with three columns that cointain 'Gender', 'Track', and 'Hometown' values of each student and their avergae. 
<img width="263" alt="image" src="https://github.com/user-attachments/assets/c44ebe6c-40df-4615-8171-3f0fd76d0aa6">


## Code and Output for Gender contributing for the High Average
``` python
#Using both matplotlib and seaborn, Making a bar graph that shows the how gender contributes to the higher average score
#colors used [light blue, cyan]
color = ['#ADD8E6','#00FFFF']
#changing the figure width to 4 and height to 7 for aesthetic purposes
plt.figure(figsize=(4, 7))
#Plotting the results for the bar graph
sns.barplot(x='Gender', y='average', data=board, hue='Gender', palette=color)
#Addeding an white grid background
sns.set(style="whitegrid")
#displaying the graph
plt.show()
```
<img width="219" alt="image" src="https://github.com/user-attachments/assets/03964a0a-8d08-4904-9f69-d0488267bb5e">

This is my output for the contribution of 'Gender' to the high average. It shows that the gender male has more contribution compared to female


## Code and Output for Track contributing for the High Average
``` python
#Using both matplotlib and seaborn, Making a bar graph that shows the how the Track contributes to the higher average score
#colors used [orange, yellow, red]
color = ['#FFA500','#FFFF00','#FF0000' ]
#changing the figure width to 7 and height to 6 for aesthetic purposes
plt.figure(figsize=(7, 6))
#Plotting the results for the bar graph
sns.barplot(x='Track', y='average', data=board, hue='Track', palette=color)
#Addeding an white grid background
sns.set(style="whitegrid")
#displaying the graph
plt.show()
```
<img width="385" alt="image" src="https://github.com/user-attachments/assets/b07b5626-6dcc-473c-ba12-4a42ef67f577">

This is my output for the contribution of 'Track' to the high average. It shows that Communication is First, Microelectronics is second, and Instrumentation is last. 


## Code and Output for Hometown contributing for the High Average
``` python
#Using both matplotlib and seaborn, Making a bar graph that shows the how the Hometown contributes to the higher average score
#colors used [Green, light green, Dark green]
color = ['#008000','#90EE90','#006400']
#changing the figure width to 7 and height to 6 for aesthetic purposes
plt.figure(figsize=(7, 6))
#Plotting the results for the bar graph
sns.barplot(x='Hometown', y='average', data=board, hue='Hometown', palette=color)
#Addeding an white grid background
sns.set(style="whitegrid")
#displaying the graph
plt.show()
```
<img width="356" alt="image" src="https://github.com/user-attachments/assets/16742900-d1c5-4705-aa7e-6bd96e08416b">

This is my output for the contribution of 'Hometown' to the high average. It shows that Luzon is First, Mindanao is second, and Visayas is last. 

## Author
Santos, Kevin Matthew L.

## References 
- ECE2112 Lecture Notes by Prof. Engr. Ma. Madecheen S. Pangaliman, MSc and Prof. Engr. Nico John Leo S. Lobos, MSc, ECE, ECT

