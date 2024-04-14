# FactorLib

FactorLib is a Python library designed for efficient and scalable factor analysis and walk-forward optimization (WFO) in quantitative finance. 

## Features

*   **Parallel Processing:** Leverages Ray for parallel data processing, enabling faster factor creation and model training.
*   **Customizable Factors:** Create custom factors by extending the `BaseFactor` class and implementing the `generate_data` method.
*   **Walk-Forward Optimization:** Perform WFO with various machine learning models (e.g., LightGBM, XGBoost) to evaluate factor performance.
*   **Portfolio Optimization:** Supports multiple portfolio optimization methods, including Mean-Variance Optimization (MVO), Hierarchical Risk Parity (HRP), and Inverse Variance weighting.
*   **Performance Analysis:** Generate comprehensive performance statistics and visualizations using QuantStats and SHAP.

## Prerequisites

Before installing FactorLib, ensure you have the following dependencies installed:

*   pandas
*   numpy
*   scikit-learn
*   scipy
*   xgboost
*   ray
*   tqdm
*   jupyter
*   shap
*   catboost
*   lightgbm
*   QuantStats
*   matplotlib
*   pyarrow
*   fastparquet
*   ipywidgets
*   yfinance
*   prettytable

To install these dependencies using pip:

```bash
pip install -r requirements.txt
```

## Getting Started

### Installation

1.  Clone the repository:

```bash
git clone https://github.com/your_username_/Project-Name.git
```

2.  Install the required packages:

```bash
pip install -r requirements.txt
```

## Usage

The FactorLib codebase is organized into several modules, each serving a specific purpose:

*   **factorlib/base\_factor.py:** Provides the `BaseFactor` class, which serves as the foundation for creating custom factors.
*   **factorlib/factor.py:** Defines the `Factor` class, representing a single factor within the FactorModel.
*   **factorlib/factor\_model.py:** Contains the `FactorModel` class, responsible for managing factors, model training, and WFO.
*   **factorlib/stats.py:** Implements the `Statistics` class for performance analysis and reporting.
*   **factorlib/types.py:** Defines various enumerations and types used throughout the library.
*   **factorlib/utils/**: Contains utility functions and modules for data handling, system operations, and datetime manipulations.
*   **scripts/data/cleaner.py:** Provides scripts for cleaning and preprocessing raw data.
*   **system\_test.py:** Offers an example of how to use FactorLib for factor analysis and WFO.

To get started, you can follow these steps:

1.  **Create Custom Factors:** Extend the `BaseFactor` class and implement the `generate_data` method to define your factor logic.
2.  **Prepare Data:** Ensure your data is formatted according to the requirements of the `Factor` class.
3.  **Build Factor Model:** Instantiate a `FactorModel` and add your custom factors using the `add_factor` method.
4.  **Walk-Forward Optimization:** Call the `wfo` method on your FactorModel to perform WFO and evaluate factor performance.
5.  **Analyze Results:** Use the `Statistics` class to generate performance reports and visualizations.

## Example Usage

The `system_test.py` script demonstrates a basic example of using FactorLib:

```python
import pandas as pd
from datetime import datetime
from factorlib.factor import Factor
from factorlib.factor_model import FactorModel
from factorlib.types import PortOptOptions, ModelType
from factorlib.utils.system import get_raw_data_dir, get_experiments_dir

# ... (load data and create factors) ...

factor_model = FactorModel(name='test_00', tickers=tickers, interval=INTERVAL, model_type=ModelType.lightgbm)

# ... (add factors to the model) ...

stats = factor_model.wfo(returns,
                         train_interval=pd.DateOffset(years=5), train_freq='M', anchored=False,
                         start_date=datetime(2017, 1, 5), end_date=datetime(2022, 12, 20),
                         candidates=candidates,
                         save_dir=get_experiments_dir(), **kwargs,
                         port_opt=PortOptOptions.MeanVariance)
```

This script loads sample data, creates factors, builds a factor model, performs WFO, and generates performance statistics. 

## Contributing

Contributions to FactorLib are welcome! Please refer to the contribution guidelines for more information.
