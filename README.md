# 📊 Financial Document Analysis with LLM + VLM

This project automates the extraction, structuring, validation, and analysis of **financial documents** such as income statements and invoices. It combines OCR tools, PDF parsing libraries, and local LLMs (e.g., Mistral via Ollama) to deliver an end-to-end intelligent pipeline for financial document understanding.

---

## 🚀 Key Features

* 🔍 **Page filtering**: Identify income statement pages from multi-page earnings PDFs
* 📄 **Docling markdown conversion**: Extract structured tables from filtered PDFs
* 📊 **Data parsing**: Convert markdown tables into JSON and Pandas DataFrames
* 🧠 **Local LLM analysis**: Analyze trends, margins, and anomalies using Mistral via Ollama
* 🧾 **Invoice validation**: Use OCR and table parsers to process invoice line items and metadata
* 📦 **Backend comparison**: Evaluate different PDF/Markdown/OCR extraction tools
* 🖼️ **Poppler-based image conversion**: Enable VLM input from filtered PDF pages
* 🧹 **Automatic cleanup**: Temporary files deleted after each run

---

## 📁 Project Structure

```
📦 Financial_Document_Analysis/
├── data/                                   # PDF samples (invoices, earnings)
├── temp/                                   # Auto-cleaned temp files
├── code/
│   └── financial_statement_validation.ipynb
├── 3packages_backend_understanding.ipynb   # OCR and backend parser evaluation
├── requirements.txt                        # Python dependencies
└── README.md                               # Project documentation
```

---

## 🧪 Notebooks Summary

| Notebook                                | Description                                                                                             |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `financial_statement_validation.ipynb`  | Parses and analyzes income statement tables using PyMuPDF, Docling, Pandas, and Mistral                 |
| `3packages_backend_understanding.ipynb` | Tests and compares tools like `pdfplumber`, `PyMuPDF`, and `docling` on sample finance and scanned PDFs |

---

## 🧰 Technology Stack

| Tool/Library | Purpose                                                |
| ------------ | ------------------------------------------------------ |
| `pandas`     | DataFrame manipulation                                 |
| `PyMuPDF`    | PDF text and page scanning                             |
| `PyPDF2`     | Extracting relevant pages from PDFs                    |
| `pdfplumber` | OCR-friendly table parsing (for invoices)              |
| `docling`    | Markdown extraction from financial tables              |
| `ollama`     | Local LLM inference with models like Mistral and Llava |
| `matplotlib` | (Optional) Data visualization                          |
| `requests`   | HTTP utility for backend logic (optional)              |
| `pdf2image`  | PDF to image conversion for VLMs                       |

---

## 🔧 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/DRgit03/Financial_Document_Analysis.git
cd Financial_Document_Analysis
```

### 2. Create a virtual environment

```bash
python -m venv venv
venv\Scripts\activate     # Windows
# OR
source venv/bin/activate    # macOS/Linux
# OR
conda create -n financial-env python=3.10 -y
conda activate financial-env
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🧠 Running the Project

### ▶️ Income Statement Analysis

```bash
jupyter notebook code/financial_statement_validation.ipynb
```

### ▶️ Backend/OCR Evaluation

```bash
jupyter notebook 3packages_backend_understanding.ipynb
```

> 💡 You’ll need `docling` installed and `ollama` running with the `mistral` and `llava` models.

---

## 🔌 LLM Setup (Ollama) and VLM (Llava)

Install and run Mistral and Llava locally:

```bash
ollama pull mistral
ollama run mistral
ollama pull llava
```

The notebook sends cleaned financial data to the LLM using the `ollama` Python client to generate insights.

---

## 📄 Poppler: Background & Installation Guide

### 🔍 What is Poppler?

Poppler is a PDF rendering library used to convert PDF pages into images. Tools like `pdf2image` require Poppler to enable conversion for vision-language model input.

---

### 💻 Installation

#### 🪟 Windows

1. Download Poppler:

   * [https://github.com/oschwartz10612/poppler-windows/releases](https://github.com/oschwartz10612/poppler-windows/releases)
2. Extract the ZIP to:

   ```
   C:\Users\<YourUsername>\poppler-24.08.0
   ```
3. Your Python script should include:

   ```python
   poppler_path = os.path.join(os.path.expanduser("~"), "poppler-24.08.0", "Library", "bin")
   ```
4. No need to modify system PATH if you set `poppler_path` explicitly in the script.

#### 🍎 macOS

Install via Homebrew:

```bash
brew install poppler
```

#### 🐧 Linux (Ubuntu/Debian)

Install with:

```bash
sudo apt update
sudo apt install poppler-utils
```

---

## 🧪 Verifying Poppler Installation

Command line check:

```bash
pdftoppm -v
```

Python test:

```python
images = convert_from_path("sample.pdf", dpi=200, poppler_path="your/path")
```

---

## 📦 requirements.txt

```txt
pandas==2.2.2
PyMuPDF==1.23.10
PyPDF2==3.0.1
matplotlib==3.8.4
pdfplumber==0.10.3
docling==0.2.3
ollama==0.1.6
requests==2.31.0
pdf2image==1.17.0
```

---

## ✅ Sample Output

**Cleaned Income Table:**

```
Metric                             Q1 2025  Q1 2024  % Change
Net Operating Revenues            11129    11300     (2)
Operating Income                  3659     2141      71
Net Income                        3330     3177      5
```

**LLM Analysis:**

* Revenue slightly declined by 2%, but operating income rose sharply.
* Cost management improved significantly (Operating margin ↑).
* Overall profitability is up; red flags include declining other income.
* Recommend leadership to monitor revenue pressure while continuing cost controls.

---

## 🙋 Support

If Poppler doesn't work, double-check the path and installation. You can also manually run:

```bash
pdftoppm sample.pdf output -png
```

