# finite-element-analysis

[![python](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/)
![os](https://img.shields.io/badge/os-ubuntu%20|%20macos%20|%20windows-blue.svg)
[![license](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/sandialabs/sibl#license)

[![codecov](https://codecov.io/gh/Lejeune-Lab-Graduate-Course-Materials/finite-element-analysis/graph/badge.svg?token=p5DMvJ6byO)](https://codecov.io/gh/Lejeune-Lab-Graduate-Course-Materials/finite-element-analysis)
[![tests](https://github.com/Lejeune-Lab-Graduate-Course-Materials/finite-element-analysis/actions/workflows/tests.yml/badge.svg)](https://github.com/Lejeune-Lab-Graduate-Course-Materials/finite-element-analysis/actions)


### Conda environment, install, and testing

Note: this is an extremely minimalist readme, but the code is highly documented and will get built out over the coures of assignment 3.

```bash
conda create --name finite-element-analysis-env python=3.12.9
```

```bash
conda activate finite-element-analysis-env
```

```bash
python --version
```

```bash
pip install --upgrade pip setuptools wheel
```

```bash
pip install -e .
```

```bash
pytest -v --cov=finiteelementanalysis --cov-report term-missing
```

# Finite Element Analysis Codebase - Overview


This repository implements a modular 2D Finite Element Analysis (FEA) solver from scratch, with capabilities to solve problems like linear elasticity and hyperelasticity. It is designed for flexibility, educational clarity, and extensibility. A complete example, `full_code_example_1.py`, is provided to demonstrate its usage on a hyperelastic uniaxial extension problem.

---

## 🚀 Code Workflow

### 1. Pre-processing (`pre_process.py`)
- **functionality**: Generates mesh and sets up boundary conditions.
  - `generate_rect_mesh(...)`: Create structured 2D rectangular meshes.
  - `get_dirichlet_nodes(...)`: Determine nodes on domain boundaries.

### 2. Discretization (`discretization.py`)
- **functionality**: Defines basis functions, numerical integration schemes.
- **Core Components**:
  - Basis function evaluations.
  - Gauss quadrature rules.

### 3. Local Element Calculations (`local_element.py`)
- **functionality**: Computes local element stiffness and force vectors.
  - Uses shape function gradients.
  - Handles nonlinear strain energy density functions (for hyperelasticity).

### 4. Global Assembly (`assemble_global.py`)
- **functionality**: Assembles global sparse matrices from local contributions.
  - Efficient sparse matrix handling.
  - Element-to-global DOF mapping.

### 5. Solver (`solver.py`)
  - Newton-Raphson nonlinear solver for hyperelasticity.
  - Applies Dirichlet and Neumann boundary conditions.

### 6. Visualization (`visualize.py`)
  - Plot deformed meshes.
  - Visualize displacement and stress fields.

### 7. Examples and Validation (`example_functions.py`)
- Provides reference solutions and load cases.
- Useful for unit testing and convergence checks.

---

## 📖 Tutorial Example: `full_code_example_1.py`

This file walks through solving a 2D **hyperelastic uniaxial extension** problem using the framework.

### Problem Setup
- **Domain**: Rectangle with length `L` and height `H`.
- **Boundary Conditions**:
  - Left (x=0): Fixed (u_x = u_y = 0)
  - Right (x=L): u_x = (lambda - 1)*L, u_y = 0
  - Top/Bottom: u_y = 0 to enforce homogeneous deformation.
- **Analytical Displacement Field**:
  - u_x(x) = (lambda - 1) * x
  - u_y(x) = 0

### Code Flow
1. **Import modules** from the FEA framework.
2. **Generate mesh** with `generate_rect_mesh`.
3. **Define material model** for hyperelasticity.
4. **Set boundary conditions**.
5. **Call `hyperelastic_solver(...)`** to compute displacements.
6. **Use `visualize.plot_deformed_mesh(...)`** to visualize the results.

---

## 📊 Key Features
- Fully modular architecture.
- Supports nonlinear hyperelastic material models.
- Structured and unstructured mesh capability.
- Sparse matrix assembly and efficient solving.
- Easy extension for new element types and materials.

---




