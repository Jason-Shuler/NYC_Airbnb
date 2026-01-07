# NYC Airbnb Market Analysis: Pricing & Revenue Optimization
### Executive Summary
This project analyzes a dataset of 48,895 NYC Airbnb listings to identify key drivers of revenue and pricing efficiency. I engineered features in SQL to identify high-performing hosts, track seasonal trends, and calculate price volatility. The analysis identified corporate housing entities (e.g., Blueground) as the dominant revenue drivers and highlighted specific neighborhoods with high arbitrage potential.

### Key Findings and Insights
* **Revenue:** Utilized Window Functions to identify that the top host, Blueground, generated over $2.2M in revenue, significantly outperforming individual hosts.
* **Neighborhood Volatility:** Greenpoint and Upper West Side showed the highest price variability ($10,000 variance), indicating a mix of luxury and budget inventory that suggests high rental arbitrage opportunities.
* **Seasonal Trends:** Analysis of review frequency and pricing revealed that December is the peak pricing month ($160/night avg), while August surprisingly offered lower average rates ($132/night), suggesting potential for off-peak marketing strategies.
* **Host Performance:** "Row NYC" achieved the highest average review monthly activity (18.62).

### Technical Skills
* **Advanced Aggregations:** Used `GROUP BY` and `SUM` to calculate financial metrics at the host and neighborhood level.
* **Window Functions:** Implemented `RANK()` and `DENSE_RANK()` to leaderboard hosts by revenue without collapsing the dataset.
* **CTEs (Common Table Expressions):** specificially for the Price Variability analysis to create readable, modular SQL code.
* **Temporal Analysis:** Utilized `julianday()` and `strftime()` to manipulate datetime objects to track review recency and seasonality.

**Example: Ranking Hosts by Revenue (Window Function)**
SELECT 
    host_name, 
    SUM(price * minimum_nights) AS total_revenue,
    RANK() OVER (ORDER BY SUM(price * minimum_nights) DESC) AS revenue_rank
FROM listings
GROUP BY host_name
ORDER BY total_revenue DESC
LIMIT 10;

