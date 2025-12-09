# NOVAMART PROJECT
A data-driven analysis project using PostgreSQL to guide product development, customer retention, and operational efficiency for a Nigerian subscription-based company that struggles to turn its data into business value.
# 🏪 NovaMart: Customer and Product Insight Optimisation  
### *Exploratory Data Analysis using PostgreSQL*

---

## 🧭 Executive Summary  
NovaMart is a **digital-first Nigerian subscription company** offering curated lifestyle bundles - wellness kits, tech accessories, snacks, and home essentials, through a monthly subscription model.  
Despite tracking thousands of transactions and customer interactions, NovaMart struggled to turn its data into actionable business insights.  
This project applies **PostgreSQL-based data exploration** to reveal:  
- Which bundles are most profitable 💰  
- How discounts impact total revenue 💸  
- Which loyalty tiers drive long-term value 👑  
- What customer issues affect satisfaction 📉
   
By merging data cleaning and PostgreSQL analysis, this project transforms raw data into a roadmap for smarter growth and retention.  

---

## 🎯 Objectives to be uncovered
1. Identify top-performing and underperforming bundles  
2. Analyse customer spending by loyalty tier  
3. Assess payment success and failure trends  
4. Determine total revenue by product category  
5. Explore issue types with the lowest customer ratings  

---

## 🗂️ Data Description  

| Table | Description |
|--------|--------------|
| `customers` | Customer demographics and loyalty details |
| `subscriptions` | Order history: quantity, discount, total value |
| `bundles` | Bundle category, size, and active status |
| `payments` | Payment method, outcome, and status |
| `support_tickets` | Customer complaints, issue types, and ratings |

📄 *Raw data sourced from CSV files was well formatted/normalised and loaded into PostgreSQL for analysis.*

---

## ⚙️ Project Workflow  

1. **Database Restoration** – Imported and normalised CSV data into PostgreSQL  
2. **PostgreSQL Exploration** – Wrote analytical queries to extract business KPIs    
3. **Insights & Recommendations** – Summarized findings for decision-making  

---

## 🧩 PostgreSQL Analysis  

### 1️⃣ Top 3 Bundles by Subscription Count  
**PostgreSQL Query**  
SELECT b.bundle_name, b.category, COUNT(s.subscriptionid) AS subscription_count  
FROM subscriptions s  
JOIN bundles b ON s.bundle_id = b.bundleid  
GROUP BY b.bundle_name, b.category  
ORDER BY subscription_count DESC  
LIMIT 3;  
 
<img width="647" height="262" alt="image" src="https://github.com/user-attachments/assets/aeeba877-4090-400d-b37a-28c41391e20f" />  

💡 Insight: Wellness and Essential bundle-categories are dominating the lists of bundle categories, while wellness comes first and second with 2,232 and 2,141 subscription   counts, respectively - this shows huge demand in health and lifestyle.  

 
### 2️⃣ Average Spend by Loyalty Tier (Successful Payments Only)  
**PostgreSQL Query**    
SELECT c.loyalty_tier, ROUND(AVG(s.total_value), 2) AS avg_spend  
FROM payments p  
JOIN subscriptions s ON p.subscription_id = s.subscriptionid  
JOIN customers c ON s.customer_id = c.customerid  
WHERE p.is_successful = 'TRUE'  
GROUP BY c.loyalty_tier  
ORDER BY avg_spend DESC;  

<img width="665" height="268" alt="image" src="https://github.com/user-attachments/assets/216e6467-d057-4fff-a94a-0c27215b525b" />  

💡 Insight: Gold-tier customers have the highest spend per order, with an average spend of 15,288.55, suggesting strong engagement and loyalty potential. Others, such as Platinum and Silver, are coming close.


### 3️⃣ Failed Payments by Method  
**PostgreSQL Query**  
SELECT payment_method, COUNT(*) AS failed_count  
FROM payments  
WHERE LOWER(payment_status) = 'failed'  
GROUP BY payment_method  
ORDER BY failed_count DESC;  

<img width="648" height="266" alt="image" src="https://github.com/user-attachments/assets/4233d30f-bba6-42e7-ac6a-6cc18f295974" />  

💡 Insight: Card, bank transfer, and wallet are topping the list of payment methods with failed transaction counts of 345, 238 and 145, respectively. Identifying the payment methods with high failure rates helps reduce revenue leakage and improve checkout reliability.  


### 4️⃣ Total Revenue by Bundle Category  
**PostgreSQL Query**  
SELECT b.category, SUM(s.total_value) AS total_revenue  
FROM subscriptions s  
JOIN bundles b ON s.bundle_id = b.bundleid  
JOIN payments p ON p.subscription_id = s.subscriptionid
WHERE b.is_active = TRUE AND p.is_successful = TRUE
GROUP BY b.category
ORDER BY total_revenue DESC;  

<img width="638" height="298" alt="image" src="https://github.com/user-attachments/assets/e822c3e1-3426-43fc-a44c-346d84096aef" />  

💡 Insight: Wellness and Essentials drive ~80% of NovaMart’s total revenue — prime targets for bundle-categpro expansion and campaign investment.  


**PostgreSQL Query**  
### 5️⃣ Issue Types with Lowest Ratings  
SELECT issue_type, ROUND(AVG(rating), 2) AS avg_rating  
FROM support_tickets  
GROUP BY issue_type  
ORDER BY avg_rating ASC;  

<img width="642" height="300" alt="image" src="https://github.com/user-attachments/assets/f1385168-3494-4e8c-8ed4-1d8c15d4029f" />  

💡 Insight: Out of the four issue types with the lowest rating, product quality and billing issues have the lowest satisfaction ratings. These are direct opportunities to improve service experience.

---

### Focus Areas and Key Insights  
1️⃣ Revenue Drivers - 80% of revenue from Wellness & Essentials  
2️⃣ Customer Spend - Gold-tier customers lead average spend  
3️⃣ Payment Performance - 728 failed payments (payment system improvements needed)  
4️⃣ Discount Impact - 14% discount — requires optimisation for profitability  
5️⃣ Feedback Focus - Product quality and billing issues drive dissatisfaction  
6️⃣ Regional Growth - Port Harcourt & Enugu have the strongest engagement  


### 📈 Recommendations  
1️⃣ Double down with more commitment on Top Categories by investing in Wellness & Essentials product innovation.  
2️⃣ Optimise discount strategy by capping at ≤15% for sustainable margins.  
3️⃣ Reduce failed payments by auditing payment gateways and retry logic.  
4️⃣ Enhance product quality by strengthening supplier and quality control processes.  
5️⃣ Reward loyal customers through personalised offers for Gold and Platinum tiers.  
6️⃣ Scale regional campaigns by prioritising Port Harcourt & Enugu for local outreach.  


### 🧰 Tools & Technology    
Tools used and their purposes  
1️⃣ CSV Files - Raw data source  
2️⃣ Excel - To effectively format the dataset before converting to CSV and subsequently importing it into PostgreSQL for analysis  
3️⃣ PostgreSQL - Data exploration and querying  


⚠️ Disclaimer  
This project is for educational and portfolio demonstration only. Data is simulated and does not represent any real organisation.  

### 🔗 Connect With Me  
Ifunanya R. Uzokwe  
📧 Uzokweifunanya10@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/Ifunanya-uzokwe/)  
💻 [GitHub](https://github.com/fumnanyasecret)   



