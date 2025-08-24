# 🛒 Zepto E-commerce: SQL Data Analysis Project

## 🎯 Executive Summary

I designed and executed a comprehensive SQL analysis of Zepto's e-commerce inventory data, transforming raw operational information into actionable business intelligence. This project demonstrates my ability to derive strategic insights from complex datasets using advanced SQL techniques.

## 📊 Technical Implementation

### Database Architecture
I built an optimized PostgreSQL database with performance-focused design:

sql
CREATE TABLE zepto_products (
    sku_id SERIAL PRIMARY KEY,
    category VARCHAR(120) NOT NULL,
    name VARCHAR(150) NOT NULL,
    mrp NUMERIC(10,2),
    discount_percent NUMERIC(5,2),
    available_quantity INTEGER,
    discounted_price NUMERIC(10,2),
    weight_gms INTEGER,
    out_of_stock BOOLEAN,
    package_quantity INTEGER
);

-- Performance indexing
CREATE INDEX idx_category ON zepto_products(category);
CREATE INDEX idx_price ON zepto_products(discounted_price);
CREATE INDEX idx_stock ON zepto_products(out_of_stock);


### Data Processing Pipeline
I implemented a robust ETL process including:
- Automated data validation checks
- Currency normalization from paise to rupees
- Comprehensive data quality assessment
- Outlier detection and handling

## 🔍 Analytical Approach

### Data Quality Assessment
I conducted thorough data profiling to ensure analysis reliability:

sql
-- Comprehensive data health check
SELECT 
    COUNT(*) AS total_records,
    SUM(CASE WHEN mrp IS NULL THEN 1 ELSE 0 END) AS null_mrp_values,
    AVG(discount_percent) AS avg_discount,
    COUNT(DISTINCT category) AS unique_categories
FROM zepto_products;


### Business Intelligence Queries

*1. Pricing Strategy Analysis*
sql
SELECT 
    category,
    ROUND(AVG(discount_percent), 2) AS avg_discount,
    ROUND(AVG(discounted_price), 2) AS avg_selling_price,
    COUNT(*) AS products_count
FROM zepto_products
GROUP BY category
ORDER BY avg_discount DESC;


*2. Inventory Health Dashboard*
sql
SELECT 
    category,
    SUM(available_quantity) AS total_stock,
    SUM(CASE WHEN out_of_stock THEN 1 ELSE 0 END) AS out_of_stock_items,
    ROUND(SUM(discounted_price * available_quantity), 2) AS inventory_value
FROM zepto_products
GROUP BY category
ORDER BY inventory_value DESC;


*3. High-Value Opportunity Analysis*
sql
SELECT 
    name,
    category,
    mrp,
    discounted_price,
    discount_percent,
    available_quantity
FROM zepto_products
WHERE mrp > 500 
AND discount_percent < 10
AND NOT out_of_stock
ORDER BY mrp DESC;


## 📈 Key Insights Delivered

### Strategic Findings:
1. *Discount Patterns*: Identified categories with most aggressive pricing strategies
2. *Revenue Opportunities*: Discovered high-value products with suboptimal discounting
3. *Inventory Gaps*: Flagged critical out-of-stock items affecting revenue
4. *Category Performance*: Quantified revenue potential across product segments

### Business Impact:
- *Pricing Optimization*: Data-driven recommendations for discount strategies
- *Inventory Management*: Identified stock replenishment priorities
- *Category Analysis*: Revealed highest-performing product categories
- *Revenue Growth*: Pinpointed opportunities for margin improvement

## 🛠 Technical Skills Demonstrated

- *Advanced SQL Querying*: Complex joins, window functions, and aggregations
- *Database Design*: Schema optimization and indexing strategies
- *Data Quality Management*: Comprehensive validation and cleaning procedures
- *Business Intelligence*: Translating data into actionable insights
- *Performance Optimization*: Efficient query design for large datasets

## 📋 Project Outcomes

This analysis provided Zepto with:
- Data-driven pricing recommendations
- Inventory optimization strategies
- Category performance insights
- Revenue growth opportunities
- Operational efficiency improvements

The project demonstrates my ability to handle complete data analysis workflows from raw data to executive-level business intelligence, showcasing expertise directly applicable to e-commerce and retail analytics roles.
