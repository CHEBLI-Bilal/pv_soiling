
# 📘 SRR Model – Detailed User Guide

This guide provides step-by-step instructions for the **preparation, execution, and troubleshooting** of the SRR (Stochastic Rate and Recovery) model to quantify the soiling effect directly from PV production and meteorological data.

---

## 📂 1. File Preparation

### Required Files:
- **Excel file (.xlsx)** containing:
  - Timestamps in the format: `yyyy/mm/dd hh:mm:ss`
  - Active Power (P) in kW
  - Plane of Array Irradiance (POA) in W/m²
  - Global Horizontal Irradiance (GHI) in W/m²
  - Ambient Temperature (Ta) in °C
  - Cell Temperature (Tc) in °C
  - Wind Speed (Ws) in m/s

### Naming Conventions:
- The **Excel file name must not contain spaces.**
  Example: `Propre-Mono_12-2017_11-2018.xlsx` (✔️)
  Instead of: `Propre Mono 12-2017 11-2018.xlsx` (❌)

- The **column headers must exactly match** the variable names used in the Python code.
  Example: `timestamp` not `Timestamp`

### Data Formatting:
- Thousand separator: **comma**
- Decimal separator: **dot**
To change this in Excel:
`File > Options > Advanced > Uncheck "Use system separators" > Set custom separators`

### Example Format:
| timestamp            | Active Power | POA  | GHI  | Ta   | WS   | Tc   |
|----------------------|--------------|------|------|------|------|------|
| 2017/12/01 00:00:01  | 0.00         | 4.93 | 1.73 | 13.59| 0.13 | 13.15|

---

## 🛠️ 2. Software and Libraries Setup

### Recommended Environment:
- **VS Code** (recommended for better error tracking and faster execution)
- Python version: **≥ 3.7.0**
- Required Python libraries:
  - `numpy`
  - `pandas`
  - `matplotlib`
  - `openpyxl`
  - `pvlib`

### Installation Commands:
```bash
pip install numpy pandas matplotlib openpyxl pvlib
```

---

## ⚙️ 3. Model Files and Execution

### Model Source:
- Download from: [NREL pv_soiling GitHub](https://github.com/NREL/pv_soiling)

### Preparation:
- Create a **Jupyter Notebook named `SRR.ipynb`** and copy the code from `Soiling calcs demo` into it.
- The notebook should control variable initialization and library management.

### Interface:
- Recommended: **VS Code with Jupyter extension**
- Alternative: Jupyter Notebook (slower execution and less graphical compatibility)

---

## 🚧 4. Common Errors and Solutions

### 4.1 Excel Errors
- **Error:** "DataFrame object has no attribute"
  **Solution:** Check the exact column names and their spellings.

- **Error:** Date format is not recognized
  **Solution:** Dates must be in `yyyy/mm/dd hh:mm:ss` format.

- **Error:** Incorrect separators
  **Solution:** Adjust Excel separators as described above.

- **Error:** Unacceptable values (outliers, invalid temperatures, etc.)
  **Solution:** Replace extreme or impossible values with `'error'` to allow the code to skip them.

---

### 4.2 Python Function Errors
- **Issue:** Some functions in `pvlib.pvsystem` are not compatible with the SRR model.

#### Solution:
- Create a **new Python file**: `pvsystemtest.py`
- Copy the compatible code from: [pvlib version 0.6.3 pvsystem](https://pvlib-python.readthedocs.io/en/v0.6.3/_modules/pvlib/pvsystem.html)
- Remove `Docs` references from the code.
- Save `pvsystemtest.py` in:
  `C:\Python\Python310\Lib\site-packages\pvlib`

#### In your Jupyter Notebook:
```python
import sys
sys.path.append('C:\\Python\\Python310\\Lib\\site-packages\\pvlib')
import pvsystemtest as test
```

---

## 🔍 5. Important Notes
- Make sure the **data series covers at least 3 years** to achieve precise and reliable confidence intervals.
- Always double-check variable initialization and file paths in your Jupyter Notebook.
- Follow the correct order: file preparation ➜ interface setup ➜ library installation ➜ code execution.

---

## 📚 Additional Resources
Refer to the full methodology and detailed analysis in:
👉 [ AIP Paper (to be added)]

---

## ✉️ Contact
**Bilal Chebli**
📧 Bilal.Chebli@Student.HTW-Berlin.de
📧 bilal.chebli@um5r.ac.ma

