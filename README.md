The objective is to analyze various aspects, such as program satisfaction, in the membership program where customers earn points when making purchases at participating retailers and can later redeem those points as dollar credits toward future purchases.

The simulated dataset consists of 3 data tables: Member Profile Data, Transaction Data, and Rewards Activity Data. 

The Member Profile Data table includes demographic characteristics, program satisfaction rating, and individual store satisfaction rating of each member/customer.

The Sales Activity Data table documents every purchase, including the member who made the purchase, sales transaction amount, points earned, retailer which the purchase is made at, and sales date. 

The Rewards Activity Data documents every points redemption transaction made, including the member who made the redemption, points used, retailer which the points are redeemed at, and redemption date. 
<br><br>

<h2>Data Preprocessing</h2>
I converted binary categorical variables' values from "Y" and "N" to "1" and "0". This is because regression models require variables to be represented numerically so that the model can estimate variable coefficients.

I also removed outlier values from variables. For example, one observation contained a reported age of 119, which is substantially outside the typical age range observed in the dataset and may indicate a data-entry error. To improve data quality and reduce the influence of potentially erroneous observations on the analyses, the record was removed before
conducting statistical tests and modelling on the remaining dataset.

<h2>Exploratory Data Analysis</h2>
There are two main approaches I took to better understand the datasets: generating new variables and analyzing the distribution of some important variables.

<h3>Creating New Variables</h3>
To support subsequent analyses, I created new variables including Current Age, Total Spend Amount, Total Redemption Amount, Purchase Count, Average Transaction Value, and Latest Sales Date. These variables provide additional insights into customer purchasing behaviour, engagement with the loyalty program, and overall customer value.

<h3>Descriptive Statistics</h3>
Firstly, I wanted to understand the overall distribution of key variables within the dataset, such as members' program satisfaction ratings. To achieve this, I used Excel's Descriptive Statistics tool on the Program Satisfaction Rating column in the Member Profile Data table. This allowed me to examine measures such as the mean, median, standard deviation, minimum, and maximum values. It provides me with an initial understanding of overall member sentiment toward the membership program. 

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

<h2>Business Question 2. Factors That Have an Impact on Satisfaction</h2>

The City variable is a categorical variable that can take in more than 2 possible values. Therefore, I chose to use one-way ANOVA F-test to evaluate whether program satisfaction differed across cities, rather than including City directly in the multiple linear regression model.

For the remaining predictor variables, which include newly created variables like Total Sales Amount, they are tested through multiple linear regression (stepwise regression). I chose stepwise regression because I only want to include statistically significant predictor variables in the model, in order to help the model to focus on learning meaningful patterns instead of noise from insignificant variables. 

<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/program_sat_rating%20multiple%20linear%20regression.png" width="500">

Based on the output, program satisfaction tends to be higher among members who do not own a credit card, male members, and members who report higher satisfaction with each of the three participating retailers. Although PurchaseCount is statistically significant (p = 0.003), its coefficient is relatively small compared to the retailer satisfaction variables, suggesting that transaction frequency has a weaker influence on overall program satisfaction. 

Overall, the model has a relatively high R-squared of 0.72, indicating that approximately 72% of the variation in program satisfaction can be explained by the 6 predictor variables included in the model. Furthermore, the model’s p-value (1.4E-1.06) is lower than alpha (0.05), indicating that the model is statistically significant and provides meaningful insights into the factors associated with membership program satisfaction.

<h2>Business Question 3. Identify Customer Spending Tiers to Encourage Higher Total Spending</h2>

I am inspired by Aritzia's Clientele tier structure, which grants members access to its semi-annual store-wide Clientele Sale based on the member's total spending throughout the year. Those in Tier 1 receive the earliest access, those in Tier 2 receive access several days later, while those in the lowest tier do not receive access to the store-wide sale and instead gain access to some discounted items only when the Public Sale begins. Essentially, customers can infer which tier they are in based on when and whether they receive exclusive sale access. They would become incentivized to gain eligibility into a higher tier by spending more money at participating retailers throughout the year.

<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/member%20grouping_tier%20characteristics.png" width="1000">

I segmented members into spending tiers based on their Total Spend Amount and profiled the characteristics of members within each tier, such as whether they own a credit card, which city they live in, and other behavioural characteristics. 

The analysis can help the membership program team determine which members belong in each spending tier when rolling out exclusive deals, rewards, and promotional campaigns.

For example, Tier 1 members are primarily in their 30s and have a relatively balanced gender distribution, suggesting that marketing campaigns should be designed to appeal to both male and female customers rather than focusing on a single demographic group. In addition, Tier 1 members exhibit a relatively even split between credit card owners and non-credit card owners, suggesting that credit card-related promotions may not be the most effective way to engage this segment.

Another interesting observation is that members across the three tiers exhibit relatively similar purchase frequencies. However, Tier 1 members have substantially higher total spending than the other tiers despite making a comparable number of purchases. This suggests that the distinguishing characteristic of Tier 1 members is not how often they shop, but rather how much they spend per transaction. From a business perspective, this may indicate that Tier 1 members are more likely to purchase higher-value products than members in the lower spending tiers.

<img src="https://github.com/w7978708wen/Membership-Program-Analysis-/blob/main/Supporting%20Visuals/member%20grouping_geographic%20distribution.png" width="900">

The analysis can also help the team design operational strategies, such as allocating more high-demand items to physical stores where a larger proportion of Tier 1 members live. This allows high-value members to more conveniently purchase sought-after products in their own city when exclusive sales begin, without having to compete with online shoppers or travel to stores outside their city.

The results show that members across all spending tiers are primarily concentrated in Cities 1 and 4. Although the concentration of Tier 1 members is not substantially different from the other tiers, the findings still support the proposed operational strategy. In this case, I would recommend allocating more high-demand products to stores in Cities 1 and 4, as these locations are likely to experience the highest customer traffic. This increases the likelihood that sought-after products are sold efficiently while also providing a more convenient shopping experience, which may encourage higher customer spending and improve customer satisfaction.

<h2>Limitation to Analysis</h2>

One limitation of this analysis is that many of the derived variables, such as Total Spend Amount, Total Redemption Amount, Purchase Count, and Average Transaction Value, were aggregated across all three participating retailers. As a result, the analyses identify trends at the overall loyalty program level rather than at the individual retailer level.

For example, while Tier 1 members have substantially higher spending than members in the lower tiers, the analysis does not indicate whether this spending is primarily concentrated at a particular retailer.
