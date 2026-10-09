# Agentic AI Inventory Management System

### Predict. Plan. Execute. Improve.

An AI-assisted inventory management prototype that brings together **machine-learning demand forecasting**, **multi-agent decision workflows**, **stock monitoring**, and an interactive **Streamlit dashboard**.

Built around a **Planner → Executor → Reflector** architecture, the system explores how historical sales records and current inventory data can inform replenishment decisions, surface low-stock risks, and support operational reviews.

> **Project status:** Local, data-driven prototype. This repository contains a working dashboard and command-line workflows; it is **not** a production-ready procurement platform. Order-execution functionality should be tested with sample data before connecting real suppliers or financial systems.

**Repository:** [Agentic-Inventory-Management](https://github.com/Manik-Manohar/Agentic-Inventory-Management)  
**Original project:** [Jagannath-K/agentic-inventory-management](https://github.com/Jagannath-K/agentic-inventory-management)

---

## Contents

- [The Idea](#the-idea)
- [Core Capabilities](#core-capabilities)
- [System Workflow](#system-workflow)
- [Multi-Agent Architecture](#multi-agent-architecture)
- [Demand Forecasting](#demand-forecasting)
- [Inventory Monitoring and Operations](#inventory-monitoring-and-operations)
- [Interactive Dashboard](#interactive-dashboard)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Running the System](#running-the-system)
- [Configuration and Safety](#configuration-and-safety)
- [Data and Model Artifacts](#data-and-model-artifacts)
- [Example Local Run](#example-local-run)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Project Attribution](#project-attribution)
- [Disclaimer](#disclaimer)

## The Idea

Inventory decisions are often made reactively: a product is running low, someone notices the issue, and the business creates a purchase request. A more proactive workflow needs to answer several questions:

- Which products are at risk of running out?
- How has demand changed over time?
- How much stock may be needed in the coming days?
- Which items should be prioritized for replenishment?
- What happens after a proposed inventory action is executed?
- How can results be reviewed to improve subsequent decisions?

**Agentic AI Inventory Management System** combines inventory records, sales history, predictive models, and specialized software agents into a single experimental workflow.

The goal is to move from *viewing stock levels* to *generating, reviewing, and evaluating inventory decisions*.

## Core Capabilities

| Capability | Description |
|---|---|
| Multi-agent workflow | Separates inventory planning, execution, and performance review into three specialized agents |
| Demand forecasting | Uses historical sales information and machine-learning approaches to estimate future product demand |
| Inventory planning | Generates replenishment recommendations based on available stock and planning logic |
| Order-execution logic | Processes proposed inventory actions within the application's business-operation workflow |
| Stock tracking | Reads inventory records and supports sales and purchase transactions |
| Low-stock alerts | Includes threshold-based alert and email-notification components |
| Operational reporting | Generates analysis and optimization recommendations |
| Streamlit dashboard | Provides an interactive interface for exploring inventory information and system features |
| Configurable controls | Exposes thresholds, automatic-execution flags, budgeting limits, and other system settings |

## System Workflow

```text
       HISTORICAL SALES                  CURRENT STOCK
          data/sales.csv                  data/stock.csv
                 \                            /
                  \                          /
                   v                        v
                    DATA LOADING & ANALYSIS
                             |
                             v
                    DEMAND FORECASTING
                             |
                             v
                       PLANNER AGENT
                Inventory action proposals
                             |
                             v
                   REVIEW / CONFIGURATION
                Priorities and safety limits
                             |
                             v
                       EXECUTOR AGENT
                 Inventory/order operations
                             |
                             v
                      REFLECTOR AGENT
                  Results and recommendations
                             |
                             v
                    REPORTS & DASHBOARD
```

The stages describe the application's intended decision workflow. They should not be interpreted as evidence of a live enterprise resource planning (ERP) or supplier integration.

## Multi-Agent Architecture

The application separates responsibilities across three agent modules, with `main.py` coordinating the components.

### 1. Planner Agent — Decide what may be needed

**Location:** `agents/planner.py`

The Planner Agent analyzes inventory and demand-related information to produce proposed actions. Its role is to identify inventory needs and support decisions about reorder priorities and quantities.

**Typical questions:**
- Which products need attention?
- What stock position does the available data suggest?
- What replenishment actions should be considered first?

### 2. Executor Agent — Act on selected plans

**Location:** `agents/executor.py`

The Executor Agent handles execution logic for inventory plans within the application. It represents the action-oriented phase of the workflow, including order-handling and inventory-operation logic.

**Important:** The presence of an executor does **not** mean this repository has been verified to place live purchase orders with external suppliers. Test changes against disposable data first.

### 3. Reflector Agent — Evaluate and improve

**Location:** `agents/reflector.py`

The Reflector Agent reviews operating information and generates insights that can be used to assess stock-management performance and improve future planning.

**Typical questions:**
- What operational issues remain?
- Which areas require attention?
- What improvements does the analysis suggest?

### Orchestration

**Location:** `main.py`

The main application creates the Planner, Executor, Reflector, Demand Predictor, Shop Operations, and Notification System components. It provides an interactive command-line menu and commands for inventory cycles, model training, scheduling, and dashboard startup.

## Demand Forecasting

**Location:** `models/predictor.py`

The forecasting module uses historical sales data to estimate demand and support better inventory planning. The repository includes code paths for multiple regression-model approaches and saved prediction artifacts.

During one documented local test, the terminal reported training **Random Forest**, **Gradient Boosting**, and **Linear Regression** models for sample product `G005`.

| Model | Test MAE shown in that local run |
|---|---:|
| Random Forest | 0.53 |
| Gradient Boosting | 0.59 |
| Linear Regression | 0.57 |

> These are **example log results for one product and one run**, not independently validated benchmarks, a system-wide accuracy percentage, or a guarantee of future prediction quality. MAE (mean absolute error) is expressed in the target variable's units.

The forecasting configuration includes a default **30-day horizon**, minimum historical-data setting, and model-retraining interval. Actual output depends on dataset coverage, model training, and application logic.

## Inventory Monitoring and Operations

**Locations:** `models/shop_operations.py`, `models/notification_system.py`

The system works with inventory and sales records to support:

- Reviewing current stock and product availability
- Flagging inventory at or below configured thresholds
- Entering sales that decrease stock
- Entering purchases/restocks that increase stock
- Generating inventory-related analytics and reports
- Producing alert messages when configured conditions are met

Email alert delivery requires valid configuration and should be verified independently before relying on it for business operations.

## Interactive Dashboard

**Location:** `ui/app.py`

The dashboard is built with **Streamlit**, with charting and tabular views for exploring the inventory-management workflow. It allows users to examine the system through a browser rather than only through the command line.

### Run locally

```powershell
python -m streamlit run ui/app.py
```

Then open **http://localhost:8501**.

### Dashboard screenshots

Add screenshots captured from your actual local application to `docs/screenshots/`, then uncomment and update the links below:

<!--
![Inventory Dashboard Overview](docs/screenshots/dashboard-overview.png)
![Demand Forecasting](docs/screenshots/demand-forecasting.png)
![Agent Planning](docs/screenshots/agent-planning.png)
-->

**Demo:** A public hosted dashboard URL has not been included. The GitHub repository hosts the *source code*; it does not automatically host the running Streamlit application.

## Technology Stack

| Area | Technology |
|---|---|
| Primary language | Python |
| Data handling | Pandas, NumPy |
| Machine learning | Scikit-learn |
| Scientific computing | SciPy (installed as a dependency) |
| Visualization | Streamlit, Plotly |
| Model serialization | Joblib / `.pkl` artifacts |
| Configuration | JSON, `python-dotenv` |
| Data storage | CSV files |
| Version control | Git, GitHub |
| Local development | Cursor or another Python-capable editor |

## Project Structure

```text
Agentic-Inventory-Management/
|
|-- agents/
|   |-- __init__.py
|   |-- planner.py                 # Inventory planning
|   |-- executor.py                # Action execution
|   `-- reflector.py               # Review and optimization
|
|-- data/
|   |-- sales.csv                  # Historical sales information
|   `-- stock.csv                  # Inventory records
|
|-- models/
|   |-- __init__.py
|   |-- predictor.py               # Demand forecasting logic
|   |-- shop_operations.py         # Sales, purchases, stock operations
|   |-- notification_system.py     # Alert functions
|   |-- demand_predictor_*.pkl     # Serialized model artifacts
|   `-- last_training.txt          # Training metadata
|
|-- ui/
|   `-- app.py                     # Streamlit dashboard
|
|-- .env.example                   # Safe environment template
|-- .gitignore                     # Excluded local/generated files
|-- config.json                    # Inventory and system settings
|-- main.py                        # CLI and orchestration
|-- requirements.txt               # Python dependencies
|-- QUICK_START.md                 # Setup notes
|-- SECURITY.md                    # Security notes
|-- run.bat                        # Windows runner
|-- run.sh                         # Unix/Linux runner
|-- setup-security.ps1             # PowerShell setup helper
|-- setup-security.sh              # Shell setup helper
`-- README.md
```

## Getting Started

### Prerequisites

- Windows, macOS, or Linux with Python installed
- Python 3.11 or newer as a starting point; library compatibility varies by version
- Git (recommended)
- An internet connection for downloading dependencies

**Verified local environment:** A Windows installation using **Python 3.13** and **Streamlit 1.65.0** successfully started the dashboard and exercised forecasting and agent-planning functionality. This is a local observation, not a full compatibility matrix.

### 1. Clone the repository

```bash
git clone https://github.com/Manik-Manohar/Agentic-Inventory-Management.git
cd Agentic-Inventory-Management
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on **Windows PowerShell**:

```powershell
.\.venv\Scripts\Activate.ps1
```

On **macOS/Linux**:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 4. Create the local environment file

**Windows PowerShell:**

```powershell
Copy-Item .env.example .env
```

**macOS/Linux:**

```bash
cp .env.example .env
```

Open `.env` and enter credentials **only** for optional integrations you intend to use. Do not upload it or publish real credentials.

### 5. Review settings before testing actions

In `config.json`, set the automatic execution flags to `false` for initial exploration:

```json
{
  "auto_execute_critical": false,
  "auto_execute_high": false,
  "auto_execute_medium": false
}
```

The snippet shows relevant settings only; **do not replace the full `config.json` with this partial snippet**. Edit the existing keys and keep the rest of the file intact.

### 6. Launch the dashboard

```bash
python -m streamlit run ui/app.py
```

Visit: **http://localhost:8501**

To stop the server, press **Ctrl+C** in the terminal that is running Streamlit.

## Running the System

The dashboard and command-line application can be used separately.

### Interactive terminal interface

```bash
python main.py
```

The menu includes:

| Option | Action |
|---:|---|
| 1 | Run an inventory cycle |
| 2 | Generate an analytics report |
| 3 | View system status |
| 4 | Start the automated scheduler |
| 5 | Train prediction models |
| 6 | Record daily sales/purchases |
| 7 | Update system settings |
| 8 | Test stock-alert email |
| 9 | View current stock levels |
| 10 | Exit |

### Command-line shortcuts

```bash
python main.py cycle
python main.py train
python main.py dashboard
python main.py scheduler
```

**Caution:** `cycle`, the automated scheduler, and transaction/ordering features may modify application data or execute internal actions. Use copies of sample data and review settings first. Do not treat the scheduler as a production-grade background service.

## Configuration and Safety

The repository includes a `config.json` file with planning and operational settings.

| Setting | Value in the published configuration | Meaning |
|---|---:|---|
| `auto_execute_critical` | `true` | Enables critical-priority auto-execution by default |
| `auto_execute_high` | `false` | High-priority automatic execution toggle |
| `max_daily_orders` | `20` | Configured daily order limit |
| `max_daily_budget` | `50000.0` | Configured daily budget number; do not assume a currency without checking deployment context |
| `run_interval_hours` | `6` | Configured scheduler interval |
| `default_low_stock_threshold` | `10` | Default low-stock threshold |
| `default_critical_stock_threshold` | `5` | Default critical-stock threshold |
| `default_forecast_days` | `30` | Forecasting setting under `forecasting_settings` |

The presence of configuration values does not, on its own, establish that every limit is enforced in every execution path. Validate safeguards before using live data.

### Security checklist

- Keep `.env` and all credentials out of version control.
- Use `.env.example` only as a template with placeholder values.
- Treat serialized `.pkl` files as potentially unsafe if obtained from untrusted sources; loading them can execute code.
- Verify the provenance of model files before loading them.
- Review dataset contents before making a public repository.
- Back up CSV files before experimenting with transactions or automated actions.
- Review [SECURITY.md](SECURITY.md) for the project's security setup notes.

## Data and Model Artifacts

The included repository contains:

- `data/sales.csv` — historical transaction information used by the application
- `data/stock.csv` — stock and product information
- `models/demand_predictor_*.pkl` — serialized prediction-related artifacts
- `models/last_training.txt` — metadata about model training

Models and outputs depend on the particular data supplied. Re-training or running the system can produce different results or update local files. No general accuracy or cost-savings claim is made here.

## Example Local Run

During local testing, the following actions were observed in application logs:

- Streamlit started successfully on `localhost:8501`.
- The demand prediction module loaded data and trained multiple models for sample product `G005`.
- The Planner Agent reported generating inventory plans for **20 products**.
- The Reflector Agent successfully loaded its data for analysis.

This confirms that significant parts of the prototype ran in the tested environment. It does not independently verify every dashboard action, procurement integration, forecast horizon, or production-reliability claim.

## Limitations

This repository should be treated as an exploratory inventory-management prototype:

1. **Sample-data dependence:** Forecast and planning outputs depend on the quality, recency, and representativeness of supplied CSV files.
2. **Forecast uncertainty:** The models can make incorrect predictions, especially for sparse, irregular, or changing demand.
3. **Supplier integration:** Execution-agent logic should not be assumed to represent a verified live supplier purchasing integration.
4. **No independent production validation:** There is no published evidence here of enterprise-scale deployment, SLA compliance, or business-wide savings.
5. **Local-file storage:** CSV-based storage has limitations for concurrent users, auditability, and transactional reliability.
6. **Automatic-action risk:** Configuration may permit inventory/order operations without manual approval; test carefully.
7. **Interface compatibility:** Newer Streamlit versions may show warnings about deprecated UI parameters such as `use_container_width`.
8. **Model portability and security:** Saved model objects may be version-sensitive and should only be loaded from trusted sources.

## Future Improvements

Potential next steps include:

- Add richer dataset validation and automated quality checks
- Benchmark forecast models across products and time periods
- Introduce consistent train/test backtesting for demand predictions
- Implement explicit human approval before executing purchasing decisions
- Add reorder-policy simulation with budget and stockout trade-offs
- Integrate a transactional database and proper audit logs
- Build authenticated multi-user access and permission controls
- Connect to supplier systems through tested, permissioned APIs
- Add automated unit, integration, and regression tests
- Containerize the application for reproducible deployment
- Improve monitoring, error handling, and alert delivery verification
- Deploy a demo dashboard with sanitized sample data
- Replace deprecated Streamlit API usage

These are improvement ideas, **not claims about features already completed**.

## Disclaimer

This is a learning and experimental software project. Inventory forecasts, stock alerts, generated plans, and execution decisions are decision-support outputs, not guarantees of availability, cost optimization, or financial performance. Validate the data, configuration, and operational consequences before applying the software to a real business.