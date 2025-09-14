# Introduction
The growing demand for ride-hailing services like Uber 🚖 generates massive volumes of booking data 📊 that often remain underutilized. Companies face challenges
in understanding ride performance 🏎️, cancellation behavior ❌, customer trends 👥, and payment preferences 💳. This project was designed to address these challenges
by transforming raw ride-booking data 📂 into actionable insights 🔍 through an interactive Power BI dashboard 🖥️. By leveraging advanced visualizations such as KPIs 📌,
trend analyses 📈, cancellation breakdowns 🚫, and payment method distributions 💵, the dashboard enables stakeholders to monitor operations ⚙️, identify pain points 📉,
and improve decision-making 💡. With intuitive navigation 🔘 and slicers 🎛️ for filtering by date 📅 and vehicle type 🚙, the solution empowers managers to evaluate
key performance metrics 📏 and enhance overall operational efficiency 🚀.

🔗 Want to explore the project?
- **🎥 Video Walkthrough (YouTube):** [Watch The Dashboard in Action](https://www.youtube.com/watch?v=pMt3A_Tkm38)
- **📊 Dashboard Preview (PDF):** [uberBI.pdf](uberBI.pdf)
- **📑 Dataset (Excel):** [uberBI.xlsx](uberBI.xlsx)
- **🛠️ Power BI Template (PBIT):** [uberBI.pbit](uberBI.pbit)
# Background
### The Questions I Wanted to Answer Through This Project Were:
1. How many total bookings were made, and how many were successfully completed, canceled, or left incomplete?
2. What percentage of bookings are completed, canceled, or incomplete?
3. Who cancels more rides, customers or drivers, and what are the main reasons?
4. How do ride bookings vary over days, weeks, or months?
5. How does driver arrival time compare with trip duration across different hours of the day?
6. Which vehicle types are most popular among riders?
7. How much distance is traveled by each vehicle category?
8. Which vehicle types generate the highest revenue?
9. Why do customers most frequently cancel rides?
10. Why do drivers most frequently cancel rides?
11. Which payment methods are most preferred by customers?
12. What are the busiest pickup areas for rides?
# Tools I Used
- **📂 Kaggle:** Source of the Uber Rides dataset
- **📝 Excel:** Initial data exploration and cleaning
- **⚡ Power BI:** Data transformation, KPI creation, and interactive dashboard design
- **💻 GitHub:** Documentation and sharing the project
# The Analysis
Each visualization in this dashboard was carefully designed to tackle a specific business problem, transforming raw ride-booking data into meaningful insights.
By aligning every chart with a targeted question, the analysis provides a clear view of ride performance, customer and driver behaviors, operational efficiency, and revenue
streams. But the real question is: how did I answer these challenges? Let’s dive into the insights behind each visualization.
## 1. How many total bookings were made, and how many were successfully completed, canceled, or left incomplete?
In order to provide a quick overview of ride activity and status distribution, I created KPI cards for `Total Bookings`, `Completed Rides`, `Cancelled by Customer`, `Cancelled by Driver`, and `Uncompleted Rides`. Using the `Booking ID` as the unique ride identifier, I applied count aggregations to calculate each total, then split them by `Booking Status`. I customized the visuals by adding icons for clarity, formatting the numbers with “K” units for large values, and applying rounded card shapes consistent with Uber’s brand style. To ensure interactivity, I linked the cards to global slicers for date and vehicle type.
### Insights
The KPIs reveal that out of 16.3M total bookings, about 10.1M rides were successfully completed while nearly 4M rides were lost due to cancellations or incompletions.
Notably, driver-initiated cancellations (2.9M) are more than double those initiated by customers (1.1M), suggesting potential supply-side issues such as driver availability,
incentive structures, or operational inefficiencies. The very low count of incomplete rides (1K) indicates that most issues occur before the trip starts. These insights help
management identify cancellation hotspots and focus efforts on improving driver retention and reliability.

![KPIs](/assets/1-kpi.png)

*This KPI card set represents the overall booking performance, highlighting completed rides, cancellations, and incomplete trips.*
## 2. What percentage of bookings are completed, canceled, or incomplete?
The aim of this visualization is to evaluate the proportion of bookings that are successfully completed versus those that fail due to cancellations or incompletions. To
achieve this, a donut chart was created with `Booking Status` as the legend and `Count of Booking ID` as the value. This approach highlights the percentage share of each
booking outcome.
### Insights
The results show that completed rides form the majority with 62.1% (10.18K), confirming that most bookings reach successful completion. However, a considerable share of
rides fails to convert: cancellations by drivers represent 17.7% (2.9K), cancellations by customers account for 7.1% (1.17K), no driver found cases represent 7.0% (1.14K),
and incomplete bookings make up 6.1% (1K). Overall, this means nearly 38% of bookings remain unfulfilled, with driver-related cancellations being the most critical
contributor to lost rides.

![Donut Chart](/assets/2-bookingStatusDistribution.png)

*This donut chart represents the distribution of booking statuses across all rides.*
## 3. Who cancels more rides, customers or drivers, and what are the main reasons?
In order to determine who cancels more rides and identify the main reasons, I created a stacked bar chart. On the X-axis, I placed `Booking Status` to categorize
rides as completed, cancelled by driver, cancelled by customer, no driver found, or incomplete. On the Y-axis, I used the count of `Booking ID` to measure the number of rides
in each category. I also added `Reason for Cancelling by Driver` and `Reason for Cancelling by Customer` to the tooltips, enabling deeper drill-downs into the specific 
causes of cancellations.
### Insights
The visualization highlights that drivers cancel significantly more rides (≈2.9K) compared to customers (≈1.1K), making driver cancellations the primary source of lost
trips. “No driver found” (≈1.2K) further emphasizes operational gaps in ride availability. These results suggest that the majority of cancellations are on the supply side,
potentially due to driver unavailability or operational inefficiencies, while customer-driven cancellations, though notable, remain secondary. This insight is key for
designing targeted strategies to reduce cancellations and improve service reliability.

![Stacked Bar Chart](/assets/3-rideCancellations.png)

*This bar chart represents ride cancellations by customers and drivers*
## 4. How do ride bookings vary over days, weeks, or months?
In order to analyze how ride bookings vary across days, weeks, or months, I created a line chart. On the X-axis, I placed the `Date` field to capture the time dimension,
while on the Y-axis, I used the `Count of Booking ID` to measure ride activity. To improve readability and highlight booking patterns, I applied a smooth line interpolation,
ensuring the trend was easier to interpret.
### Insights
The chart shows that ride demand peaked notably during May 2024, where bookings consistently reached higher levels, likely due to increased travel activity during spring and
early summer. In contrast, the lowest booking volumes appear in July 2024, where activity declined, possibly explained by holidays or reduced commuting patterns. Towards
September and November 2024, booking levels stabilized but with moderate fluctuations, indicating a steady but balanced demand. These findings suggest strong seasonality in
customer behavior, which businesses can leverage for staffing, promotions, and resource allocation.

![Line Chart](/assets/4-ridesTrendOverTime.png)

*This line chart represents the trend of ride bookings over time, highlighting periods of peak demand and seasonal declines.*
## 5. How does driver arrival time compare with trip duration across different hours of the day?
In order to assess how driver arrival time (VTAT) compares with trip duration (CTAT) across hours of the day, I created a smoothed line chart using a calculated 
`Hour = HOUR('ncr_ride_bookings'[Time])` on the X-axis and the DAX measure `Diff_CTAT_VTAT = AVERAGE(ncr_ride_bookings[Avg CTAT]) - AVERAGE(ncr_ride_bookings[Avg VTAT])`
on the Y-axis, with smoothing applied to reveal hourly patterns clearly.
### Insights
The chart shows the gap fluctuates roughly between ~19.5 and ~21.5 minutes, with a pronounced peak in the early morning (around hours 2–3) reaching ≈21.5 minutes, a dip near
hour 4 to ≈19.5 minutes, and secondary peaks in the late afternoon/evening (~21.0–21.1); this suggests that during early-morning and evening peak windows trips tend to be
longer relative to wait time (possible longer routes, traffic or supply constraints), while mid-period dips imply shorter trips or faster pickups — indicating opportunity to
reallocate drivers toward hours with higher gap to improve service.

![secondLineChart](/assets/5-tripVSWait.png)

*This line chart represents the hourly gap between average trip duration (CTAT) and average driver arrival time (VTAT), highlighting when trip time outstrips wait time and vice versa.*
## 6. Which vehicle types are most popular among riders?
In order to determine which vehicle types are most popular among riders, I created a grouped bar chart using the `Vehicle Type` field on the Y-axis and the
`Count of Booking ID` on the X-axis; I configured the visual to aggregate booking counts per category, sorted the bars in descending order for immediate readability, enabled data labels for exact counts.
### Insights
The results show a clear preference for compact, economical options: Auto leads with 4.1K bookings, followed by Go Mini (3.3K) and Go Sedan (3.0K), while Uber XL registers
the lowest demand (0.5K). This pattern likely reflects rider priorities in the dataset’s market—cost sensitivity, short urban trips, and high availability of smaller
vehicles—whereas larger or premium options (XL, Premier) see lower utilization due to higher fares and narrower use cases. Operationally, this suggests prioritizing fleet
allocation and driver incentives toward high-demand classes (Auto, Go Mini, Go Sedan), while considering targeted promotions or price adjustments to grow under-utilized
segments (e.g., Uber XL, eBike) and monitoring supply constraints that could cause lost bookings.

![Grouped Bar Chart](/assets/6-ridesByVehicleType.png)

*This grouped bar chart represents the total number of bookings per vehicle type, comparing popularity across all available vehicle categories.*
## 7. How much distance is traveled by each vehicle category?
In order to analyze the total distance traveled by each vehicle category, I created a grouped bar chart with `Vehicle Type` placed on the X-axis and `Ride Distance`
on the Y-axis, where the ride distance values were aggregated using the SUM function. This setup allowed me to compare the cumulative travel distances across different
vehicle categories and clearly highlight which types of vehicles account for the highest or lowest overall mileage.
### Insights
The analysis reveals that Autos lead with the highest total ride distance (70K), followed by Go Mini (56K) and Go Sedan (50K), showing their dominant role in covering urban
travel demand. Bikes (39K) and Premier Sedans (34K) cover a moderate share, likely used for shorter urban commutes and mid-range trips, respectively. On the other hand,
eBikes (20K) and Uber XL (8K) account for the lowest distances, which may be explained by their niche use: eBikes being limited to very short trips and XL vehicles being
used rarely, mostly for group rides or special occasions. Overall, the demand distribution highlights how compact and cost-effective vehicles handle most of the urban
travel load, while premium and specialty vehicles remain less utilized.

![Ride Distance](/assets/7-rideDistanceByVehicleType.png)

*This bar chart represents the total ride distance traveled across different vehicle categories.*
## 8. Which vehicle types generate the highest revenue?
In order to determine which vehicle categories contribute the most to platform revenue, I created this treemap by placing `Vehicle Type` as the category and using
the sum of `Booking Value` as the measure; the treemap visual was chosen for its ability to convey proportional contributions at a glance, so I configured the visual
to display both absolute values and relative area.
### Insights
The treemap shows that compact vehicle classes drive the bulk of revenue: Auto leads with approximately 1.40M in booking value, followed by Go Mini (~1.17M) and Go Sedan
(~1.05M), while Bike (~0.83M) and Premier Sedan (~0.70M) contribute moderate shares and eBike (~0.40M) and Uber XL (~0.16M) are the smallest contributors; this pattern
indicates that high-frequency, short-to-mid distance services generate the largest aggregate revenue (volume × fare), whereas premium or niche categories (XL, eBike)
produce less total revenue due to lower utilization despite potentially higher per-ride fares—insight that suggests prioritizing fleet allocation, driver incentives
and promotional spend toward high-performing vehicle classes while exploring targeted strategies (pricing, bundles, marketing) to grow underutilized segments.

![Treemap](/assets/8-bookingValueContributionByVehicleType.png)

*This treemap represents the booking value contribution by vehicle type across the platform, illustrating which vehicle categories generate the highest share of total revenue.*
## 9. Why do customers most frequently cancel rides?
In order to determine why customers most frequently cancel rides, I created a bar chart that displays the number of cancellations across different reasons provided
by customers. The data was grouped by cancellation reason, with each reason aggregated based on its total count of cancellations, and then plotted along the x-axis
while the frequency was shown on the y-axis. This visualization clearly highlights the leading factors driving cancellations, making it easier to identify
both customer-driven and driver-driven issues.
### Insights
The analysis reveals that the most common reason for cancellations is “Wrong Address” with 274 cases, indicating possible issues with inaccurate customer inputs or GPS
mapping errors. “Change of plans” and “Driver not moving towards pickup location” both follow closely with 252 cancellations each, reflecting the unpredictability
of customer behavior as well as operational inefficiencies on the driver’s side. Additionally, “Driver asked to cancel” (240) shows that some drivers themselves contribute
to cancellations, potentially due to scheduling conflicts or mismatched ride preferences. Finally, “AC is not working” is significantly lower at 121 cancellations,
suggesting that service quality issues are less frequent but still noteworthy. Overall, cancellations stem from both system inefficiencies and human factors,
highlighting areas where customer experience can be improved.

![Customer Reasons](/assets/9-topCustomerCancellationReasons.png)

*This bar chart represents the distribution of top customer cancellation reasons across total ride bookings.*
## 10. Why do drivers most frequently cancel rides?
To identify the primary causes of driver cancellations and address operational inefficiencies, I created this clustered bar chart. The visualization was built by first
aggregating the booking data based on the documented cancellation reason provided by the driver through the app. The `Driver Cancellation Reason` field was placed
on the categorical axis (x-axis), while the quantitative measure 'Number of Cancellations', represented by a distinct count of `Booking ID`, was plotted on the value axis
(y-axis). This approach provides a clear, ranked comparison of the volume of cancellations attributable to each specific cause, allowing for immediate prioritization
of issues.
### Insights
The data reveals that cancellations are nearly evenly distributed among the top four reasons, indicating no single overwhelming cause but a set of significant, parallel
challenges. "Personal & Car related issues" is the leading cause (761 cancellations), suggesting a need for better vehicle maintenance support or more flexible policies
for drivers facing unforeseen personal circumstances. The high rate of cancellations due to "The customer was coughing/sick" (736) and "More than permitted people in there"
(725) are both customer-related safety and policy violations. This points to a potential gap in the pre-ride process; solutions could include implementing a more prominent
passenger policy agreement pre-booking and a streamlined, in-app reporting system for drivers to flag these issues without canceling, allowing for faster rider re-matching.

![Driver Reasons](/assets/10-topDriverCancellationReasons.png)

*This bar chart represents the frequency of driver cancellations segmented by the primary reasons provided across all completed trips.*
## 11. Which payment methods are most preferred by customers?
In order to determine customer preference for transaction methods and guide strategic partnerships and platform development, I created this pie chart. The visualization
was built by categorizing the complete booking history dataset based on the `Payment Method` field selected at the time of trip completion. The values were calculated
as a percentage of total bookings, with each segment sized proportionally to represent its share of the total transaction volume. A distinct count of `Booking ID`
was used as the metric to ensure each transaction was only counted once, providing a clear and immediate visual representation of payment method prevalence.
### Insights
The data reveals an overwhelming and decisive preference for digital wallets, with UPI accounting for 45.39% of all transactions, making it the dominant payment method
by a significant margin. This is followed by traditional Cash payments at 25.11%, indicating a substantial segment of the user base still relies on physical currency.
The Uber Wallet holds a strong third place at 11.88%, suggesting that loyalty programs and prepaid benefits are effective. Credit and Debit cards collectively represent
less than 18% of transactions. The key insight is the market's strong inclination towards fast, seamless digital payment systems like UPI. To further reduce cash handling
and improve driver satisfaction, strategic initiatives could include promoting UPI and Wallet usage through targeted discounts or cashback incentives.

![Payment Method](/assets/11-paymentMethodDistribution.png)

*This pie chart represents the percentage distribution of trip bookings segmented by the chosen payment method across the customer base.*
## 12. What are the busiest pickup areas for rides?
To identify high-demand zones and optimize driver allocation and surge pricing models, I created this horizontal bar chart. The visualization was built by aggregating
the complete trip dataset based on the `Pickup Location` field. The distinct count of `Booking ID` was plotted on the x-axis to quantify the total number of rides
originating from each area, while the corresponding location names were listed on the y-axis. This horizontal orientation was selected to improve the readability
of the longer location labels, allowing for a clear, ranked comparison of transaction volume across the top metropolitan hotspots.
### Insights 
The data reveals a highly competitive landscape of demand, with the top seven pickup locations all generating a very similar volume of rides, clustered between 109 and 117
trips. Subhash Chowk is the busiest area with 117 rides, but it is closely followed by Barakhamba Road (112) and Jahangirpuri Road (110). This indicates that demand
is not concentrated in a single central business district but is distributed across several commercial, market, and residential hubs like Khan Market, Punjabi Bagh,
and Shivaji Park. The presence of Panipat suggests significant demand from satellite cities. To capitalize on this, operations strategy should focus on dynamic driver
incentives to ensure adequate supply across this distributed network of hotspots, especially during peak hours, to minimize wait times and prevent lost demand
in these critical areas.

![Pickup Locations](/assets/12-topPickupLocations.png)

*This horizontal bar chart represents the total volume of rides originating from the most frequented pickup locations across the operational network.*

# What I Learned
- **Slicers for Interactive Filtering 📊:** I learned how to implement and customize slicers to allow users to dynamically filter data across all visualizations. This greatly enhanced the dashboard’s interactivity and user experience, making it easy to drill down into specific time frames, locations, or ride attributes.

- **Navigation Buttons for user Experience 🔄:** This was my first time using bookmarks and buttons to create a seamless navigation experience between different dashboard pages. I designed an intuitive menu that helps users smoothly transition from overviews to detailed reports without confusion.

# Conclusions
1. **🛠️ Implement a Driver Support Hub to Reduce Cancellations**
The analysis identifies driver-initiated cancellations as the most significant operational leak, primarily due to personal/vehicle issues and passenger policy violations.
To address this, we recommend deploying an integrated Driver Support Hub within the app, featuring one-tap access to roadside assistance and a non-penalty reporting tool
for policy breaches. This allows drivers to be reassigned while the system re-matches the rider, tackling the root causes by offering immediate support and preserving
the booking. This strategy directly converts lost rides into completed trips and improves driver retention.

2. **📍 Launch a Dynamic Incentive Program to Optimize Fleet Allocation**
Demand is distributed across a network of hotspots, with a clear rider preference for compact vehicle types. To align supply with this demand, we propose a Dynamic Driver
Incentive Program. This data-driven strategy leverages real-time heatmaps to push targeted alerts to drivers, guiding them to high-demand zones, and offers bonus incentives
for drivers of high-utilization categories during predicted peak hours. This ensures optimal fleet allocation, minimizes "no driver found" incidents, reduces wait times,
and maximizes revenue from the most popular service tiers.

3. **💳 Accelerate the Shift to Digital Payments with Targeted Incentives**
While UPI is the dominant payment method, a substantial portion of transactions still relies on cash, which is less efficient and secure. To accelerate the transition
to higher-margin digital methods, we advise executing targeted UPI/Cashless Campaigns. These initiatives would offer discounts or cashback rewards for digital payments
and could introduce a small convenience fee for cash transactions. This approach improves operational efficiency, speeds up the payment process for drivers, enhances
security, and grows the adoption of the Uber Wallet.

4. **📱 Enhance Pre-Booking UX to Minimize Customer Cancellations**
The leading causes of customer cancellations are address errors and changes of plans. To mitigate these, we suggest introducing two key app features: an Address
Confirmation Prompt before booking finalization and a 5-Minute Grace Period for free cancellations. By improving booking clarity and offering a small amount
of flexibility, we can significantly reduce preventable cancellations, decrease rider frustration, and improve overall customer satisfaction.
