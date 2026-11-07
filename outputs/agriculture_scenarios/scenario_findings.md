# Agricultural warehouse scenario simulation — findings

**All prices, storage costs, reserves, capacity and future price changes are illustrative assumptions. Historical crop stocks are derived from 50-сг 2025 reports, not direct warehouse-capacity measurements.**

- Baseline optimized net revenue: 399,517,385 UAH (reproduces notebook 04).
- Baseline gain vs **feasible reserve-only** alternative: 9,215,178 UAH.
- Capacity 40% objective: 397,291,340 UAH; capacity 100% objective: 401,389,644 UAH.
- Higher warehouse capacity cannot reduce the LP optimum with otherwise unchanged assumptions.
- Shadow prices are local derivatives, not global gains over large capacity changes.
- Insufficient capacity for mandatory crop reserves is explicitly flagged infeasible.
- This is a single-period, deterministic allocation of sell-now versus hold-for-later quantities, NOT route optimization or real farm profit forecasting.
