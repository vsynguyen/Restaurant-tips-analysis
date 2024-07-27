# Restaurant-tips-analysis

🍽️ Restaurant Tips Analysis
restaurant.jpg

This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations. We will examine the relationship between different variables and the tips given.

The dataset consists of information from 244 restaurant bills, collected in the US in 1987.

It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.

📥 Data import
First, let's import the needed libraries: Pandas & Matplotlib.


[1]
# PUT YOUR CODE HERE
import pandas as pd
import matplotlib.pyplot as plt
Then load data from the following link: https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv


[2]
# PUT YOUR CODE HERE
df = pd.read_csv('https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv')
🔍 Data exploration
Test sample
Let's take a look at the first 5 rows to be sure, that data is loaded properly:


[3]
0s
# PUT YOUR CODE HERE
df.head(5)

🎉 Great! It seems to be okay.

As you can see each observation represents a customer who left a tip at a restaurant.

We can see information about:

the day it occurred
if it was at lunch or dinner
the total bill
the sex of the person
if they were a smoker or not
the size of the party
Before continuing take a look at a few rows of the data and use info and describe to analyze dataset column types and values.

Column types checking
Show the columns of the dataframe and their types:

[4]
0s
# PUT YOUR CODE HERE
df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 244 entries, 0 to 243
Data columns (total 8 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   id          244 non-null    int64  
 1   total_bill  244 non-null    float64
 2   tip         244 non-null    float64
 3   sex         244 non-null    object 
 4   smoker      244 non-null    object 
 5   day         244 non-null    object 
 6   time        244 non-null    object 
 7   size        244 non-null    int64  
dtypes: float64(2), int64(2), object(4)
memory usage: 15.4+ KB
Ooops... 🤔

We have string columns considered as objects.

image.png

Let's fix their types and make them string:


[5]
# PUT YOUR CODE HERE
df['sex'] = df['sex'].astype(str)
df['smoker'] = df['smoker'].astype(str)
df['day'] = df['day'].astype(str)
df['time'] = df['time'].astype(str)
Check again (output columns and their types):


[6]
0s
# PUT YOUR CODE HERE
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 244 entries, 0 to 243
Data columns (total 8 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   id          244 non-null    int64  
 1   total_bill  244 non-null    float64
 2   tip         244 non-null    float64
 3   sex         244 non-null    object 
 4   smoker      244 non-null    object 
 5   day         244 non-null    object 
 6   time        244 non-null    object 
 7   size        244 non-null    int64  
dtypes: float64(2), int64(2), object(4)
memory usage: 15.4+ KB
Nice! We finished this. Look like we are ready to explore some statistics on the given data.

Basic descriptive statistics
Show a descriptive statistics of the numeric columns:


[7]
0s
# PUT YOUR CODE HERE
df.describe()


Great! Now we know a little more about our data.

➡️ Let's move forward!

💸 Tip value influencers
🚬 Do people who smoke give more tips?
Let's figure out the difference between smokers and non-smokers in terms of their behavior and purchasing habits in public catering establishments.

Separate smokers and non-smokers
Create a new dataframe smokers_df containing only info about smokers.


[17]
# PUT YOUR CODE HERE
yes_smokers_df = df[df['smoker'] == 'Yes']
Check whether everything is okay. Output a test sample (5 random rows):


[18]
0s
# PUT YOUR CODE HERE
df.head(5)

Also create another one dataframe non_smokers_df containing only non-smokers.


[19]
# PUT YOUR CODE HERE
non_smokers_df = df[df['smoker'] == 'No']
Check whether everything is okay. Output a test sample (5 random rows):


[11]
0s
# PUT YOUR CODE HERE
df.head(5)

Compare their measures of central tendency
As we know, measures of central tendency is one of the basic tools, that allow us to compare different datasets as it shows the most typical values.

🌏 Whole dataset
Let's try to calculate measures of central tendency for the whole dataset first.

Calculate them for the 'tip' column through the whole dataset and save them into the following variables:

min => common_tip_min
max => common_tip_max
mean => common_tip_mean
median => common_tip_median

[12]
# YOUR CODE
common_tip_min = df['tip'].min()
common_tip_max = df['tip'].max()
common_tip_mean = df['tip'].mean()
common_tip_median = df['tip'].median()
Let's show the resulting values for whole dataset (we already have the code written for you 😉)


[13]
0s
# Make a list of values
common_values = [common_tip_min, common_tip_max, common_tip_mean, common_tip_median]
# Round all the values to 4 decimal places
common_values = map(lambda x: round(x, 4), common_values)

# Make a dataframe from the list
common_mct = pd.DataFrame(common_values, index=['min', 'max', 'mean', 'median'])
# Output the dataframe
common_mct

🚬 Smokers
Do the same taking into account only smokers. Use the following variables:

min => smokers_tip_min
max => smokers_tip_max
mean => smokers_tip_mean
median => smokers_tip_median

[14]
# YOUR CODE
smokers_tip_min = smokers_df['tip'].min()
smokers_tip_max = smokers_df['tip'].max()
smokers_tip_mean = smokers_df['tip'].mean()
smokers_tip_median = smokers_df['tip'].median()
Let's output the results in the same format.

Make the same dataframe containing the measures of central tendency for smokers as we did for whole dataset. Then output it.


[15]
1s
# YOUR CODE
# Make a list of values
smokers_value = [smokers_tip_min, smokers_tip_max, smokers_tip_mean, smokers_tip_median]
# Round all the values to 4 decimal places
smokers_value = map(lambda x: round(x, 4), smokers_value)

# Make a dataframe from the list
smokers_mct = pd.DataFrame(smokers_value, index=['min', 'max', 'mean', 'median'])
# Output the dataframe
smokers_mct

🚭 Non-smokers
Now repeat it for non-smokers. Use the following variables:

min => non_smokers_tip_min
max => non_smokers_tip_max
mean => non_smokers_tip_mean
median => non_smokers_tip_median

[20]
# YOUR CODE
non_smokers_tip_min = non_smokers_df['tip'].min()
non_smokers_tip_max = non_smokers_df['tip'].max()
non_smokers_tip_mean = non_smokers_df['tip'].mean()
non_smokers_tip_median = non_smokers_df['tip'].median()
Make the same dataframe containing the measures of central tendency for non-smokers as we did for whole dataset. Then output it.


[ ]
# YOUR CODE

📝 Conclusion
Let's show the retrieved results together (we already have the code written for you 😉):


[21]
0s
all_vals_dict = {
    'Common': {'min': common_tip_min, 'max': common_tip_max, 'mean': common_tip_mean, 'median': common_tip_median},
    'Smokers': {'min': smokers_tip_min, 'max': smokers_tip_max, 'mean': smokers_tip_mean, 'median': smokers_tip_median},
    'Non-smokers': {'min': non_smokers_tip_min, 'max': non_smokers_tip_max, 'mean': non_smokers_tip_mean, 'median': non_smokers_tip_median}
}

# Make a dataframe
all_mct = pd.DataFrame(all_vals_dict)
# Output the dataframe
all_mct

Insights based on measures of central tendency comparison:

Insight 1
Insight 1
General conclusion:

Look at histograms
As we already discussed on the last lecture, there are a lot of cases, when comparing the measures of central tendency is not enough.

This is because they only show the most typical values. However, the way data is distributed is equally important. There are situations where measures of central tendency are exactly the same, but due to different distributions, it is incorrect to say that the datasets are similar.

🌏 Whole dataset tips histogram
Plot the histogram for the whole dataset tips distribution.

Use the following settings:

Size: 15 x 5
Color: #74b9ff
X-axis label: Tip value
Y-axis label: Frequency
Chart title: Whole dataset tip values
Gridlines: show

[22]
0s
# YOUR CODE
plt.figure(figsize=(15, 5))
plt.hist(df['tip'], bins=10, color='#74b9ff')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Whole dataset tip values')
plt.grid(True)
plt.show()

🚬 Smokers tips histogram
Plot the histogram for smokers tips distribution.

Use the following settings:

Size: 15 x 5
Color: #ff7675
X-axis label: Tip value
Y-axis label: Frequency
Chart title: Smokers tip values
Gridlines: show

[23]
0s
# YOUR CODE
plt.figure(figsize=(15, 5))
plt.hist(yes_smokers_df['tip'], bins=10, color='#ff7675')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Smokers tip values')
plt.grid(True)
plt.show()

🚭 Non-smokers tips histogram
Plot the histogram for non-smokers tips distribution.

Use the following settings:

Size: 15 x 5
Color: #55efc4
X-axis label: Tip value
Y-axis label: Frequency
Chart title: Non-smokers tip values
Gridlines: show

[24]
0s
# YOUR CODE
plt.figure(figsize=(15, 5))
plt.hist(non_smokers_df['tip'], bins=10, color='#55efc4')
plt.xlabel('Tip value')
plt.ylabel('Frequency')
plt.title('Non-smokers tip values')
plt.grid(True)
plt.show()


⭐ Extra-task with a higher difficulty
Plot all 3 charts in a row in the same cell:


[25]
1s
# YOUR CODE
fig, axes = plt.subplots(1, 3, figsize=(45, 5))

# Plot histogram for the whole dataset
axes[0].hist(df['tip'], bins=10, color='#74b9ff')
axes[0].set_xlabel('Tip value')
axes[0].set_ylabel('Frequency')
axes[0].set_title('Whole dataset tip values')
axes[0].grid(True)

# Plot histogram for smokers
axes[1].hist(smokers_df['tip'], bins=10, color='#ff7675')
axes[1].set_xlabel('Tip value')
axes[1].set_ylabel('Frequency')
axes[1].set_title('Smokers tip values')
axes[1].grid(True)

# Plot histogram for non-smokers
axes[2].hist(non_smokers_df['tip'], bins=10, color='#55efc4')
axes[2].set_xlabel('Tip value')
axes[2].set_ylabel('Frequency')
axes[2].set_title('Non-smokers tip values')
axes[2].grid(True)

# Display the plots
plt.tight_layout()
plt.show()

📝 Conclusion
Insights based on distribution comparison:

Insight 1
General conclusion:

👨👩 Do males give more tips?
Perform the same steps based on the column sex.

📆 Do weekends bring more tips?
Perform the same steps based on the column day.

🕑 Do dinners bring more tips?
Perform the same steps based on the column time.

Colab paid products - Cancel contracts here
Connected to Python 3 Google Compute Engine backend
