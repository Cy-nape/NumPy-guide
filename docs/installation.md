# Environment Setup & Installation Guide

This guide will help you configure a clean Python environment for running this NumPy guide on macOS, Windows, or Linux.

---

## 1. Prerequisites

Make sure you have Python 3.10 or higher installed. You can check your version in your terminal:

```bash
python3 --version
# or on Windows:
python --version
```

If you don't have Python installed, download it from [python.org](https://www.python.org/downloads/).

---

## 2. Setting Up a Virtual Environment

Using a virtual environment isolates project dependencies and keeps your global Python installation clean.

### macOS & Linux

```bash
# 1. Navigate to the project directory
cd NumPy

# 2. Create a virtual environment named 'venv'
python3 -m venv venv

# 3. Activate the virtual environment
source venv/bin/activate
```

### Windows (Command Prompt or PowerShell)

```powershell
# 1. Navigate to the project directory
cd NumPy

# 2. Create a virtual environment named 'venv'
python -m venv venv

# 3. Activate the virtual environment
# In PowerShell:
venv\Scripts\Activate.ps1
# Or in Command Prompt (cmd.exe):
venv\Scripts\activate.bat
```

> **Tip:** Once activated, your terminal prompt will show `(venv)` at the beginning of the line.

---

## 3. Installing Dependencies

With your virtual environment active, run:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

This installs:
- **`numpy`**: High-performance array computing
- **`matplotlib`**: 2D plotting and data visualization
- **`jupyter` & `ipykernel`**: Interactive Jupyter Notebook environment

---

## 4. Registering Kernel with Jupyter (Optional but Recommended)

To ensure Jupyter runs inside your `venv` kernel:

```bash
python -m ipykernel install --user --name=numpy-guide --display-name="Python (NumPy Guide)"
```

---

## 5. Launching Jupyter Notebooks

From the project root directory, launch Jupyter:

```bash
jupyter notebook
```

Or if you prefer JupyterLab:

```bash
pip install jupyterlab
jupyter lab
```

Your browser will automatically open at `http://localhost:8888`. Click on `phase-1.ipynb` or `numpy_masterclass.ipynb` to start learning!

---

## 6. Verification

Inside a notebook or python shell, test your installation:

```python
import numpy as np
import matplotlib.pyplot as plt

print(f"NumPy Version: {np.__version__}")
print(f"Sample Array: {np.array([1, 2, 3])}")
```

If no errors appear, your environment is ready.
