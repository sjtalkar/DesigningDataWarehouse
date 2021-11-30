# DesigningDataWarehouse

Kimball Dimensional Modeling Techniques

The idea that a measurement event in the physical world has a one-to-one relationship to a **single row** in the corresponding fact table is a bedrock principle for dimensional modeling. Everything else builds from this foundation.

You will see that facts are sometimes semi-additive or even non-additive.
- Semi-additive facts, such as account balances, cannot be summed across the time dimension.
- Non-additive facts, such as unit prices, can never be added.
