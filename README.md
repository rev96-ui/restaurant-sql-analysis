# Restaurant Database SQL Analysis

## Project Overview

A SQL analysis of **real restaurant transaction data** from January-March 2023. I analyzed **5,370 orders** to understand what customers order, who spends the most money, and what patterns drive revenue.

**Dataset:** 5,370 orders | 12,234 line items | 32 menu items | 4 categories  
**Tools:** MySQL, SQL  
**Time Period:** January 1 - March 31, 2023

---

## SQL Queries Used

### Query 1: Combine Order & Menu Data
```sql
SELECT *
FROM order_details od
LEFT JOIN menu_items mi
ON od.item_id = mi.menu_item_id;
```
**Purpose:** Joins orders with menu details so I can see what was ordered and at what price.

### Query 2: Most & Least Ordered Items
```sql
SELECT item_name, category, COUNT(order_details_id) AS num_purchases
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY item_name, category
ORDER BY num_purchases DESC;
```
**Purpose:** Shows which items customers order most frequently.

### Query 3: Top 5 Spending Orders
```sql
SELECT order_id, SUM(price) AS total_spend
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spend DESC
LIMIT 5;
```
**Purpose:** Finds the orders that spent the most money.

### Query 4: Highest Order Analysis
```sql
SELECT category, COUNT(order_details_id) AS total_orders
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
WHERE order_id = 440
GROUP BY category;
```
**Purpose:** Shows what was in the highest-spending order.

### Query 5: Top 5 Orders Comparison
```sql
SELECT order_id, category, COUNT(order_details_id) AS total_orders
FROM order_details od
LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id
WHERE order_id IN (440, 2075, 1957, 330, 2675)
GROUP BY order_id, category;
```
**Purpose:** Compares items across all top 5 orders to find patterns.

---

## My Key Findings

### Finding 1: What Do Customers Actually Order?

**The Question:** Which items are most and least popular?

**The Data:**
- **Most ordered:** Hamburger (American) - **622 times**
- **Least ordered:** Chicken Tacos (Mexican) - **123 times**
- **Difference:** Hamburger ordered **5x more** than Chicken Tacos

**What This Means:**
Customers strongly prefer affordable, familiar comfort food over specialized cuisine. Hamburger appeals to everyone—it's classic, reliable, and probably the cheapest item on the menu. Chicken Tacos are more niche; not everyone wants Mexican food, but everyone likes hamburgers.

**For the business:** Feature hamburger in marketing. Comfort food drives volume.

---

### Finding 2: Who Spends the Most Money?

**The Question:** Do high spenders buy expensive items or just order more items?

**The Data:**
- **Top 5 orders spent:** $118.75 - $145.50 per order
- **Average order spent:** ~$50 (estimate)
- **Comparison:** Top 5 orders spend **2-3x MORE** than average
- **Order size:** Top 5 averaged **7-8 items each**

**What This Means:**
High spenders don't buy expensive items—they buy MORE items. This isn't a customer ordering one $50 steak. This is a group of people ordering 7-8 items total. These are families dining together, business dinners, or parties.

**For the business:** One group order generates the revenue of 2-3 individual orders. Groups are your best customers.

---

### Finding 3: What's in a High-Value Order?

**The Question:** What does a top-spending order actually look like?

**The Data:**
Order #440 ($145.50 total) contained:
- **3 American items** (Hamburgers, Mac & Cheese, etc.)
- **2 Asian items** (Pad Thai, etc.)
- **2 Italian items** (Pasta, etc.)
- **1 Mexican item** (Burrito, etc.)

**What This Means:**
The highest-spending order has items from ALL FOUR categories. This isn't one person ordering—it's a group of 3-4 people, each choosing from different cuisines. Everyone got something they wanted. This confirms the pattern: groups order variety.

**For the business:** Promote group dining. Create combo packages where people can mix cuisines. Let groups easily order for diverse tastes.

---

## Why This Matters

### Pattern Across All Top 5 Orders:
All top 5 high-spending orders include multiple categories and American items. Groups consistently order a variety of cuisines in large quantities.

### Business Opportunities:
1. **Target groups, not individuals** - Market to families, business teams, celebrations
2. **Promote combo/group packages** - Let people mix cuisines easily
3. **Feature comfort food** - Hamburger drives volume; use it to attract customers
4. **Upsell groups** - When you see large orders coming in, recognize them as premium customers

---

## SQL Skills Demonstrated

✅ **LEFT JOIN** - Combined order_details with menu_items  
✅ **GROUP BY** - Grouped items/orders together  
✅ **COUNT & SUM** - Counted purchases and calculated spending  
✅ **WHERE & ORDER BY** - Filtered and ranked data  
✅ **Data Quality** - Handled NULL values (found one in row 122)  
✅ **Business Analysis** - Interpreted data for actionable insights

---

## How This Project Helps Me

This was my first real SQL analysis with actual transaction data. It taught me:

- How to write queries that answer business questions
- That data tells a STORY—I'm not just counting numbers
- How to interpret findings and make recommendations
- That analyzing data is about understanding CUSTOMERS, not just data

---

## Next Steps

If I had more time, I would:
- Analyze how orders change by day/week (time trends)
- Look at repeat customers vs. one-time customers
- Find which items are ordered together (does burger + fries combo happen often?)
- Track average order value over time

---

## Files in This Project

```
restaurant-sql-analysis/
├── README.md                    ← You are here
├── queries/
│   ├── 01_join_data.sql
│   ├── 02_most_popular.sql
│   ├── 03_top_5_orders.sql
│   ├── 04_highest_order.sql
│   └── 05_top_5_comparison.sql
└── database/
    └── create_restaurant_db.sql
```

---

## Let's Connect

📧 **Email:** revreven96@gmail.com  
🔗 **LinkedIn:** https://www.linkedin.com/in/rev-reven/  
💻 **GitHub:** [Your GitHub repo URL - add this after you create it]

---

**Status:** ✅ Complete  
**Last Updated:** March 23, 2026
