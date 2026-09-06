# Book Market Analysis and Rating Prediction Using Web Scraping and Machine Learning

## Project Overview

This project presents an end-to-end data science workflow for analysing book catalogue data collected through web scraping and applying machine learning to predict book ratings.

The project uses the **Books to Scrape** website as the data source. A total of **1,000 book records** were collected, cleaned, analysed, modelled, and presented through an interactive Power BI dashboard. :contentReference[oaicite:0]{index=0}

## Project Objectives

- Collect book information from multiple web pages using Python web scraping.
- Build a structured dataset containing 1,000 book records.
- Clean and preprocess the scraped data.
- Perform exploratory data analysis.
- Investigate relationships between price, rating, stock, categories, and descriptions.
- Build regression models to predict book ratings.
- Compare model performance using RMSE and R².
- Select and save the better-performing model.
- Develop an interactive Power BI dashboard.
- Generate business and analytical recommendations. :contentReference[oaicite:1]{index=1}

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- Requests
- BeautifulSoup
- Matplotlib
- Seaborn
- Scikit-learn
- Joblib
- Microsoft Power BI

## Project Workflow

### Phase 1 – Web Scraping

Book data was collected from the **Books to Scrape** website using `Requests` and `BeautifulSoup`.

The scraper collected information from catalogue pages and individual book detail pages, including:

- Title
- Price
- Rating
- Availability
- Product URL
- Category
- UPC
- Stock count
- Tax
- Description

The final raw dataset contained **1,000 records and 10 columns**. :contentReference[oaicite:3]{index=3}

### Phase 2 – Data Cleaning and Feature Engineering

The raw data was cleaned and transformed using Pandas.

Key steps included:

- Handling missing descriptions
- Checking duplicate records
- Cleaning currency values
- Converting ratings from words to numerical values
- Cleaning tax values
- Standardizing availability
- Validating numerical fields
- Creating derived features

Three additional features were created:

- **Price Category**
  - Budget: < £20
  - Mid-Range: £20–£39.99
  - Premium: ≥ £40
- **Rating Category**
  - Low Rated: ≤ 2
  - Average Rated: 3
  - Highly Rated: > 3
- **Description Length**

The final dataset contained **1,000 rows and 13 columns**, with **0 missing values and 0 duplicate records**. :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5}

### Phase 3 – Exploratory Data Analysis

EDA was performed using summary statistics, histograms, bar charts, scatter plots, correlation analysis, heatmaps, boxplots, and category analysis.

Key findings:

| Metric | Result |
|---|---:|
| Total Books | 1,000 |
| Categories | 50 |
| Average Price | £35.07 |
| Average Rating | 2.92 / 5 |
| Average Stock | 8.59 |
| Average Description Length | 1,441.50 characters |

The correlation between **price and rating was approximately 0.028**, indicating a very weak relationship. :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

### Phase 4 – Machine Learning

The machine learning problem was defined as:

**Regression – Predict Book Rating**

Features:

- Price
- Stock Count
- Description Length
- Category

Target:

- Rating

An 80/20 train-test split was used with `random_state = 42`, and the categorical category variable was encoded using One-Hot Encoding within a Scikit-learn pipeline. :contentReference[oaicite:8]{index=8}

#### Model Comparison

| Model | RMSE | R² |
|---|---:|---:|
| Random Forest Regression | 1.5236 | -0.1328 |
| Linear Regression | 1.5244 | -0.1341 |

Random Forest performed slightly better and was therefore selected as the final model. :contentReference[oaicite:9]{index=9}

The trained model was saved as:

```text
final_book_rating_regression_model.joblib
```
The model comparison results were saved as:

regression_model_comparison.csv
Although Random Forest performed slightly better, its negative R² shows that the selected features have limited ability to predict book ratings.

### Phase 5 – Power BI Dashboard

The cleaned dataset was imported into Microsoft Power BI to create an interactive Book Market Analysis & Rating Dashboard.

#### The dashboard contains two pages:

Dashboard Overview
Book Details

#### Key dashboard features include:

KPI cards
Price analysis
Rating analysis
Category analysis
Stock analysis
Key Influencers
Decomposition Tree
Interactive slicers
Bookmarks
Drill-through
Synchronized slicers
Row-Level Security (RLS)

#### The Premium Books RLS role filters the dataset to Premium books and produced:

Total Books: 403
Average Price: £49.91
Price Range: £40.11–£59.99
Key Insights
The catalogue contains 1,000 books across 50 categories.
Average book price is £35.07.
Premium books have a substantially higher average price than Budget and Mid-Range books.
Average rating is 2.92 out of 5.
Price and rating have an extremely weak correlation of approximately 0.028.
The selected machine-learning features have limited predictive power.
Random Forest slightly outperformed Linear Regression, but both models produced negative R² values.
The Power BI dashboard provides interactive exploration from high-level KPIs to individual book details.
### Recommendations
Continue using Budget, Mid-Range, and Premium price segmentation.
Do not use price alone as an indicator of book quality or rating.
Introduce richer features such as textual, author, publication, and review-related information for future rating prediction.
Monitor category-level performance carefully, especially for categories with small sample sizes.
Use the Power BI dashboard for interactive catalogue analysis.
Extend Row-Level Security to additional business roles in a larger real-world implementation.
### Limitations
Books to Scrape is a practice/sandbox website, so the data does not represent the entire real-world book market.
The dataset has no date or time field, so time-series analysis was not possible.
The selected predictive features have weak relationships with rating.
Both regression models produced negative R² values.
Category sizes vary substantially, so some category-level averages should be interpreted carefully.
Tax is constant at zero and availability is standardized to a single value, limiting their analytical usefulness.

### Repository Structure
```
book-market-analysis-rating-prediction/
├── 01_Web_Scraping.ipynb
├── 02_Data_Cleaning.ipynb
├── 03_EDA.ipynb
├── 04_Machine_Learning.ipynb
├── BOOK MARKET ANALYSIS AND RATING PREDICTION.pdf
├── Book_Market_Analysis_Dashboard.pbix
└── README.md
```
### Conclusion

This project demonstrates a complete end-to-end data science pipeline, beginning with web data acquisition and continuing through data cleaning, exploratory analysis, machine learning, and interactive dashboard development.

The project successfully collected and processed 1,000 book records, evaluated two regression models, selected Random Forest as the better-performing model, and developed an interactive Power BI dashboard. The limited predictive performance itself is an important finding, demonstrating that model quality depends heavily on the informativeness of the available features.
