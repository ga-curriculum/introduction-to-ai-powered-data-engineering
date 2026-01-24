# Data Dictionary: RetailPulse Customer Dataset

**Dataset:** `customers.csv`  
**Source:** RetailPulse CRM System (simulated)  
**Records:** 50 customers  
**Last Updated:** 2025-01-23

---

## Overview

This dataset contains customer information from RetailPulse, an e-commerce company. It includes demographic, transactional, and behavioral data used for customer churn prediction.

---

## Schema

| Column Name | Data Type | Description | Example Values |
|-------------|-----------|-------------|----------------|
| `customer_id` | String | Unique identifier for each customer | C001, C002, C050 |
| `email` | String | Customer's email address (PII) | alice.johnson@email.com |
| `signup_date` | Date (YYYY-MM-DD) | Date the customer created their account | 2023-01-15 |
| `last_purchase_date` | Date (YYYY-MM-DD) | Date of the customer's most recent purchase | 2024-11-20 |
| `total_orders` | Integer | Cumulative number of orders placed | 1 - 28 |
| `total_spent` | Float | Cumulative amount spent in USD | 45.00 - 3420.75 |
| `loyalty_tier` | String (Categorical) | Customer loyalty program tier | Bronze, Silver, Gold, Platinum |
| `preferred_category` | String (Categorical) | Most frequently purchased product category | Electronics, Clothing, Home & Garden, Books, Sports, Beauty |
| `days_since_last_purchase` | Integer | Days between last_purchase_date and dataset refresh date (2025-01-23) | 3 - 330 |
| `is_churned` | Integer (Binary) | Churn label: 1 = churned, 0 = active | 0, 1 |

---

## Categorical Value Definitions

### loyalty_tier
| Value | Criteria |
|-------|----------|
| Bronze | 0-5 lifetime orders OR < $200 total spent |
| Silver | 6-12 lifetime orders OR $200-$800 total spent |
| Gold | 13-20 lifetime orders OR $800-$2000 total spent |
| Platinum | 21+ lifetime orders OR > $2000 total spent |

### preferred_category
| Value | Description |
|-------|-------------|
| Electronics | Phones, computers, accessories, gadgets |
| Clothing | Apparel, shoes, fashion accessories |
| Home & Garden | Furniture, décor, outdoor, kitchen |
| Books | Physical and digital books, audiobooks |
| Sports | Athletic equipment, fitness gear, outdoor recreation |
| Beauty | Skincare, makeup, personal care |

### is_churned
| Value | Definition |
|-------|------------|
| 0 | Active customer (purchased within last 120 days) |
| 1 | Churned customer (no purchase in 120+ days) |

---

## Data Quality Notes

1. **No missing values** - All fields are populated
2. **Email addresses are synthetic** - Not real PII
3. **Dates are consistent** - `signup_date` always precedes `last_purchase_date`
4. **Derived field** - `days_since_last_purchase` is calculated from `last_purchase_date` relative to 2025-01-23

---

## Statistical Summary

| Metric | Value |
|--------|-------|
| Total customers | 50 |
| Churned customers | 18 (36%) |
| Active customers | 32 (64%) |
| Avg. total orders | 10.7 |
| Avg. total spent | $953.42 |
| Date range (signup) | 2021-04-18 to 2023-12-01 |
| Date range (last purchase) | 2024-02-28 to 2025-01-20 |

---

## Usage Guidelines

This dataset is intended for educational purposes in the Data Engineering & Automation with AI course. It can be used for:

- Data ingestion and pipeline exercises
- Transformation and feature engineering practice
- ML model training demonstrations
- Data quality validation exercises

---

## Related Datasets

As the course progresses, additional datasets will be introduced:
- `orders.csv` - Transaction-level order data
- `products.csv` - Product catalog
- `clickstream.json` - Real-time user behavior events
