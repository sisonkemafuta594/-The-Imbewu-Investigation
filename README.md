# 🛒 The Imbewu Investigation — Retail Revenue Analytics

> A structured, end-to-end data analytics capstone investigating a revenue decline across a national South African retail chain — from stakeholder brief to store-level recommendations.

---

## 📌 Project Overview

This project follows a real-world analytics investigation commissioned by the Head of Sales at **Imbewu Retail**, a fictional South African retailer operating 45 stores across four provinces. The brief was simple:

> *"Numbers are down in Western Cape, but foot traffic is roughly flat. I have an exec readout in three weeks — I need to know what's going on."*
> — Sizwe Khumalo, Head of Sales

The investigation spans **three structured weeks**, moving from initial data profiling and hypothesis formation, through causal analysis by format, category, and loyalty tier, down to individual store-level diagnostics and concrete recommendations.

---

## 📁 Repository Contents

| File | Description |
|---|---|
| [`Week1_Investigation_Plan.docx`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/Week1_Investigation_Plan.docx) | Stakeholder brief, data overview, quality audit, 4 testable hypotheses, and Week 2 investigation plan |
| [`Week3_StoreLevel_DeepDive.docx`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/Week3_StoreLevel_DeepDive.docx) | Individual store performance across all 12 WC stores; deep-dive into top declining stores with category and monthly breakdowns |
| [`SQL_queries.html`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/SQL_queries.html) | Full Databricks SQL notebook all queries used in the investigation with inline findings and commentary |
| [`imbewu_final_board_dashboard.html`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/imbewu_final_board_dashboard__2_.html) | Interactive executive dashboard summarising findings for the board readout |
| ! [`ERD_Diagram.png`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/ERD_Diagram.png) | Entity Relationship Diagram showing the full database schema | 
| [`data_dictionary.md`](https://github.com/sisonkemafuta594/imbewu-investigation/blob/main/data_dictionary.md) | Complete data dictionary — all 6 tables, column definitions, row counts, quality issues, and key analysis decisions |

---

![Imbewu Retail ERD](ERD_diagram.png)
- [Week 1 Investigation Plan](Week1_Investigation_Plan.pdf)
- [Data Dictionary](data_dictionary.md)
- [View SQL Queries](SQL_queries.html)
- [Week 3 Store Level Deep Dive](Week3_StoreLevel_DeepDive.pdf)
- [Investigation Notes](Investigation_Notes.pdf)
- [Interactive Dashboard](imbewu_board_dashboard.html)
  
---

## 🗄️ Dataset at a Glance

The dataset covers **January 2024 – June 2025** across 6 relational tables:

| Table | Rows | Description |
|---|---|---|
| `stores` | 45 | Store metadata — format, province, city |
| `products` | 48 | Product catalogue with cost and price |
| `customers` | 3,000 | Loyalty programme members (Bronze / Silver / Gold) |
| `transactions` | 9,164 | Till receipts, including ~43% anonymous (non-loyalty) shoppers |
| `transaction_items` | 48,641 | Line-item detail — quantity, price at sale, discount applied |
| `promotions` | 4 | Active promotions with dates, categories, and discount rates |

**Revenue is defined as:** `(quantity × unit_price_at_sale) − discount_applied`

**Key data quality decisions:**
- `stores.province` had inconsistent casing — standardised to Title Case for all analysis
- `transactions.customer_id` has 3,911 NULLs (anonymous shoppers) — included in all revenue totals, excluded from loyalty-tier analysis
- All year-over-year comparisons use **H1 only (Jan–Jun)** in both 2024 and 2025 for a like-for-like comparison

---

## 🔍 Investigation Structure

### Week 1 — Discovery & Hypothesis Building

Confirmed the problem is real and WC-specific through initial profiling:

| Province | H1 2024 Revenue | H1 2025 Revenue | Change |
|---|---|---|---|
| Western Cape | R388,788 | R365,245 | **−6.0%** |
| Gauteng | R251,827 | R274,484 | +9.0% |
| KwaZulu-Natal | R218,302 | R249,409 | +14.3% |
| Eastern Cape | R88,529 | R97,117 | +9.7% |

Western Cape is the **only declining province**. Transaction count dropped just 2.3% (confirming flat foot traffic), but average basket size fell from R387.62 to R372.70 a **−3.9% spend-per-visit decline** that no other province experienced.

**Four hypotheses were formed and prioritised:**

| # | Hypothesis | Status |
|---|---|---|
| A | Mega-format stores dragging WC average down | ✅ Confirmed — primary driver |
| B | Product mix shift toward lower-value categories | ✅ Confirmed — secondary driver |
| C | Silver-tier loyalty customers spending/visiting less | ✅ Confirmed — tertiary driver |
| D | Promotion coverage gap in WC | 🔵 Held in reserve — not required to explain the gap |

---

### Week 2 — Hypothesis Testing

**Hypothesis A- Mega Store Drag:**
WC Mega stores declined **−11.6%** in H1. Express stores in WC grew +14.7% and Market stores grew +2.8%. The entire WC net decline is driven by the Mega format. Nationally, Mega stores also declined −12.7%, but WC has 3 of the 6 national Mega stores making the impact disproportionate.

**Hypothesis B- Product Mix Shift:**
Groceries (−9.1%) and Household (−10.9%) declined across all WC formats. Nationally, these same categories grew +2.8% and +0.1% respectively. WC customers are spending less on high-volume staple categories consistent with a local competitive threat drawing grocery shoppers elsewhere.

**Hypothesis C- Silver-Tier Erosion:**
Silver-tier revenue in WC fell **−10.7%** (vs Gold at 0.0% and Bronze at −5.6%). Silver visits dropped −9.0% meaning customers are visiting less often, not just spending less per visit. Silver basket size dropped −1.9% while nationally Silver baskets grew +5.6%. This signals that mid-tier customers may be defecting to a competitor.

**Promotion Analysis (Pap Power Promo PR001):**
The Buy 2 Get 1 Free promotion on Maize Meal in April 2025 drove a **+50.5% volume uplift** but only a **+2.2% revenue gain** due to the deep 33.3% discount. A May 2025 demand dip suggests stockpiling occurred during the promo period. Recommendation: evaluate gross margin impact before repeating; consider a 20% discount to protect revenue while still driving volume.

---

### Week 3 Store-Level Deep Dive

Following a challenge from the Western Cape Regional Manager, all 12 WC stores were analysed individually:

| Store | Format | H1 2024 | H1 2025 | Revenue Δ |
|---|---|---|---|---|
| Imbewu Mega Bellville | Mega | R74,192 | R55,365 | **−25.4%** |
| Imbewu Market Claremont | Market | R23,327 | R20,090 | −13.9% |
| Imbewu Mega Paarl Central | Mega | R68,342 | R60,079 | −12.1% |
| Imbewu Market George Central | Market | R26,822 | R23,679 | −11.7% |
| Imbewu Mega Tygervalley | Mega | R60,329 | R56,211 | −6.8% |
| Imbewu Express Mitchell's Plain | Express | R5,778 | R8,186 | **+41.7%** |
| Imbewu Express Sea Point | Express | R6,848 | R9,020 | **+31.7%** |
| Imbewu Market Khayelitsha | Market | R22,903 | R29,682 | **+29.6%** |

**Key finding:** The WC decline is not province-wide. It is **concentrated in 3 Mega stores** (Bellville, Paarl Central, Tygervalley) which together account for R31,209 of gross revenue loss **132.6% of the total net WC gap**. Four stores are actively growing.

**Imbewu Mega Bellville** (worst performer, −25.4%):
- Groceries alone declined 31.6%, accounting for 65.8% of the store's total revenue loss
- Electronics declined −33.6% simultaneously
- February 2025 was the inflection point (basket size dropped 31.3% vs Feb 2024)
- Pattern strongly suggests a large-format competitor opened in the Bellville catchment area in late 2024 / early 2025
- June 2025 showed a small positive reversal early signal worth monitoring

---

## 🛠️ Tools & Technologies

- **SQL (Databricks)** all data profiling, hypothesis testing, and store-level analysis
- **Power BI** executive board dashboard
- **Microsoft Word** structured weekly investigation reports

---

## 📐 Schema

```
stores ──────────────────────── transactions
  (store_id)                      (store_id FK, customer_id FK)
                                        │
customers ──────────────────────────────┘
  (customer_id)                         │
                                  transaction_items
                                  (transaction_id FK, product_id FK)
                                        │
products ───────────────────────────────┘
  (product_id)

promotions — linked to transaction_items via category + date overlap
```

---

## 💡 Key Takeaways

1. **Aggregate metrics mask store-level truth.** "WC is down 6%" is a much weaker finding than "3 specific Mega stores are down 7–25%, while 4 stores are growing strongly."
2. **Foot traffic ≠ revenue.** A flat transaction count with a falling basket size points to competitive pressure on spend, not customer acquisition failure.
3. **Deep promotions can move volume without moving revenue.** The Pap Power Promo is a textbook example: +50% units, +2% revenue. Discount depth matters.
4. **Loyalty tiers behave differently under competitive pressure.** Gold customers remained loyal and growing. Silver customers showed clear visit-frequency decline a leading indicator of churn.

---

## 👤 Author

**Sisonke Mafuta**
GitHub: [@sisonkemafuta594](https://github.com/sisonkemafuta594)

---

*This project was completed as a data analytics capstone. All company names, store names, and individuals referenced are fictional.*
