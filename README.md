The objective is to analyze various aspects, such as program satisfaction, in the membership program where customers earn points when making purchases at participating retailers and can later redeem those points as dollar credits toward future purchases.

The simulated dataset consists of 3 data tables: Member Profile Data, Transaction Data, and Rewards Activity Data. 

The Member Profile Data table includes demographic characteristics, program satisfaction rating, and individual store satisfaction rating of each member/customer.

The Sales Activity Data table documents every purchase, including the member who made the purchase, sales transaction amount, points earned, retailer which the purchase is made at, and sales date. 

The Rewards Activity Data documents every points redemption transaction made, including the member who made the redemption, points used, retailer which the points are redeemed at, and redemption date. 
<br><br>

<h2>Exploratory Data Analysis</h2>
Firstly, I wanted to understand the overall distribution of key variables within the dataset, such as members' program satisfaction ratings. 

<h3>Descriptive Statistics</h3>
To achieve this, I used Excel's Descriptive Statistics tool on the Program Satisfaction Rating column in the Member Profile Data table. This allowed me to examine measures such as the mean, median, standard deviation, minimum, and maximum values. It provides me with an initial understanding of overall member sentiment toward the membership program. 

The descriptive statistics also helps to identify whether ratings are concentrated around a particular range and whether there are unusually low or high ratings (such as 10s and 1s). If there are outliers, this may justify further investigation to better understand differences in customer experiences across the membership base.

<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/program_sat_rating%20descriptive%20statistics.png" width="350">

<h3>Frequency Analysis</h3>
To better understand the dataset, I also find it helpful to visualize the distribution of a key variable using a histogram. While the Descriptive Statistics tool provides summary measures such as the mean and identifies potential outlier values, I also want to understand how ratings are distributed across the membership base. For example, I am interested in seeing how many members gave less common but still frequently occurring satisfaction scores, such as 6s and 9s, rather than focusing only on the most popular ratings.


<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/program_sat_rating%20frequency%20analysis.png" width="500">

<h2>Business Question 1. Demographic Differences in Satisfaction</h2>

I used a one-way ANOVA F-test because I wanted to compare the mean program satisfaction rating across more than two groups (Cities A to F). To prepare the data for the analysis, I created a separate worksheet containing only the City and Program_Satisfaction_Rating columns. I then reorganized the satisfaction ratings into city-specific columns, such as "city_A_rating", so that they could be used as inputs for the ANOVA F-test.
<br><br>
The ANOVA test evaluates whether there is statistically significant evidence that mean satisfaction ratings differ across cities. The null hypothesis states that all cities have the same mean program satisfaction rating, while the alternative hypothesis states that at least one city has a different mean rating.

<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/program_sat_rating%20one-way%20anova%20f-test.png" width="500">

The ANOVA output produced a p-value of 0.97, which is substantially greater than the significance level (α = 0.05). Therefore, I fail to reject the null hypothesis. Based on the sample data, there is insufficient statistical evidence to conclude that program satisfaction differs across cities. This conclusion is also consistent with the output table, which shows relatively similar mean satisfaction ratings across the cities.
<br><br>
From a business perspective, this suggests that customer satisfaction with the membership program is relatively consistent across geographic locations, suggesting that we should explore other factors that may impact membership program satisfaction scores. 


