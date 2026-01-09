# Inventory Clearance as an Economic Decision

## SKU-level pricing framework using discounted cash flows

## 1. Problem Statement

Slow-moving inventory is often treated as a logistical issue, but it is fundamentally a financial decision expressed through operations. Inventory ties up working capital, incurs holding costs over time, and depreciates in value as demand shifts.

When organizations manage hundreds or thousands of SKUs, clearance decisions—maintaining price, discounting, or liquidating—are frequently made using heuristics or fixed rules, without explicitly modeling time, capital costs, or demand elasticity. This leads to delayed actions, inconsistent outcomes, and avoidable value erosion.

## 2. Objective

This case study presents a decision framework to determine the economically optimal pricing strategy for slow-moving inventory at the SKU level.

Rather than forcing profitability, the model’s objective is to maximize discounted economic value from today forward, even when the best outcome is to minimize further losses.

## 3. Approach

Each SKU is evaluated across three mutually exclusive strategies:

Maintain price: preserves unit margin but extends sell-through time.

Discount: lowers price to accelerate demand, incorporating expected demand uplift.

Immediate clearance: liquidates inventory instantly, eliminating future holding costs and risk.

All strategies are evaluated using a discounted cash flow (DCF) framework, explicitly accounting for:

Inventory levels and sales velocity

Holding costs

Pricing and discount levels

Demand uplift from discounts (market research inputs)

Time value of money

The recommended decision is the strategy that maximizes discounted economic value, not the one that “recovers sunk costs.”

## 4. Outputs

The model generates two management-ready deliverables:

SKU-level Excel report

Recommended pricing action per SKU

Organized by product category

Visual cues to highlight clearance and discount decisions

Executive summary (Word)

Aggregated view of decisions by category

Clear visibility into value-preserving vs. loss-minimizing actions

These outputs are designed for direct integration into pricing and inventory workflows.

## 5. Key Insights

Time can be more expensive than price for slow-moving inventory.

Discounting is not inherently value-destructive when it accelerates sell-through and releases capital.

Clearance can be economically rational, even at a loss, when future holding costs dominate.

Optimization does not guarantee profitability—it guarantees better decisions.

Consistency at scale beats intuition in large SKU portfolios.

## 6. Scope & Limitations

The model uses deterministic demand within each pricing scenario and evaluates strategies independently at the SKU level. Cross-SKU interactions, stochastic demand, and staged markdown paths are intentionally excluded to preserve interpretability and scalability. These extensions represent natural areas for future work.

## 7. How to Explore Further

Full Python notebook with detailed implementation and assumptions
