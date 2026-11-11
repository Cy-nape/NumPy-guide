# 🚀 NumPy Learning Guide: Zero to Hero

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![NumPy](https://img.shields.io/badge/NumPy-2.x-013243.svg?logo=numpy&logoColor=white)](https://numpy.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange.svg?logo=jupyter)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Target Audience](https://img.shields.io/badge/Audience-Beginner%20to%20Intermediate-brightgreen.svg)]()

Welcome to the **NumPy Learning Guide** — an interactive, hands-on masterclass designed to take you from foundational array operations to advanced multi-dimensional computing, computer vision image manipulation, and performance optimization.

---

## 📚 Curriculum & Learning Path

| Phase | Notebook | Core Topics Covered |
|:---|:---|:---|
| **Phase 1** | [`phase-1.ipynb`](phase-1.ipynb) | Array architecture, memory layout, Python lists vs NumPy speed benchmarks, built-in generators (`zeros`, `ones`, `arange`, `linspace`, `randint`), shapes, reshaping, `.ravel()` vs `.flatten()`, transposing. |
| **Phase 2** | [`phase-2.ipynb`](phase-2.ipynb) | 1D & 2D slicing, the View vs. Copy hazard, sorting & ranking with `np.argsort()`, boolean masking (`&`, `\|`, `~`), fancy indexing, `np.where()` ternary labeling, `vstack`/`hstack`, retail business case study. |
| **Phase 3** | [`phase-3.ipynb`](phase-3.ipynb) | Vectorization with ufuncs, the Golden Rules of Broadcasting, axis mechanics (`axis=0` vs `axis=1`), aggregations, restaurant chain revenue case study with Matplotlib visualizations, vector math & cosine similarity. |
| **Phase 4** | [`phase-4.ipynb`](phase-4.ipynb) | High-performance binary persistence (`.npy`, compressed `.npz`), CSV I/O, images as ndarrays, procedural image generation, image inversion, ROI cropping, channel isolation, C-contiguous memory optimization. |
| **Complete** | [`numpy_masterclass.ipynb`](numpy_masterclass.ipynb) | **All-in-One Master Notebook**: The complete curriculum combined in a single cohesive workbook with an interactive Table of Contents. |

---

## 📂 Repository Structure

```text
NumPy-guide/
├── README.md                 # Project landing page and navigation
├── requirements.txt          # Python dependencies
├── .gitignore                # Protects against committing venv/ and cache
│
├── phase-1.ipynb             # Phase 1: Fundamentals & Array Architecture
├── phase-2.ipynb             # Phase 2: Indexing, Slicing & Stacking
├── phase-3.ipynb             # Phase 3: Vectorization, Broadcasting & Analytics
├── phase-4.ipynb             # Phase 4: File I/O & Image Array Processing
├── numpy_masterclass.ipynb   # Complete all-in-one workbook
│
└── docs/
    ├── installation.md       # Setup guide for macOS, Windows & Linux
    ├── cheat_sheet.md        # Quick reference syntax cheat sheet
    └── faq.md                # Common pitfalls (View vs Copy, Axis 0 vs 1, etc.)
```

---

## ⚡ Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/Cy-nape/NumPy-guide.git
cd NumPy-guide
```

### 2. Set Up Virtual Environment & Dependencies
```bash
# macOS / Linux:
python3 -m venv venv
source venv/bin/activate

# Windows (Command Prompt / PowerShell):
python -m venv venv
venv\Scripts\activate

# Install dependencies:
pip install -r requirements.txt
```

### 3. Launch the Interactive Notebooks
```bash
jupyter notebook
```
Open [`phase-1.ipynb`](phase-1.ipynb) to start with the fundamentals, or explore [`numpy_masterclass.ipynb`](numpy_masterclass.ipynb) for the full end-to-end journey!

---

## 📖 Supplemental Documentation

- 🛠️ **[Installation & Environment Setup](docs/installation.md)**: Detailed instructions for setting up Conda or virtualenv across all operating systems.
- 📋 **[NumPy Syntax Cheat Sheet](docs/cheat_sheet.md)**: Printable reference table of the most frequently used NumPy functions and methods.
- ❓ **[FAQ & Common Pitfalls](docs/faq.md)**: Clear explanations of subtle pitfalls like `axis=0` vs `axis=1`, broadcasting rules, and the View vs. Copy hazard.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to open an issue or submit a pull request if you find typos or have suggestions for new real-world case studies.

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
