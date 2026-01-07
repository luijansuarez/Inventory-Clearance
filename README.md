# Inventory-Clearance
## Excutive Summary
Day-to-day operational decisions have a direct and often underestimated impact on bottom-line performance, particularly in environments with large and diverse inventories. When managing hundreds or thousands of SKUs, intuition alone is insufficient; decision-makers require structured models that can evaluate trade-offs quickly and consistently.

This case study presents a decision framework designed to determine the optimal pricing strategy for slow-moving inventory. The model evaluates multiple strategic options at the SKU level—including maintaining full price, applying targeted discounts, or executing immediate clearance—while explicitly accounting for holding costs, the time value of money, expected demand uplift from discounts, and clearance pricing. Rather than assuming every SKU can be made profitable, the framework focuses on maximizing economic value and minimizing further losses where necessary.

The solution integrates operational data (inventory levels, sales velocity, holding costs, and pricing) with market research inputs (product categories and demand elasticity) to automate strategy selection across the entire inventory portfolio. The output consists of a structured Excel report that assigns a recommended pricing decision to each SKU, as well as a Word executive summary that aggregates results and highlights key insights for management review.

Together, these outputs provide a scalable, transparent, and economically grounded approach to inventory clearance decisions—bridging analytical rigor with practical supply-chain execution.

## Business Context

In supply chain and operations, inventory decisions sit at the intersection of finance, logistics, and pricing strategy. While inventory is often treated as a purely operational concern, it is fundamentally a financial asset: it ties up working capital, incurs ongoing holding costs, and depreciates in value over time as demand shifts and products age.

Slow-moving inventory amplifies these challenges. As inventory remains unsold, organizations continue to incur storage and handling costs while capital remains locked in assets that cannot be redeployed elsewhere. In many real-world settings, these holding costs are not perfectly variable—warehouse leases, labor, and capacity constraints introduce fixed or stepwise costs that persist even when inventory is reduced. As a result, delaying action can be more expensive than it appears on the surface.

Pricing decisions further complicate the problem. Maintaining full price preserves unit margins but often extends sell-through timelines. Discounting can accelerate demand but requires sacrificing price to unlock volume. Clearance or liquidation removes inventory risk immediately, but frequently at the cost of realizing explicit losses. Each of these options represents a trade-off across time, margin, and operational flexibility rather than a clear-cut “right” or “wrong” choice.

At scale, these trade-offs become difficult to manage through intuition alone. Organizations managing hundreds or thousands of SKUs cannot reliably apply consistent pricing logic manually, leading to delayed decisions, inconsistent outcomes, and avoidable value erosion. Moreover, not all inventory can be made profitable—some SKUs are already economically impaired, and the optimal decision is simply the one that minimizes further losses.

This case study addresses these challenges by framing inventory clearance as a structured economic decision problem. By combining operational data with market-driven demand elasticity and applying a time-value-of-money perspective, the model enables consistent, transparent pricing decisions across an entire inventory portfolio.

## Modeling Assumptions

To ensure consistency and scalability across a large SKU portfolio, the model operates under a set of explicit simplifying assumptions.

Demand is treated as deterministic within each pricing scenario. Monthly sales volumes are assumed to remain constant over time, with demand uplift from discounting derived from external market research inputs. No cross-SKU demand interactions or substitution effects are modeled.

Pricing strategies are evaluated independently and remain fixed throughout the sell-through horizon. The “status quo” option maintains the current price and demand level, discount strategies apply a fixed price reduction and corresponding demand uplift, and clearance is modeled as an immediate liquidation event with no future holding or discounting effects.

Inventory sell-through is modeled on a monthly basis. Sales in any given month are capped by remaining inventory to prevent overselling, and inventory is assumed to sell down deterministically until depletion. Partial-month dynamics and intra-month timing effects are not explicitly modeled.

Holding costs are applied at the beginning of each month based on the inventory on hand. This assumption reflects capacity-based or contracted storage costs, such as warehouse leases or baseline labor requirements, which do not immediately scale down when inventory is reduced mid-month.

Future cash flows are discounted using a constant discount rate to reflect the time value of money, opportunity cost of capital, and risk. Discounting is applied symmetrically to both revenues and holding costs to enable consistent economic comparison across strategies.

The objective of the model is to maximize discounted economic value at the SKU level. The framework does not assume that all inventory can be made profitable; instead, it identifies the strategy that minimizes further value erosion when losses are unavoidable.

### Analytical Approach

The model evaluates inventory decisions by comparing the economic value of three mutually exclusive strategies at the SKU level: maintaining the current pricing strategy, applying a price discount to accelerate sell-through, or immediately clearing inventory at a clearance price. Each strategy is assessed using a discounted cash flow framework to ensure consistent comparison across time.

Status Quo (Full-Price Strategy).
Under the status quo option, each SKU is assumed to continue selling at its current price and observed monthly sales rate until inventory is depleted. Monthly revenues are generated based on sales volume, while holding costs are incurred on inventory carried into each period. Both revenues and costs are discounted to present value using a constant discount rate, reflecting the time value of money. The cumulative discounted profit from this sell-through represents the economic value of maintaining the current pricing strategy.

Clearance Strategy.
The clearance option is modeled as an immediate liquidation of remaining inventory at the specified clearance price. In some cases, this price may be negative, reflecting disposal or exit costs required to eliminate inventory exposure. Because this strategy eliminates future holding costs and uncertainty, it is treated as a single-period event with no discounting applied. The resulting value represents the fastest possible exit from inventory exposure and serves as a benchmark against longer-duration strategies.

Discount Strategies.
To evaluate discounting, the model incorporates market research data that estimates demand uplift associated with specific discount levels. For each discount scenario, the product price is reduced accordingly, and the monthly sales rate is increased based on the expected uplift. Using these adjusted parameters, the model simulates inventory sell-through over time and computes the discounted profit in the same manner as the status quo strategy. This process is repeated across all available discount levels, allowing the model to identify the most economically favorable discount option for each SKU.

Strategy Selection.
For each SKU, the model compares the discounted profit generated by the status quo strategy, the clearance strategy, and the best-performing discount scenario. The recommended pricing decision is the strategy that maximizes discounted economic value. Importantly, the framework does not assume that all strategies yield positive profits; when losses are unavoidable, the model selects the option that minimizes further value erosion.

## Implementation Highlights

The solution was implemented with an emphasis on robustness, transparency, and scalability in a notebook-based analytical environment.

Core economic logic, including inventory sell-through and discounted cash flow calculations, was encapsulated in reusable functions. This modular design ensured consistent application of assumptions across all pricing scenarios and reduced the risk of logic drift as the model evolved.

Physical and operational constraints were enforced explicitly in the implementation. Monthly sales were capped by remaining inventory to prevent overselling, and inventory was reduced deterministically over time until depletion. These safeguards ensured that simulated revenues remained economically feasible.

Time was modeled explicitly through month-by-month iteration, with both revenues and holding costs discounted consistently to reflect the time value of money. Clear control over timing assumptions—such as the application of holding costs at the beginning of each month—made the model’s behavior interpretable and auditable.

To improve reliability in a stateful notebook environment, the implementation followed defensive programming practices, including explicit DataFrame copying and avoidance of chained assignment. This reduced the likelihood of silent errors when rerunning or modifying cells.

SKU-level decisions and associated economic outcomes were stored using dictionary-based mappings and efficiently merged back into tabular outputs. This approach allowed rapid enrichment of results without complex joins, improving both performance and code clarity.

Finally, the model automated the generation of management-ready deliverables. An Excel workbook was produced with SKU-level decisions organized by product category and highlighted through conditional formatting, alongside a Word executive summary aggregating results for leadership review. Together, these outputs translated analytical results directly into operationally actionable artifacts.

## Results & Deliverables

The model produces two complementary, management-ready outputs designed to support both operational execution and strategic oversight.

SKU-Level Pricing Decision Report (Excel).
The primary operational output is an Excel workbook containing SKU-level pricing recommendations across the full inventory portfolio. Products are organized into separate worksheets by product category, enabling category managers and planners to focus on relevant subsets of the inventory. For each SKU, the report displays the recommended pricing strategy—maintain current price, apply a specific discount, or execute clearance—alongside key supporting metrics.

Conditional formatting is used to visually distinguish decisions, allowing users to quickly identify SKUs requiring immediate action, such as clearance or aggressive discounting. This structure supports rapid prioritization and facilitates direct integration into day-to-day inventory and pricing workflows.

Executive Summary Report (Word).
To support higher-level decision-making, the model also generates a Word document summarizing results at an aggregated level. This executive summary consolidates SKU-level outcomes into counts by product category and recommended strategy, providing leadership with a clear overview of the scale and distribution of pricing actions across the portfolio.

By separating operational detail from strategic summary, these outputs ensure that each stakeholder group receives information at the appropriate level of granularity. Together, the reports translate analytical results into concrete pricing recommendations that can be reviewed, approved, and executed within existing supply chain and pricing processes.

## Key Insights

Time can be more expensive than price.
For slow-moving inventory, the economic cost of holding inventory over time can outweigh the benefit of maintaining higher nominal prices, particularly when capital costs and storage constraints are considered.

Discounting is not inherently value-destructive.
When discounts meaningfully accelerate sell-through, the resulting reduction in holding costs and faster recovery of cash can increase overall economic value despite lower unit margins.

Clearance can be the rational choice even at a loss.
Some SKUs are economically impaired, and immediate liquidation—even at a negative value—can minimize further losses and remove ongoing operational risk.

Optimization does not guarantee profitability.
The objective of the model is to maximize economic value from the current point forward, not to retroactively recover sunk costs or force positive outcomes where they are not feasible.

Scale demands consistency, not intuition.
In large SKU portfolios, applying structured, repeatable decision logic produces more reliable outcomes than manual or intuition-based approaches.

Visibility into losses is strategically valuable.
Explicitly identifying loss-making inventory enables organizations to move beyond pricing actions toward root-cause analysis and process improvements upstream in forecasting, sourcing, and inventory planning.

## Limitations & Future Work
As with any decision framework designed for scalability and interpretability, the model relies on a set of simplifying assumptions that define its scope. 

First, pricing strategies are evaluated as fixed policies over time. In practice, pricing decisions are often staged, with deeper discounts applied as inventory ages. Extending the framework to evaluate predefined multi-period pricing paths—such as maintaining full price initially before applying successive markdowns—would allow more granular SKU-level decisions while preserving transparency and computational simplicity. 
Second, demand is treated as deterministic within each scenario. Monthly sales rates are assumed constant, adjusted only through discount-driven uplift factors. Incorporating stochastic demand or probabilistic sell-through would enable explicit risk analysis but would materially increase model complexity and data requirements. 
Third, the model evaluates SKUs independently and does not account for cross-product interactions such as substitution effects, cannibalization, or shared capacity constraints. While this independence assumption supports scalability across large portfolios, future extensions could incorporate category-level or capacity-based constraints to better reflect operational realities. 
Holding costs are modeled as a simplified per-SKU approximation applied at the beginning of each period. This approach captures the economic pressure of carrying inventory but does not explicitly optimize warehouse-level capacity, stepwise cost structures, or consolidation decisions. A more detailed capacity model could further refine clearance timing and prioritization. 
Finally, while intuitive revenue-based guardrails—such as bounding outcomes between immediate clearance value and full-price sell-through—can be useful as high-level diagnostics, they were not enforced as strict constraints in this framework. Such bounds can oversimplify the economics by mixing discounted and undiscounted quantities and by ignoring the impact of holding costs and time-to-sell. Instead, the model prioritizes internal consistency, physical feasibility (e.g., no overselling of inventory), and decision consistency across strategies. Future extensions could formalize diagnostic checks that respect the timing and discounting structure of the model without imposing misleading economic bounds. 
These limitations reflect deliberate trade-offs between realism, interpretability, and scalability. Future enhancements should be guided by the specific decision context and the marginal value of added complexity relative to operational usability.
