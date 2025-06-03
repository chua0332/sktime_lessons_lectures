# Forecasting Course

Welcome to the forecasting course! This  readme will guide you through the installation process for the course dependencies.

## Overview

This repository supports two methods to install dependencies:

1. **Using `requirements.txt`** – a traditional method using pip.
2. **Using Poetry** – a modern dependency manager that also manages virtual environments.

Choose the method that best fits your workflow.

## Prerequisites

- **Python:** Make sure you're running Python 3.11.
- **Virtual Environment (Optional but Recommended):** Creating a virtual environment is a best practice.

### Creating a Virtual Environment

Using Python’s built-in `venv` module, run:

```bash
python3 -m venv .venv
```

Then activate it:

- **On macOS/Linux:**
  ```bash
  source .venv/bin/activate
  ```
- **On Windows:**
  ```bash
  .venv\Scripts\activate
  ```

## Installation Methods

### 1. Installing via `requirements.txt`

To install dependencies using pip and `requirements.txt`, run:

```bash
pip install -r requirements.txt
```

This command reads the `requirements.txt` file and installs all the listed packages into your active environment.

### 2. Installing via Poetry

#### Installing Poetry Version 1.8.4

If you prefer using [Poetry](https://python-poetry.org/), install version **1.8.4** by executing the following commands:

- **On Unix/macOS:**
  ```bash
  curl -sSL https://install.python-poetry.org | python3 - --version 1.8.4
  ```
- **On Windows (PowerShell):**
  ```powershell
  (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python - --version 1.8.4
  ```

#### Installing Project Dependencies with Poetry

1. **Navigate to your project directory:**

   ```bash
   cd path/to/your/project
   ```

2. **Install the dependencies:**

   ```bash
   poetry install
   ```

   This command reads the `pyproject.toml` file and installs the required packages. It will also set up a virtual environment if one is not already activated.

3. **Activating the Poetry Shell (Optional):**

   To enter the virtual environment managed by Poetry, run:

   ```bash
   poetry shell
   ```
   
## Troubleshooting

- **Python Version:** Ensure you have Python 3.11.
- **Virtual Environment:** Confirm that your virtual environment is activated if you are using one.
- **Poetry Issues:** If you encounter problems with Poetry, refer to the [Poetry documentation](https://python-poetry.org/docs/).