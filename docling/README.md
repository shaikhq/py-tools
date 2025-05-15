# 🛠️ Python 3.13 Project Setup with `uv` and `docling` on macOS (Apple M2)

This README documents the full setup process I followed to:

- Install a **recent Python release** (3.13.x) on macOS with an Apple M2 chip
- Set up a **clean, modern Python project environment** using [`uv`](https://github.com/astral-sh/uv) — a fast, Rust-based tool for Python package and venv management
- Fix common **SSL certificate errors** in custom Python builds
- Install and use [`docling`](https://github.com/docling/docling) to convert a **PDF file into Markdown**

This guide is intended for developers who want to work with newer versions of Python and use `uv` for efficient project management, while ensuring HTTPS, OCR, and package installations work smoothly on macOS.

---

## 🐍 Step 1: Install Python 3.13.x on macOS (Apple M2)

To get started, I installed Python **3.13.2**, which is one or two versions behind the latest stable release — this avoids unexpected issues with pre-releases or bleeding-edge versions.

### ✅ Instructions

1. Go to the official Python download page for macOS:  
   👉 [https://www.python.org/downloads/macos/](https://www.python.org/downloads/macos/)

2. Under the version list (e.g., Python 3.13.2), download:
   - **macOS 64-bit universal2 installer** (`python-3.13.2-macos11.pkg`)

3. Once downloaded:
   - Double-click the `.pkg` installer
   - Complete the installation through the GUI installer

4. Verify that Python 3.13 is installed correctly:
   ```bash
   python3.13 --version


## ⚙️ Step 2: Install `uv` — A Fast Python Package Manager

`uv` is a high-performance tool for managing Python environments and dependencies.

### 1. Install `uv` using the official script:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Add it to your PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

### 3. Verify `uv` is available:

```bash
which uv
uv --version
```

---

## 🧪 Step 3: Create a Virtual Environment with Python 3.13

```bash
uv venv --python /usr/local/bin/python3.13
source .venv/bin/activate
```

This creates and activates a `.venv/` using Python 3.13.

---

## 🔐 Step 4: Fix SSL Certificate Issues (Common in Custom Python Installs)

Python 3.13 installed manually may not trust macOS system certificates. To fix this:

### 1. Install `certifi` using `uv`:

```bash
uv pip install --upgrade certifi
```

### 2. Get the path to the certifi CA bundle:

```bash
python3.13 -m certifi
```

### 3. Set the SSL certificate environment variable:

```bash
export SSL_CERT_FILE=$(python3.13 -m certifi)
```

This ensures `urllib`, `requests`, and other tools using HTTPS work correctly.

---

## 📄 Step 5: Install `docling` and Convert a PDF to Markdown

`docling` is a document processing tool that can extract structure and text from PDFs.

### 1. Install `docling`:

```bash
uv pip install docling
```

### 2. Run `docling` on a PDF:

```bash
docling 3636218.3636235.pdf
```

On first use, it will download OCR models via EasyOCR. After setup, it extracts text and outputs Markdown based on document structure.

---

## ✅ Final Notes

* These steps were tested on macOS (Apple M2) with Python 3.13.2
* `uv` helps keep everything fast and isolated
* SSL fixes are required if you don’t use Homebrew or system Python builds

---

Feel free to fork or adapt this workflow for your own Python projects!

```
