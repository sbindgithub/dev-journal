# Day 4 – Inventory Management and Planning

## 1. What is Inventory?
Inventory refers to goods and materials held by a company for:
- Production
- Sale
- Supporting operations

Inventory exists to **balance demand and supply**, but it also ties up money.

---

## 2. Warehouse and Inventory Flow
A warehouse has three core activities:
- Inbound (receiving goods)
- Storage (holding inventory)
- Outbound (dispatching goods)

Inventory primarily resides in the **storage stage**.

---

## 3. Types of Inventory

### Raw Material
Basic materials used in manufacturing.

### Work In Progress (WIP)
Goods that are partially processed but not yet finished.

### Finished Goods
Completed products ready for sale.

### MRO Inventory
Maintenance, Repair, and Operations items that support production but are not sold.

### Merchandise Inventory
Goods purchased and sold without any transformation.

### Transit Inventory
Inventory that is moving between locations.

### Anticipatory Inventory
Inventory built in advance for known future demand (seasonal or promotional).

### Buffer Inventory
Extra inventory held to protect against uncertainty.

### Safety Stock
A **calculated portion of buffer inventory** used to protect against demand and lead-time variability.

---

## 4. Why Inventory Management is Important
Poor inventory management leads to:
- Stock-outs (lost sales)
- Dead stock
- Expiry and obsolescence
- Poor cash flow
- Low customer satisfaction (CSAT)

Good inventory management balances **availability and cost**.

---

## 5. Inventory Management Techniques

### Just In Time (JIT)
Inventory arrives only when needed, reducing holding cost.

### Just In Case (JIC)
Extra inventory is kept to manage uncertainty.

### ABC Analysis
Inventory is classified based on value:
- A: High value, tight control
- B: Moderate value
- C: Low value, simple control

### FIFO / LIFO
Methods to decide which stock is issued first.

### Dropshipping
Seller does not hold inventory; supplier ships directly.

### Vendor Managed Inventory (VMI)
Supplier manages inventory levels for the buyer.

### Cross Docking
Goods move directly from inbound to outbound with minimal storage.

### Cycle Counting
Continuous verification of inventory accuracy.

---

## 6. Inventory-Related Costs

### Holding (Carrying) Cost
- Storage
- Insurance
- Damage
- Obsolescence

### Ordering (Setup) Cost
- Purchase processing
- Transportation
- Administration

### Opportunity (Stock-out) Cost
- Lost sales
- Customer dissatisfaction

---

## 7. Economic Order Quantity (EOQ)

### Purpose
EOQ determines **how much to order** to minimize total inventory cost.

### Formula
EOQ = √(2DS / H)

Where:
- D = Annual demand
- S = Ordering cost per order / Setup cost
- H = Holding cost per unit per year

# What is EOQ (Economic Order Quantity)?

## Definition
**EOQ (Economic Order Quantity)** is the order quantity that **minimizes the total inventory cost**.

It does **not** mean:
- Minimum stock
- Minimum number of orders

It means:
- **Minimum total cost**

---

## Understanding Total Inventory Cost

Total inventory cost has **two opposing components**:

### 1. Ordering Cost
- Cost incurred every time an order is placed
- Includes paperwork, processing, transport, setup, etc.
- **Decreases** when you order **larger quantities less frequently**

### 2. Holding (Carrying) Cost
- Cost of storing inventory
- Includes storage, insurance, damage, obsolescence, capital cost
- **Increases** when you order **larger quantities**

---

## Why EOQ Exists (Intuition First)

### If you order **small quantities frequently**
- Many orders
- High ordering cost
- Low holding cost

### If you order **large quantities infrequently**
- Few orders
- Low ordering cost
- High holding cost

EOQ identifies the **sweet spot** where the **sum of ordering cost and holding cost is the lowest**.

At EOQ:
> **Ordering cost ≈ Holding cost**

---

## EOQ Formula

\[
\text{EOQ} = \sqrt{\frac{2DS}{H}}
\]

Where:
- **D** = Annual demand (units/year)
- **S** = Ordering cost per order
- **H** = Holding cost per unit per year

---

## EOQ – Step-by-Step Example

### Given:
- Annual demand (**D**) = 12,000 units  
- Ordering cost (**S**) = ₹80 per order  
- Holding cost (**H**) = ₹25 per unit per year  

---

### Step 1: Apply the formula

\[
\text{EOQ} = \sqrt{\frac{2 \times 12{,}000 \times 80}{25}}
\]

\[
= \sqrt{\frac{1{,}920{,}000}{25}}
\]

\[
= \sqrt{76{,}800}
\]

\[
\approx 277 \text{ units}
\]

---

## Interpretation (Critical Concept)

**EOQ = 277 units does NOT mean you keep 277 units in stock forever.**

It means:
- Every time you place an order, you should order **277 units**
- This order size minimizes the **total inventory cost**

---

## Supporting Calculations (Proof of EOQ Logic)

### Number of orders per year
\[
\frac{12{,}000}{277} \approx 43 \text{ orders/year}
\]

### Annual ordering cost
\[
43 \times 80 = ₹3{,}440
\]

### Average inventory held
\[
\frac{277}{2} = 138.5 \text{ units}
\]

### Annual holding cost
\[
138.5 \times 25 = ₹3{,}462.5
\]

### Key Observation
➡ **Ordering cost ≈ Holding cost**

This balance confirms that EOQ is correctly calculated.

---

## What EOQ Does NOT Consider

EOQ assumes:
- Constant demand
- Fixed lead time
- No stock-outs
- No quantity discounts

If these assumptions do not hold, **EOQ must be modified or replaced** with advanced models.

---

## EOQ vs ROP (Common Confusion)

- **EOQ** → How much to order  
- **ROP (Reorder Point)** → When to order  

They solve **different inventory problems**.

---

## One-Line Interview-Ready Definition

**EOQ is the optimal order quantity that minimizes the combined ordering and holding costs under stable demand conditions.**

---

## 8. Reorder Point (ROP)

ROP determines **when to place an order**.

### Formula
ROP = (Average Daily Demand × Lead Time) + Safety Stock

---

## 9. Safety Stock Concept
Safety stock protects against:
- Demand variability during lead time
- Lead time uncertainty

Safety stock is consumed **only when actual demand exceeds expected demand**.

---

## 10. Concept Summary (Memory Aid)
- EOQ → Right quantity
- ROP → Right time
- Safety stock → Protection during lead time
- Buffer stock → General protection
- Anticipatory stock → Known future demand
