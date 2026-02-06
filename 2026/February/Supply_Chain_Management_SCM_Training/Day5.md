# Day 5 – Inventory Management Fundamentals

This document covers the core inventory management concepts used in operations, supply chain, and production planning. It includes definitions, formulas, worked examples, and practical interpretations.

---

## 1. Inventory Control – Why It Matters

Inventory exists to:
- Meet customer demand
- Buffer against uncertainty
- Enable smooth production and distribution

Poor inventory control leads to:
- Stock-outs (lost sales, production stoppage)
- Excess holding cost
- Obsolete and non-moving stock

Inventory management is about **balancing availability and cost**.

---

## 2. Economic Order Quantity (EOQ)

### Definition
EOQ is the optimal order quantity that minimizes the **total inventory cost**, which is the sum of:
- Ordering cost
- Holding (carrying) cost

EOQ assumes:
- Constant demand
- Constant lead time
- No stock-outs
- Instant replenishment

---

### EOQ Formula

\[
EOQ = \sqrt{\frac{2DS}{H}}
\]

Where:
- **D** = Annual demand (units/year)
- **S** = Ordering cost per order
- **H** = Holding cost per unit per year

---

### Example: EOQ Calculation

Given:
- Annual demand (D) = 16,000 units
- Ordering cost (S) = ₹55 per order
- Holding cost (H) = ₹15 per unit/year

\[
EOQ = \sqrt{\frac{2 \times 16000 \times 55}{15}}
\]

\[
EOQ = \sqrt{117,333.33}
\]

\[
EOQ \approx 342.5 \text{ units}
\]

**Interpretation:**  
The company should place orders of approximately **343 units per order**.

---

## 3. Order Frequency and Order Cycle Time

### Number of Orders per Year

\[
\text{Orders per year} = \frac{D}{EOQ}
\]

\[
= \frac{16000}{342.5} \approx 47 \text{ orders/year}
\]

---

### Time Between Orders (Order Cycle)

If the company operates **300 days per year**:

\[
\text{Order cycle time} = \frac{300}{47} \approx 6.4 \text{ days}
\]

**Meaning:**  
A new order is placed roughly every **6–7 days**.

---

## 4. Holding Cost (Annual)

Average inventory under EOQ:

\[
\text{Average inventory} = \frac{EOQ}{2}
\]

\[
= \frac{342.5}{2} = 171.25 \text{ units}
\]

Annual holding cost:

\[
= 171.25 \times 15 = ₹2568.75
\]

---

## 5. Lead Time Demand (LTD)

### Definition
Lead Time Demand is the quantity required **during the supplier lead time**.

### Formula

\[
\text{Lead Time Demand} = \text{Average Daily Demand} \times \text{Lead Time}
\]

---

### Example

If:
- Annual demand = 16,000 units
- Operating days = 300 days/year
- Lead time = 10 days

Average daily demand:

\[
= \frac{16000}{300} \approx 53.33 \text{ units/day}
\]

Lead time demand:

\[
= 53.33 \times 10 = 533 \text{ units}
\]

---

## 6. Safety Stock

### Purpose
Safety stock protects against:
- Demand variability
- Lead time variability

It is **not the same as lead time demand**.

---

### Basic Safety Stock Formula (Deterministic)

\[
\text{Safety Stock} =
(\text{Max Daily Demand} \times \text{Max Lead Time})
-
(\text{Avg Daily Demand} \times \text{Avg Lead Time})
\]

If variability is not provided, safety stock is either:
- Given directly, or
- Assumed to be zero

---

## 7. Reorder Point (ROP)

### Definition
Reorder Point is the inventory level at which a **new order must be placed**.

### Formula

\[
ROP = \text{Lead Time Demand} + \text{Safety Stock}
\]

---

### Example

If:
- Lead time demand = 533 units
- Safety stock = 100 units

\[
ROP = 533 + 100 = 633 \text{ units}
\]

**Meaning:**  
When inventory falls to **633 units**, place a new order.

---

## 8. Inventory Control Methods

### 1. Just-In-Time (JIT)
- Inventory ordered only when needed
- Very low buffer stock
- High dependency on supplier reliability
- Reactive system

---

### 2. Economic Order Quantity (EOQ)
- Cost-optimization model
- Suitable for stable demand
- Assumes predictable environment

---

### 3. ABC Analysis (Value-Based)

Based on Pareto Principle (80/20 rule):

| Class | Description | Control Level |
|-----|-------------|---------------|
| A | High-value items | Very tight |
| B | Medium-value items | Moderate |
| C | Low-value items | Simple |

---

### 4. FSN Analysis (Movement-Based)

| Category | Meaning |
|--------|--------|
| F | Fast-moving items |
| S | Slow-moving items |
| N | Non-moving items |

Used for:
- Disposal decisions
- Warehouse space optimization

---

### 5. VED Analysis (Criticality-Based)

Used mainly for **spares and healthcare inventory**.

| Category | Meaning |
|--------|--------|
| V | Vital |
| E | Essential |
| D | Desirable |

Often combined with ABC (ABC–VED matrix).

---

## 9. FMCG vs Durable Goods (Inventory Perspective)

| Aspect | FMCG | Durables |
|-----|------|---------|
| Demand frequency | Very high | Low |
| Inventory turnover | High | Low |
| ROP sensitivity | Very high | Moderate |
| Stock-out impact | Immediate | Delayed |

---

## 10. Key Exam & Interview Warnings

- EOQ is a **quantity**, not a cost
- Safety stock ≠ lead time demand
- Operating days must match the question
- ROP always includes **demand**, not just time
- Wrong assumption = wrong answer

---

## Summary

Inventory management is a quantitative discipline.  
Precision in formulas, units, and assumptions is mandatory.

EOQ optimizes **how much to order**.  
ROP determines **when to order**.  
Classification techniques decide **how tightly to control**.

---
