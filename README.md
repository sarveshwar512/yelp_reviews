# Yelp Reviews Analysis Platform

## Project Overview
An end-to-end data analytics pipeline processing 7 million Yelp reviews (5GB) and business data (100MB) to derive actionable business insights through data engineering, warehousing, and analytical techniques.

## Architecture
[yelp_review_project.png](https://github.com/sarveshwar512/yelp_reviews/blob/680390df4651f3e4ecc380435eae3670afbad6b0/yelp_review_project.png)

The pipeline follows this workflow:
1. **Data Ingestion**: JSON files from Yelp dataset (reviews and business data)
2. **Data Processing**: Python scripts to transform and preprocess data
3. **Cloud Storage**: Amazon S3 for staging the processed data
4. **Data Warehousing**: Snowflake for storing and analyzing the data
5. **Analysis**: SQL queries and sentimental analysis with UDFs
6. **Visualization**: (Optional section about visualization tools if used)

## Technical Implementation

### Data Pipeline
- Designed and implemented ETL processes to handle 5GB of Yelp review data (7 million records)
- Built robust data processing scripts in Python to handle JSON parsing and transformation
- Implemented efficient data loading strategies to transfer data from S3 to Snowflake
- Created Snowflake tables and optimized schema design for analytics performance

### Analysis Capabilities
The data model enables various business insights including:

1. **Business Category Analysis**
   - Distribution of businesses across categories
   - Most popular business categories based on review volume

2. **User Behavior Analysis**
   - Identification of power users and their reviewing patterns
   - Analysis of user engagement with different business types

3. **Review Pattern Analysis**
   - Temporal patterns in review submissions
   - Correlation between ratings and business attributes

4. **Sentiment Analysis**
   - Implementation of User-Defined Functions (UDFs) for sentiment scoring
   - Identification of positive/negative review patterns

## Key Business Queries
The platform supports complex analytical queries including:

```sql
-- Sample queries (simplified versions)

-- Distribution of businesses across categories
SELECT category, COUNT(*) as business_count 
FROM business_categories 
GROUP BY category 
ORDER BY business_count DESC;

-- Finding top reviewers for restaurants
SELECT u.user_id, u.name, COUNT(*) as review_count
FROM reviews r
JOIN users u ON r.user_id = u.user_id
JOIN businesses b ON r.business_id = b.business_id
WHERE b.categories LIKE '%Restaurant%'
GROUP BY u.user_id, u.name
ORDER BY review_count DESC
LIMIT 10;

-- Finding businesses with highest percentage of 5-star reviews
SELECT b.name, b.city,
       COUNT(CASE WHEN r.stars = 5 THEN 1 END) * 100.0 / COUNT(*) as percentage_5_star
FROM reviews r
JOIN businesses b ON r.business_id = b.business_id
GROUP BY b.name, b.city
HAVING COUNT(*) > 20
ORDER BY percentage_5_star DESC;
```

## Performance Considerations
- Implemented appropriate indexing strategies in Snowflake
- Optimized query performance for large dataset handling
- Utilized Snowflake's columnar storage for efficient analytical queries

## Skills Demonstrated
- Data Modeling & Schema Design
- ETL Pipeline Development
- Cloud Data Warehousing (Snowflake)
- SQL Analytics & Optimization
- Python for Data Processing
- AWS S3 for Cloud Storage
- Large Dataset Handling
- Business Intelligence & Analytics

## Future Enhancements
- Implementation of real-time data streaming
- Integration with BI tools for dashboard creation
- Addition of machine learning models for predictive analytics
- Geographic analysis and visualization

## Setup Instructions
(Include instructions for running the code locally)

## Dataset
This project uses the public Yelp dataset available at [Yelp Dataset](https://www.yelp.com/dataset).
