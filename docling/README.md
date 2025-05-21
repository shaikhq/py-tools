
---

# 🛠️ Python 3.13 + uv + docling Setup on macOS (Apple M2)

This guide walks you through setting up a modern Python development environment on macOS (Apple Silicon), including:

* Installing Python 3.13.x
* Creating a clean project environment using [`uv`](https://github.com/astral-sh/uv)
* Fixing common SSL issues with custom Python builds
* Installing and running [`docling`](https://github.com/docling/docling) to convert PDFs to Markdown

---

## 🐍 Step 1: Install Python 3.13.x

Download and install the latest stable **Python 3.13.x** for macOS:

1. Visit: [https://www.python.org/downloads/macos/](https://www.python.org/downloads/macos/)
2. Under the Python 3.13.x section, download:

   * **macOS 64-bit universal2 installer** (`python-3.13.x-macos11.pkg`)
3. Run the `.pkg` installer and follow the GUI instructions.
4. Confirm installation:

   ```bash
   python3.13 --version
   ```

---

## ⚙️ Step 2: Install `uv` – Fast Python Package Manager

[`uv`](https://github.com/astral-sh/uv) is a high-performance, Rust-based tool for managing Python packages and environments.

1. Install `uv`:

   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```
2. Add `uv` to your shell’s `PATH` (if not already):

   ```bash
   export PATH="$HOME/.local/bin:$PATH"
   ```
3. Verify installation:

   ```bash
   which uv
   uv --version
   ```

---

## 🧪 Step 3: Create and Activate Virtual Environment

1. Create a virtual environment using Python 3.13:

   ```bash
   uv venv --python=/usr/local/bin/python3.13 myenv
   ```
2. Activate it:

   ```bash
   source myenv/bin/activate
   ```

---

## 🔐 Step 4: Fix SSL Certificate Issues

Custom Python installations may not use macOS’s trusted certificates. Fix this as follows:

### Option A: Run the bundled macOS certificate installer

```bash
/Applications/Python\ 3.13/Install\ Certificates.command
```

### Option B: Use `certifi` to set up a trusted CA bundle manually

1. Install `certifi`:

   ```bash
   uv pip install --upgrade certifi
   ```
2. Set SSL cert environment variable:

   ```bash
   export SSL_CERT_FILE=$(python3.13 -m certifi)
   ```

---

## 📦 Step 5: Install docling and Dependencies

With your virtual environment activated:

```bash
uv pip install docling
uv pip install ipykernel --upgrade --force-reinstall
```

Download required OCR models for `docling`:

```bash
docling-tools models download
```

---

## 📄 Step 6: Run the PDF to Markdown Notebook

To convert PDF files using `docling`, run the included notebook:

1. Open the notebook:

   ```bash
   jupyter notebook docling/pdf-2-md.ipynb
   ```

2. Follow the notebook instructions to convert your PDF to Markdown.

> ✅ Tip: Ensure your virtual environment is selected as the active kernel in Jupyter.

