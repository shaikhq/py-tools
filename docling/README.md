# 🛠️ Python 3.12 Project Setup with `uv` and `docling` on RHEL 8.10

This README documents the setup process to:

* Install **Python 3.12.8** via RHEL package manager
* Set up a clean, modern Python environment using [`uv`](https://github.com/astral-sh/uv) — a fast Rust-based tool for managing packages and virtual environments
* Install and use [`docling`](https://github.com/docling/docling) to convert **PDF files into Markdown**

This guide is intended for RHEL users who want to use a newer Python version with minimal hassle, and leverage `uv` for modern dependency management.

---

## 🐍 Step 1: Install Python 3.12.8 via DNF

If you're using **RHEL 9.4 or later**, Python 3.12 is available directly in the package repositories.

### ✅ Install Python 3.12:

```bash
sudo dnf install python3.12
```

### ✅ Verify installation:

```bash
python3.12 --version
# Output should be: Python 3.12.8
```

---

## ⚙️ Step 2: Install `uv` — A Fast Python Package Manager

[`uv`](https://github.com/astral-sh/uv) is a modern tool that replaces pip, venv, and virtualenv with faster performance and dependency resolution.

### 1. Install `uv` using the official script:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Add it to your shell profile (if not already):

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 3. Confirm `uv` is installed:

```bash
uv --version
```

---

## 🧪 Step 3: Create a Virtual Environment with Python 3.12

```bash
uv venv --python $(which python3.12)
source .venv/bin/activate
```

This creates and activates a virtual environment in `.venv/`.

---

## 📄 Step 4: Install `docling` and Convert a PDF to Markdown

[`docling`](https://github.com/docling/docling) is a document processing tool that extracts structured content from PDFs and outputs Markdown.

### 1. Install `docling`:

```bash
uv pip install docling
```

### 2. Convert a PDF:

```bash
docling path/to/your-document.pdf
```

The first time it runs, `docling` will download OCR models. After setup, it outputs a `.md` file with embedded images and structured content.

---

## ✅ Final Notes

* Python 3.12.8 installed cleanly via `dnf` — no need to compile from source
* `uv` simplifies virtual environments and dependency management
* `docling` enables quick conversion of PDFs to clean Markdown
