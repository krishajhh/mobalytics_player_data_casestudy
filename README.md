<img width="900" height="480" alt="image" src="https://github.com/user-attachments/assets/2a6bc490-9469-4f07-a4c9-6c0e488189ad" />



## Identifying Untapped Engagement Behaviors for Mobalytics
Market Research & Data Analytics Case Study

### 📌 Summary  
This case study analyzes player engagement patterns across 23,000+ Steam games (2020–2024) to identify high-engagement behaviors not captured by traditional performance analytics platforms. Using normalized, review-based engagement metrics and behavior-first segmentation, the analysis finds that simulation and sandbox games exhibit sustained, non-competitive engagement patterns comparable in scale but different in nature to competitive games. 

These findings indicate a significant underserved market opportunity and support a data-backed **product expansion strategy** for Mobalytics into **non-competitive performance analytics** focused on creativity, exploration, and long-term consistency.

### 🎯 Context & Problem
Mobalytics is a gaming performance analytics platform designed to help players improve their gameplay through data-driven feedback. The platform has successfully established itself within competitive, skill-based games such as Valorant and Call of Duty, where performance is defined by rankings, mechanical execution, and win-loss outcomes.

During my Market Research and Data Analytics Externship, I noticed a large portion of the gaming market engages deeply with non-competitive genres, including simulation, sandbox, and casual games. These players demonstrate strong engagement but lack access to meaningful performance feedback, as traditional analytics tools are optimized for competitive metrics.

The core problem I want to address in this study is whether high-engagement player behaviors exist outside competitive contexts, and whether these behaviors justify expanding Mobalytics’ analytics framework beyond competitive play. 

### 📊 Data Source 
Check out the dataset -> [Steam Games Metadata and Player Reviews (2020–2024)](https://data.mendeley.com/datasets/jxy85cr3th/2)
* 23,107 games, 31+ million user reviews, game level metadata, engagement proxies (negative/positive reviews). 
* Steam review data is used as a behavioral proxy for engagement because direct telemetry or demographic data is unavailable. 
* The dataset reflects PC gaming behavior and captures engagement during a pivotal period of digital gaming growth.

### 🔣 My Methodology 
**Excel**

I used excel as a initial data preparation layer to validate data quality, build my derived engagement metrics, and perform sanity checks before large scale aggregation.

1. Data Validation
* I identified and cleaned missing or null values, games with 0 total reviews, and inconsistent release dates that could affect my data analysis. 

2. Engagement Normalization & Adjusted Metric 
* To account for differences in game age, I decided to create a normalized metric for engagement. I called this reviews_per_year. In this metric, I set reviews_per_year = total_reviews / (current_year - release_year)
* This metric allows newer and older games to be compared on equal footing by measuring engagement rate over time rather than cumulative popularity.
* Although, when I created this I noticed games with zeros or very recent release dates produced infinite or undefined values. To resolve this, I created an adjusted metric called reviews_per_year_adj. 
* This adjusted metric became the primary engagement signal that I used later in SQL and Tableau for my analysis and visualization. 

3. Sanity Checks
* I created a pivot table to validate my average engagement by genre, confirm the expected distribution patterns and also identify any null or malformed genre entries so I can exclude them. 

**SQL**

I used SQLite to scale analysis, define behavioral classifications, and also use for my visualizations in Tableau. 

1. Data Model
* I structured each row representative of one game and one genre combination. Some games with multiple genres would appear in multiple rows. This structure allowed me to enable genre level behavioral analysis without having to collapse multi-genre games in a single category. 

2. Behavioral Classification
* To move beyond surface level genre analysis, I chose to introduce two behavioral flags, is_competitive and is_simulation. Is_competitive includes genres from action, shooter, sports, fighting, racing, etc. Is_simulation includes genres from simulation, sandbox, casual, management, indie, etc. 
* These 2 flags or categories allowed me to aggregate by player behavior type, rather than relying solely on genre labels.  

3. Engagement Comparison Queries 
* Using the reviews_per_year_adj, I compared engagement across behavioral categories to answer my key questions.
      * Do simulation and sandbox games show sustained engagement?
      * How does engagement differ between competitive and non-competitive games?
      * What proportion of the market falls into each behavioral segment?
* All aggregation queries used normalized engagement metrics to ensure fair comparison across release years. 

4. Market Sizing & View Creation
* SQL views were created to estimate market size by behavioral category, aggregate engagement metrics at the segment level, provide a stable interface for Tableau visualizations

### 📈 Data Visualization

I used tableau to translate my SQL-derived engagement metrics into interpretable visuals that support behavioral analysis and strategic decision-making. 

🔗 Tableau Dashboard: [Link](https://public.tableau.com/views/MobalyticsUntappedEngagementBehaviors2020-2024/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

**Visualization 1: Market Size by Engagement Behavior*** 
* **Purpose:** "Do simulation and sandbox games represent a meaningful portion of the market?" In other words, determining whether simulation and sandbox games represent a meaningful and scalable segement of the market. 
* **Data Source:** SQL view aggregating game counts by behavioral category (is_competitive, is_simulation)
* **Key insight:** Simulation and Sandbox games account for nearly half of the addressable market, indiciating a large and underserved audience not currently prioritizied by analytics platforms. 

**Visualization 2: Engagement Intensity by Behavior Type**
* **Purpose:** Which genres combine high engagement with non-competitive behavior? In other words, comparing normalized engagement rates between competitive and non-competitive games. 
* **Metric Used:** reviews_per_year_adj
* **Key Insight:** Competitive games show a higher engagement intensity, while simulation game demostrate consistent, sustained engagement over time - highlighting different engagement dynamics rather than weaker engagement. 

**Visualization 3: Engagement Patterns by Genre**
* **Purpose:** How large is the untapped audience? In other words, I am identifying game-level engagement behaviors and uncover non-competitive genres with strong engagement signals. 
* **Key Insight:** Simulation, indie and casual games show meaningful engagement despite lacking performance-based mechanics, suggesting that there are opportuntoes for alternative analytics frameworks and expansion to simulation. 

**Strategic Implications for Mobalytics**
* What the Data Implies: Through these graphs, it shows that high engagement does not require competition games only. There are large, stable audiences that exist outside competitive games or ecosystems that lack meaningful performance feedback. 

* Product Expansion Opportunities: Based on my analysis, I believe Mobalytics should introduce non-competitive games on their platform. 

**Features to add**
* Non-competitive performance metrics (e.g., creative diversity, exploration rate, consistency over time). 
* AI chatbox that goal sets for sandbox and simulation players
* Community challenges focused on creation and progression rather than ranking
