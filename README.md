# Introduction
The growing demand for ride-hailing services like Uber 🚖 generates massive volumes of booking data 📊 that often remain underutilized. Companies face challenges
in understanding ride performance 🏎️, cancellation behavior ❌, customer trends 👥, and payment preferences 💳. This project was designed to address these challenges
by transforming raw ride-booking data 📂 into actionable insights 🔍 through an interactive Power BI dashboard 🖥️. By leveraging advanced visualizations such as KPIs 📌,
trend analyses 📈, cancellation breakdowns 🚫, and payment method distributions 💵, the dashboard enables stakeholders to monitor operations ⚙️, identify pain points 📉,
and improve decision-making 💡. With intuitive navigation 🔘 and slicers 🎛️ for filtering by date 📅 and vehicle type 🚙, the solution empowers managers to evaluate
key performance metrics 📏 and enhance overall operational efficiency 🚀.

🔗 Want to explore the project?
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
