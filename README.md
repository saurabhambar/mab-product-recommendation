# E-Commerce Product Recommendation using Multi-Armed Bandits

This project implements **Multi-Armed Bandit (MAB)** algorithms to optimize product recommendations in an e-commerce setting.

The goal is to maximize **net profit (Revenue - Cost)** by learning which product to recommend to each user instead of relying on a random strategy.

---

## Problem Overview

A large e-commerce platform displays **one product per user session**. The objective is to maximize long-term profit.

Each dataset row represents a user session:


- `ProductX`: Revenue generated if product X is shown
- `CostX`: Cost incurred to show product X
- **Reward = Revenue - Cost**

There are **6 products → 6 arms** in the bandit problem.

---

## Objective

- Learn which product maximizes profit
- Compare different bandit strategies
- Replace inefficient random recommendation system

---

## Dataset Insights

From analysis:

- **Product 2 → Most profitable**
- **Product 5 → Consistently loss-making**

Example:

| Product | Mean Profit | Positive Profit % |
|--------|------------|------------------|
| 1 | 7.06 | 100% |
| 2 | 66.99 | 100% |
| 3 | 31.42 | 100% |
| 4 | 9.60 | 100% |
| 5 | -17.06 | 0% |
| 6 | 36.99 | 100% |

Product 2 clearly dominates in profit. :contentReference[oaicite:0]{index=0}

---

## Implemented Strategies

---

## 1. Random Strategy

### Description
- Selects a product randomly for each user
- No learning involved

### Result

- Average profit per round ≈ **21.58**
- Picks best product only occasionally

### Problem

- Wastes impressions on bad products
- Highly inefficient

---

## 2. Explore-Then-Commit Strategy

### Description

- Explore each product fixed number of times
- Then always choose best-performing product

### Result

- Correctly identifies Product 2
- **Cumulative Profit ≈ 30,681**

### Insight

- Works well but:
  - Exploration is blind
  - May commit too early

---

## 3. Epsilon-Greedy Strategy

### Description

- With probability ε → explore
- Otherwise → exploit best-known product

### Tested Values

| Exploration Level | ε | Total Profit |
|------------------|--|-------------|
| Low | 2% | 14,246 |
| Moderate | 10% | 28,586 |
| High | 25% | 26,372 |

### Insights

- **Low (2%)**
  - Gets stuck early
- **High (25%)**
  - Over-explores → lower profit
- **Moderate (10%)**
  - Best balance → near-optimal performance

---

## 4. UCB (Upper Confidence Bound)

### Description

- Selects actions based on:


- Automatically balances exploration & exploitation

### Result

- **Cumulative Profit ≈ 33,099 (Highest)**
- Quickly focuses on Product 2
- Other products tried only once

### Key Insight

- Smart exploration → eliminates bad products early

---

## Final Comparison

| Strategy | Total Profit |
|---------|-------------|
| Random | 10,747 |
| Explore-Then-Commit | 30,681 |
| Epsilon-Greedy (2%) | 14,246 |
| Epsilon-Greedy (10%) | 28,586 |
| Epsilon-Greedy (25%) | 26,372 |
| **UCB** | **33,099** |

👉 **Best Strategy: UCB**

👉 **Best Product: Product 2** :contentReference[oaicite:1]{index=1}

---

## Key Learnings

### Random Strategy
- No learning
- Highly inefficient

### Explore-Then-Commit
- Fast convergence
- Risk of early wrong decision

### Epsilon-Greedy
- Needs tuning
- Best at moderate exploration

### UCB
- Best overall
- Smart exploration
- Highest profit

---

### Estimated Reward + Exploration Bonus

## Visualization

The project includes:

- Cumulative profit curves
- Strategy comparison plots
- Exploration vs exploitation analysis

---

## Tech Stack

- Python
- NumPy
- Pandas
- Matplotlib

---

## Project Structure

```
├── MAB_Assignment.ipynb
├── Dataset_Product_Recommendation.csv
├── README.md
```

---

## How to Run

```bash
git clone https://github.com/<your-username>/mab-product-recommendation
cd mab-product-recommendation
pip install -r requirements.txt
jupyter notebook

## Business Impact

This project demonstrates:

- How learning algorithms outperform static rules
- How profit optimization can be automated
- Real-world application of bandit algorithms in:
  - Recommendation systems
  - Ads optimization
  - Pricing strategies

## Future Improvements
- Thompson Sampling
- Contextual Bandits
- Deep RL approaches
- Real-time deployment simulation
