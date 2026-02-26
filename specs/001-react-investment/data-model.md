# Data Model: AI Investment Portfolio Agent

## Core Entities

### 1. `InvestorProfile` (Input Model)
Represents the exact parameters collected from the user to determine their portfolio allocation.
- `age` (Integer): The age of the investor in years. Must be >= 18.
- `investment_term_years` (Integer): The time horizon for the investment. Must be > 0.
- `max_drawdown_percent` (Float): The maximum portfolio drop the investor can emotionally/financially tolerate. Must be between 0.0 and 100.0.
- `investment_goal` (String): The primary objective (e.g., "growth", "fixed income", "capital preservation").

### 2. `AssetAllocation` (Internal/Output Model)
The high-level split of asset classes based on the `InvestorProfile` constraints.
- `equity_percent` (Float): Percentage of the portfolio in stocks/equities.
- `fixed_income_percent` (Float): Percentage of the portfolio in bonds/treasuries.
- `cash_percent` (Float): Percentage of the portfolio in cash equivalents.
*Validation*: `equity_percent + fixed_income_percent + cash_percent` MUST exactly equal 100.0.

### 3. `InvestmentAsset` (Output Model)
An individual ETF or stock recommended within the `AssetAllocation`.
- `ticker` (String): The official market ticker (e.g., "VTI", "BND").
- `name` (String): The full name of the fund/stock.
- `allocation_percent` (Float): The specific percentage of the total portfolio assigned to this asset.
- `rationale` (String): The AI's 1-2 sentence justification for including this specific asset.

### 4. `PortfolioPlan` (Final Output Model)
The completed, structured recommendation returned to the user.
- `summary` (String): A high-level overview of the strategy.
- `assets` (List[`InvestmentAsset`]): The specific assets.
*Validation*: The sum of `allocation_percent` across all `assets` MUST exactly equal 100.0.
