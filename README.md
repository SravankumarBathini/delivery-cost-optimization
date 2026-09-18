# 📦 E-Commerce Dynamic Delivery Cost Optimization Engine

## 🏢 Business Case Overview
This project builds a production-grade **Continuous Regression Pipeline** designed to predict fluid delivery trip fees (`delivery_cost_usd`) for a large-scale e-commerce food delivery platform. 

In modern food logistics, static pricing models fail to protect profit margins during high-volatility events like lunch rushes or severe rainstorms. Conversely, overly aggressive pricing drives away customers. This engine resolves that tension by learning non-linear market behaviors to balance customer satisfaction with absolute corporate revenue security.

---

## 🏗️ Systems Architecture Map
The application is structured as an end-to-end decoupled data pipeline running on a local multi-threaded architecture:

1. **Parallel Synthesis Engine (`Polars`):** Compiles 100,000 transaction records utilizing multi-threaded execution loops. It bypasses global interpreter locks by leveraging high-speed Rust array allocations.
2. **Analytical Data Warehouse (`DuckDB` & `PyArrow`):** Instead of storing loose text sheets, data is cleanly indexed directly into an enterprise relational database binary (`delivery_warehouse.db`).
3. **Model Partitioning & Training (`scikit-learn`):** The model completely decouples from memory variables. It connects straight to the local database file via SQL queries, pulls the transaction matrix, splits it into isolated training and testing arrays (80/20 Split) to eliminate data leakage, and runs a bounded **Decision Tree Regressor**.
4. **Asset Serialization (`joblib`):** The final trained logic is compressed into a compact `5.86 KB` production-ready `.pkl` binary asset capable of microsecond deployments.

---

## 🛠️ Repository Layout
```text
delivery-cost-optimization/
├── data/
│   ├── delivery_warehouse.db     # DuckDB Relational Storage Ledger
│   └── raw_delivery_records.csv  # High-Speed Flat Backup Matrix
├── docs/
│   └── ml_concept_guide.md       # Layman Guide to ML Mathematics
├── models/
│   └── delivery_tree_v1.pkl      # Serialized Bounded Machine Learning Model (5.86 KB)
├── notebooks/
│   └── delivery_cost_engine.ipynb # Interactive Sandbox Development Pipeline
├── README.md                     # Technical Operations Overview
└── requirements.txt              # Frozen Package Infrastructure Manifest
```

---

## 🚀 Execution & System Deployment Guide
To initialize and re-run this entire system pipeline from absolute scratch on a fresh machine, run these PowerShell scripts sequentially:

```powershell
# 1. Establish the clean virtual environment sandbox
python -m venv hft_env
.\hft_env\Scripts\Activate.ps1

# 2. Deploy all frozen project packages in a single pass
pip install -r requirements.txt

# 3. Boot up VS Code and execute the delivery_cost_engine.ipynb notebook cells sequentially
code .
```
