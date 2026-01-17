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
Visual 1: Market Size by Engagement Behavior
* The question I am answering here is "Do simulation and sandbox games represent a meaningful portion of the market?"

INSERT IMAGE HERE 

* **What the graph shows**
    * The x-axis showcases the two main groups of genres, Competitive and Simulation/Sandbox genres. 
    * The y-axis measures the number of games that go into either of these genres. 
* **Insight**
    * The graph aims to showcase based on their genre, how many games are present in competitive vs simulation/sandbox categories.
    * Around 55,000 competitive games and around 51,000 simulation and sandbox games. 
* **Interpretation**
    * Yes, simulation and sandbox games do show meaningful engagement. There is a nearly evenly split close group of users who play simulation/sandbox games just as competitive games.
    * Analytics platforms are disproportionately focused on competitive games, indicating a substantial underserved segment.
 
