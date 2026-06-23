# Understanding Python Wheels (`.whl`)

A **Wheel** is the standard built-package format used for Python distributions. Defined in **PEP 427**, it is essentially a ZIP archive with a `.whl` extension that contains all the files needed to install your software.

---

## 💡 Why Use Wheels?

Before Wheels, Python used **Source Distributions (SDist)**. When you installed an SDist, your computer had to build the package from scratch. 

| Feature | Source Distribution (`.tar.gz`) | Wheel Distribution (`.whl`) |
| :--- | :--- | :--- |
| **What it is** | Raw code + setup scripts. | Ready-to-install, pre-compiled package. |
| **Installation Speed** | **Slow** (requires compilation/building). | **Fast** (just copies files). |
| **Dependencies** | Requires local build tools (C compiler, etc.). | No build tools required on the target machine. |
| **User Experience** | Can fail if system libraries are missing. | Highly reliable and predictable. |

---

## 🔍 Anatomies of a Wheel File Name

Wheel filenames follow a strict layout containing specific tags. This tells `pip` exactly which operating system and Python version the wheel is compatible with.

### Format:
`{distribution}-{version}-{python_tag}-{abi_tag}-{platform_tag}.whl`

### Example 1: Pure Python Wheel
```text
markdown-3.4.1-py3-none-any.whl
```
* **`markdown`**: Package name
* **`3.4.1`**: Package version
* **`py3`**: Works on any Python 3 interpreter
* **`none`**: No specific Application Binary Interface (ABI) required
* **`any`**: Works on any OS (Windows, Mac, Linux) because it is pure Python code

### Example 2: Platform-Specific Wheel (C-Extension)
```text
numpy-1.26.0-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
```
* **`numpy`**: Package name
* **`1.26.0`**: Package version
* **`cp311`**: Requires CPython 3.11
* **`cp311`**: Matches the CPython 3.11 ABI
* **`manylinux...`**: Works only on 64-bit Linux environments meeting specific system library requirements

---

## 🛠️ Step-by-Step Example: Building a Wheel

Here is how to structure a basic Python project and build it into a Wheel file.

### 1. Project Directory Structure
```text
my_package/
├── pyproject.toml
├── README.md
└── src/
    └── my_package/
        ├── __init__.py
        └── core.py
```

### 2. Configuration (`pyproject.toml`)
This file tells build tools how to package your code.

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "my_package"
version = "0.1.0"
description = "An example package to demonstrate wheels"
readme = "README.md"
requires-python = ">=3.8"
```

### 3. Build the Wheel
Install the official PyPA `build` tool and run it in your terminal:

```bash
# Install the build frontend
pip install build

# Build the project
python -m build
```

### 4. Output
The tool generates a `dist/` directory containing two files:
```text
dist/
├── my_package-0.1.0-py3-none-any.whl   <-- The Wheel file
└── my_package-0.1.0.tar.gz             <-- The Source Distribution (Fallback)
```

Now, anyone can install your packaged library instantly using:
```bash
pip install dist/my_package-0.1.0-py3-none-any.whl
```
