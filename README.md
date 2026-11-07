
# Forecasting and Decision Optimization

An end-to-end data science project combining time-series forecasting, agricultural data analysis, linear programming, explainable optimization, and scenario simulation.

The project demonstrates how historical data can support both predictive and prescriptive analytics:

- **Predictive analytics:** What is likely to happen?
- **Descriptive analytics:** What happened, and how did key indicators change?
- **Prescriptive analytics:** What decisions should be made under resource constraints?
- **Scenario analysis:** How do optimal decisions change under different assumptions?

The project consists of two complementary parts:

1. Retail sales forecasting using a Kaggle dataset.
2. Agricultural inventory analysis and warehouse allocation optimization using Ukrainian statistical reports.

---

## 1. Project Objectives

The main objectives are to:

1. Analyze historical retail sales and agricultural production data.
2. Develop and compare classical, machine learning, and deep learning forecasting models.
3. Evaluate forecasting performance using appropriate time-series validation.
4. Extract and analyze agricultural production, cost, and inventory data.
5. Implement a linear programming model for inventory allocation.
6. Provide explainable, data-driven decision recommendations.
7. Simulate alternative warehouse management scenarios.
8. Ensure reproducibility through structured notebooks and automated CI checks.

---

## 2. Repository Structure

```text
forecasting-and-decision-optimization/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── notebooks/
│   │
│   ├── 01_retail_data_audit.ipynb
│   ├── 02_classical_forecasting.ipynb
│   ├── 03_calendar_state_space_forecasting.ipynb
│   ├── 04_ml_forecasting.ipynb
│   ├── 05_dl_forecasting.ipynb
│   ├── 06_nbeats_tft_forecasting.ipynb
│   ├── 07_model_comparison_and_test.ipynb
│   │
│   ├── 01_agriculture_pdf_extraction.ipynb
│   ├── 02_agriculture_costs_inventory.ipynb
│   ├── 03_agriculture_eda.ipynb
│   ├── 04_agriculture_optimization.ipynb
│   └── 05_agriculture_scenarios.ipynb
│
├── data/
│   └── agriculture/
│       ├── raw/                  # Local source PDF reports
│       └── processed/            # Generated structured datasets
│
├── outputs/
│   ├── agriculture_eda/
│   ├── agriculture_optimization/
│   └── agriculture_scenarios/
│
├── requirements.txt
├── README.md
├── .gitignore
└── LICENSE
```

The retail notebooks follow a separate forecasting workflow.

Agricultural notebooks are numbered independently and should be executed in ascending order.

Raw agricultural reports and processed source datasets are excluded from version control to protect potentially sensitive enterprise information.

---

# Part I. Retail Sales Forecasting

## 3. Retail Dataset and Exploratory Analysis

The first part of the project focuses on daily retail sales forecasting using historical data from Kaggle.

The forecasting workflow begins with data auditing and exploratory analysis.

Main activities include:

- Inspecting dataset structure and data types.
- Checking missing values and duplicate observations.
- Examining daily sales patterns.
- Investigating trends and seasonality.
- Identifying calendar-related effects.
- Preparing chronological training and evaluation periods.

**Notebook:**

`01_retail_data_audit.ipynb`

The cleaned and prepared data provide the foundation for the subsequent forecasting experiments.

---

## 4. Classical Forecasting

Classical statistical approaches provide interpretable benchmarks for evaluating more complex models.

The forecasting experiments include traditional time-series modeling techniques and calendar-aware approaches.

Key concepts covered in the forecasting workflow include:

- Trend and seasonality.
- Autocorrelation and temporal dependence.
- Moving averages and exponential smoothing.
- Autoregressive and integrated models.
- Seasonal forecasting.
- Calendar effects.
- State-space representations.

**Notebooks:**

- `02_classical_forecasting.ipynb`
- `03_calendar_state_space_forecasting.ipynb`

These methods provide reference points against which machine learning and deep learning models can be evaluated.

---

## 5. Machine Learning Forecasting

Machine learning forecasting transforms a time series into a supervised learning problem.

Predictive information may include:

- Lagged observations.
- Rolling statistics.
- Calendar features.
- Day-of-week effects.
- Historical sales patterns.
- Other features available at prediction time.

**Notebook:**

`04_ml_forecasting.ipynb`

The experiments investigate how machine learning methods can capture relationships that may be difficult to represent using purely classical forecasting approaches.

To avoid data leakage, features must use information available at each forecast origin.

---

## 6. Deep Learning Forecasting

Neural forecasting models are investigated to capture temporal dependencies and nonlinear patterns in retail sales.

The project includes deep learning experiments and advanced neural forecasting architectures.

**Notebooks:**

- `05_dl_forecasting.ipynb`
- `06_nbeats_tft_forecasting.ipynb`

The advanced forecasting stage includes:

### N-BEATS

N-BEATS is a neural architecture designed for time-series forecasting using stacked blocks that generate forecast contributions.

### Temporal Fusion Transformer (TFT)

TFT is an attention-based architecture designed for multi-horizon forecasting and the integration of different types of temporal information.

The neural forecasting experiments examine model performance and computational complexity.

---

## 7. Forecast Model Comparison

The final forecasting stage compares the implemented models using chronological evaluation procedures.

**Notebook:**

`07_model_comparison_and_test.ipynb`

The evaluation focuses on:

- Forecast accuracy.
- Generalization to unseen periods.
- Performance across stores.
- Model complexity.
- Stability across validation windows.
- Final test performance.

Common forecasting error measures include:

- Mean Absolute Error (MAE).
- Root Mean Squared Error (RMSE).
- Percentage-based error metrics, where appropriate.

The final model selection should be based on validation results rather than test-set optimization.

Detailed experimental results are available in the forecasting notebooks.

---

# Part II. Agricultural Data Analysis and Optimization

## 8. Agricultural Dataset

The second part uses annual statistical reports from an agricultural enterprise in Ukraine.

Two official statistical reporting forms are analyzed:

| Form | Description |
|------|-------------|
| 29-сг | Agricultural crop areas and production |
| 50-сг | Agricultural production costs and economic indicators, including product movement |

The dataset covers:

**2021–2025**

The reports contain information about:

- Crop production.
- Sown and harvested areas.
- Crop yields.
- Production costs.
- Material and labor expenses.
- Inventory balances and movements.

The analysis focuses on six crops that have matched inventory and cost records:

- Wheat.
- Maize.
- Barley.
- Rapeseed.
- Soybeans.
- Sunflower.

### Data limitations

The agricultural reports contain annual observations rather than daily or monthly time series.

Therefore, the agricultural component focuses primarily on descriptive analysis and decision optimization instead of fitting complex forecasting models to five annual observations.

The reports do not provide all parameters required for real-world warehouse optimization, such as physical storage capacity, future selling prices, and storage tariffs.

These missing parameters are explicitly modeled as illustrative assumptions.

---

## 9. PDF Extraction and Data Preparation

### Notebook 01: Agricultural PDF Extraction

`01_agriculture_pdf_extraction.ipynb`

This notebook extracts structured information from the original PDF reports.

Main operations:

1. Load the archive containing agricultural reports.
2. Identify document types and reporting years.
3. Extract table rows and numerical fields.
4. Normalize data types and measurement units.
5. Preserve references to original report pages.
6. Perform initial quality checks.
7. Export structured CSV datasets.

Main output:

`data/agriculture/processed/crop_production.csv`

Additional intermediate extraction files support auditing and source verification.

### Notebook 02: Costs and Inventory Processing

`02_agriculture_costs_inventory.ipynb`

This notebook processes production costs and inventory movements from form 50-сг.

It performs:

- Cost extraction.
- Inventory extraction.
- Data cleaning and standardization.
- Crop code mapping.
- Inventory balance validation.
- Cross-dataset integration.

Main outputs:

```text
data/agriculture/processed/
├── production_costs.csv
├── inventory_flows.csv
├── agriculture_panel.csv
├── agriculture_qa.csv
└── extraction_review.csv
```

The integrated agricultural panel is used in subsequent analysis and optimization.

---

## 10. Agricultural Exploratory Data Analysis

**Notebook:**

`03_agriculture_eda.ipynb`

The EDA investigates agricultural production, costs, and inventory dynamics.

### 10.1 Data Quality

The analysis examines:

- Missing values.
- Dataset coverage.
- Reporting years.
- Duplicate records.
- Extraction warnings.
- Consistency of inventory calculations.

Missing values are not automatically replaced with zero.

### 10.2 Crop Production

Crop production and yield trends are analyzed across 2021–2025.

The production analysis distinguishes individual crop records from aggregate reporting categories to avoid double counting.

The extracted production subset is not presented as a complete enterprise-wide production total.

### 10.3 Production Costs

The analysis examines:

- Total production costs.
- Material expenses.
- Labor expenses.
- Other direct and overhead costs.
- Cost differences across crops.
- Changes in cost structure over time.

Monetary values are reported in nominal thousand UAH.

Historical cost changes should not automatically be interpreted as changes in operational efficiency because inflation and other external factors are not fully controlled.

### 10.4 Inventory Analysis

Inventory movement is analyzed using:

```text
Derived closing stock =
    Opening stock
    + Inventory inflow
    - Inventory outflow
```

The analysis also investigates:

- Inventory composition.
- Outflow volumes.
- Closing-stock-to-outflow ratios.
- Relative inventory shares.
- Differences between crop categories.

A logarithmic scale is used for the stock-to-outflow ratio chart because one extreme observation would otherwise obscure the remaining data.

### EDA Outputs

```text
outputs/agriculture_eda/
├── 01_missingness.png
├── 02_harvest_by_crop.png
├── 03_yield_by_crop.png
├── 04_cost_structure.png
├── 05_costs_by_crop.png
├── 06_closing_stocks.png
├── 07_inventory_outflows_and_ratio.png
├── 08_latest_inventory_ranking.png
├── data_coverage.csv
├── inventory_eda_metrics.csv
├── latest_inventory_metrics.csv
├── missingness.csv
└── eda_summary.md
```

---

## 11. Agricultural Inventory Optimization

**Notebook:**

`04_agriculture_optimization.ipynb`

### 11.1 Optimization Problem

The optimization problem determines how agricultural inventory should be allocated between immediate sales and future storage.

The goal is to maximize hypothetical net revenue under limited storage capacity.

The model uses Linear Programming (LP).

### 11.2 Decision Variables

For each crop i:

- q_i: available stock, in tonnes.
- x_i: quantity held for later sale.
- q_i - x_i: quantity sold immediately.

### 11.3 Objective Function

The model maximizes:

```text
Net revenue =
    Revenue from immediate sales
    + Expected future sales revenue
    - Holding costs
```

Mathematically:

```text
Maximize:

SUM_i [
    p_now_i * (q_i - x_i)
    + (p_later_i - h_i) * x_i
]
```

Where:

- p_now_i: assumed immediate selling price per tonne.
- p_later_i: assumed future selling price per tonne.
- h_i: assumed incremental holding cost per tonne.

Since immediate-sale revenue for the entire available stock is constant, the equivalent incremental objective is:

```text
Maximize:

SUM_i [
    (p_later_i - p_now_i - h_i) * x_i
]
```

### 11.4 Constraints

The model includes:

**Available stock:**

```text
0 <= x_i <= q_i
```

**Minimum inventory reserves:**

```text
x_i >= reserve_fraction * q_i
```

**Warehouse capacity:**

```text
SUM_i (space_i * x_i) <= capacity
```

Where `space_i` represents an illustrative space planning coefficient.

The coefficients are not measured warehouse cubic meters.

### 11.5 Optimization Method

The linear program is solved using:

`scipy.optimize.linprog(method="highs")`

The solver returns:

- Optimal quantities sold immediately.
- Optimal quantities retained in storage.
- Objective function value.
- Capacity utilization.
- Binding constraints.
- Sensitivity information.

---

## 12. Optimization Results

The optimization uses derived closing inventory for 2025.

### Baseline Inventory

Six matched crops provide approximately:

**37,399.5 tonnes of available inventory.**

### Illustrative Baseline Configuration

- Warehouse capacity: 60% of the space required to hold all available stock.
- Minimum reserve: 10% of each crop's available inventory.
- Selling prices: illustrative assumptions.
- Future price changes: illustrative assumptions.
- Holding costs: illustrative assumptions.

### Baseline Optimization Results

| Metric | Result |
|--------|--------|
| Available inventory | 37,399.5 tonnes |
| Optimized net revenue | 399,517,385 UAH |
| Gain over feasible reserve-only baseline | 9,215,178 UAH |
| Warehouse capacity utilization | Approximately 100% |
| Capacity shadow price | 296 UAH per additional planning space unit |

These results are generated under hypothetical economic parameters and must not be interpreted as actual enterprise profit, validated market forecasts, or operational recommendations.

### Allocation Interpretation

Under the illustrative baseline assumptions, the model prioritizes crops with higher marginal benefit per storage-space unit.

Soybeans, sunflower, and rapeseed are fully retained in the optimal solution.

Wheat receives substantial storage allocation, while barley and maize remain at their minimum reserve levels.

This allocation follows from the assumed price differences, holding costs, storage coefficients, and capacity constraint.

---

## 13. Explainability and Prescriptive Analytics

The project includes an explainability layer for understanding optimization outcomes.

The explainability analysis focuses on:

### Marginal Economic Benefit

For each crop:

```text
Marginal benefit per held tonne =
    Future selling price
    - Current selling price
    - Holding cost
```

### Benefit per Storage Unit

```text
Benefit per storage unit =
    Marginal benefit per held tonne
    / Storage space coefficient
```

### Binding Constraints

The model identifies:

- Crops held at their minimum reserve.
- Crops stored up to their available quantity.
- Crops receiving intermediate allocations.
- Whether total warehouse capacity is fully utilized.

### Shadow Prices

Shadow prices represent the local marginal value of relaxing an optimization constraint.

For the baseline scenario, the warehouse capacity shadow price is approximately:

**296 UAH per additional planning space unit.**

This value is local to the current optimal solution and does not imply a constant benefit for arbitrarily large capacity expansions.

### Prescriptive Interpretation

The optimization model converts data into conditional recommendations about:

- Which crops should receive storage priority.
- Which crops could be sold immediately.
- How warehouse capacity should be allocated.
- Which resource constraints influence decisions.
- How additional capacity could affect economic outcomes.

The recommendations depend on the assumed economic parameters.

---

## 14. Warehouse Scenario Simulation

**Notebook:**

`05_agriculture_scenarios.ipynb`

This notebook performs scenario analysis using the same linear programming formulation as the baseline optimization model.

The model is re-optimized under different assumptions.

### Scenarios

| Scenario | Modification |
|----------|--------------|
| Baseline | 60% warehouse capacity |
| Capacity 40% | Reduced storage capacity |
| Capacity 50% | Reduced storage capacity |
| Capacity 75% | Increased storage capacity |
| Capacity 100% | Full reference storage capacity |
| Higher holding costs | Holding costs increase by 30% |
| Lower price levels | Assumed prices decrease by 20% |
| Lower future price growth | Future price changes decrease by 5 percentage points |
| Lower supply | Available inventory decreases by 20% |
| Infeasible capacity | Warehouse capacity falls to 5% |

### Selected Scenario Results

| Scenario | Optimized net revenue (UAH) |
|----------|----------------------------:|
| Capacity 40% | 397,291,340 |
| Baseline 60% | 399,517,385 |
| Capacity 75% | 400,297,392 |
| Capacity 100% | 401,389,644 |
| Higher holding costs | 396,796,837 |

The 5% capacity scenario is infeasible because the available storage capacity cannot accommodate mandatory minimum reserves.

The lower-supply and lower-price scenarios alter the underlying economic conditions. Therefore, changes in objective value should not be interpreted exclusively as the effect of warehouse allocation.

### Scenario Findings

The analysis demonstrates that:

1. Increasing available storage capacity cannot reduce the optimal objective when all other model parameters remain unchanged.
2. Higher holding costs reduce the attractiveness of storing inventory.
3. Lower future price growth can reduce optimal warehouse utilization.
4. Mandatory inventory reserves can make low-capacity scenarios infeasible.
5. Marginal capacity values depend on which constraints are binding.

These results demonstrate sensitivity to modeling assumptions, not predicted market outcomes.

### Scenario Outputs

```text
outputs/agriculture_scenarios/
├── 01_gain_over_reserve_only.png
├── 02_capacity_sensitivity.png
├── 03_held_volume_by_capacity.png
├── scenario_summary.csv
├── scenario_allocations.csv
├── scenario_vs_baseline_by_crop.csv
├── scenario_explainability.csv
├── scenario_definitions.json
└── scenario_findings.md
```

---

# Part III. Technical Implementation

## 15. Technologies

The project uses Python and the following libraries.

| Category | Libraries |
|----------|-----------|
| Data processing | NumPy, pandas |
| Visualization | Matplotlib, Seaborn |
| Statistical forecasting | statsmodels, Prophet |
| Machine learning | scikit-learn |
| Deep learning | PyTorch, NeuralForecast |
| Optimization | SciPy / HiGHS |
| PDF extraction | PyMuPDF |
| Notebooks | Jupyter |
| Testing and CI | pytest, Ruff, GitHub Actions |

Additional dependencies are listed in `requirements.txt`.

---

## 16. Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/dasha-pn/forecasting-and-decision-optimization.git

cd forecasting-and-decision-optimization
```

### Step 2: Create a Virtual Environment

Python 3.11 is recommended.

```bash
python3.11 -m venv .venv
```

Activate it.

macOS/Linux:

```bash
source .venv/bin/activate
```

Windows:

```bash
.venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Check for dependency conflicts:

```bash
python -m pip check
```

### Step 4: Start Jupyter

```bash
jupyter lab
```

Open the required notebook and execute its cells in order.

---

## 17. Reproducing the Agricultural Analysis

### Required Input

Place the source archive containing the agricultural reports at:

```text
data/agriculture/raw/data_pdf.zip
```

The archive should contain both reporting forms for each year from 2021 to 2025.

The source archive is not included in the current repository.

### Execution Order

Run:

```text
1. notebooks/01_agriculture_pdf_extraction.ipynb

2. notebooks/02_agriculture_costs_inventory.ipynb

3. notebooks/03_agriculture_eda.ipynb

4. notebooks/04_agriculture_optimization.ipynb

5. notebooks/05_agriculture_scenarios.ipynb
```

Each notebook should be executed using **Run All**.

The first two notebooks generate the processed datasets required by the subsequent notebooks.

Notebook 04 produces the baseline optimization artifacts used by notebook 05.

### Output Directories

```text
data/agriculture/processed/

outputs/agriculture_eda/

outputs/agriculture_optimization/

outputs/agriculture_scenarios/
```

Some derived analysis artifacts may be included in the repository, but the complete workflow requires the original input files to reproduce them.

---

## 18. Reproducing the Retail Forecasting Analysis

The retail forecasting experiments should be executed in the following order:

```text
01_retail_data_audit.ipynb
02_classical_forecasting.ipynb
03_calendar_state_space_forecasting.ipynb
04_ml_forecasting.ipynb
05_dl_forecasting.ipynb
06_nbeats_tft_forecasting.ipynb
07_model_comparison_and_test.ipynb
```

The notebooks may depend on locally generated datasets and intermediate forecasting outputs.

Inspect the input-path configuration in the first retail notebook and supply the corresponding Kaggle dataset before reproducing the complete forecasting pipeline.

The retail source dataset is not bundled with this repository.

Deep learning experiments may require additional computation time and access to a suitable runtime.

---

## 19. Continuous Integration

The repository uses GitHub Actions for automated checks.

Workflow:

`.github/workflows/ci.yml`

The workflow is configured to run on:

- Pushes to `main`.
- Pull requests targeting `main`.
- Manual workflow dispatch.

The CI configuration includes:

1. Python environment setup.
2. Dependency installation.
3. Jupyter notebook structure validation.
4. Notebook code-cell syntax checks.
5. Python module compilation where applicable.
6. Tests when a test suite is present.
7. Selected Ruff lint checks for Python source modules.

### Important Limitation

The current CI workflow validates notebook structure and code syntax but does not execute the complete forecasting or agricultural pipelines.

End-to-end execution requires datasets and potentially substantial computational resources.

Passing CI therefore does not guarantee that every notebook can reproduce all numerical results on a new machine.

---

# Part IV. Interpretation and Limitations

## 20. Project Contributions

The project demonstrates the relationship between forecasting and decision optimization.

### Predictive Analytics

Historical retail sales are modeled using statistical, machine learning, and neural forecasting approaches.

### Descriptive Analytics

Agricultural reports are transformed into structured datasets and analyzed to identify production, cost, and inventory patterns.

### Prescriptive Analytics

Linear programming identifies an optimal allocation of agricultural products between immediate sales and future storage under explicit assumptions.

### Explainability

Marginal benefits, storage priorities, active constraints, and shadow prices provide transparent explanations of the optimization decisions.

### Scenario Simulation

Alternative storage capacities, prices, costs, and available inventory quantities are used to examine the sensitivity of the optimization results.

---

## 21. Limitations

### Retail Forecasting

Forecasting quality depends on:

- Historical data coverage.
- Feature availability.
- Validation design.
- Model assumptions.
- Changes in future sales behavior.

Forecasting performance observed on historical data does not guarantee future accuracy.

### Agricultural Data

The agricultural component is limited by:

- Five annual reporting periods.
- Missing fields in some crop records.
- Differences between reporting-form layouts.
- Incomplete historical production extraction for some crops.
- Source verification requirements.

Some PDF extraction results remain subject to manual source-document review.

### Optimization Assumptions

The optimization model assumes:

- A single decision period.
- Deterministic available inventory.
- Illustrative selling prices.
- Illustrative future price changes.
- Illustrative holding costs.
- Illustrative warehouse capacity.
- Fixed minimum inventory reserves.

The model does not explicitly include:

- Transportation network routing.
- Warehouse locations.
- Storage facility operating schedules.
- Real physical storage volumes.
- Product quality degradation.
- Detailed demand constraints.
- Transaction costs or financing constraints.
- Stochastic market-price forecasting.

### Interpretation

The calculated optimization gains are conditional results of the mathematical model.

They are not verified financial gains or recommendations for real commercial operations.

Actual deployment would require validated market prices, facility specifications, operational constraints, and domain-expert review.

---

## 22. Future Improvements

Potential extensions include:

- Integrating actual warehouse capacities and storage tariffs.
- Incorporating historical market prices.
- Using probabilistic or scenario-based price forecasts.
- Adding uncertainty-aware optimization.
- Modeling multiple warehouses.
- Integrating transportation costs.
- Introducing a multi-period inventory planning horizon.
- Connecting forecasting outputs directly to optimization decisions.
- Developing an interactive analytics dashboard.
- Adding automated data extraction and optimization tests.
- Expanding reproducibility checks in CI.

---

## 23. Conclusion

This project combines forecasting, statistical analysis, and optimization within one applied data science workflow.

The retail component investigates how different forecasting methods can be developed, evaluated, and compared.

The agricultural component demonstrates how structured enterprise data can support interpretable resource allocation decisions.

By combining exploratory analysis, linear programming, explainability, and scenario simulation, the project illustrates the transition from understanding historical data to making conditional, quantitatively justified decisions.

---

## License

See the `LICENSE` file for repository licensing information.

The repository license does not automatically grant permission to redistribute third-party datasets or confidential agricultural reports.
