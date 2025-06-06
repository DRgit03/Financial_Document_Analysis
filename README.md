# 📊 Financial Document Analysis

This project automates the extraction, structuring, validation, and analysis of **financial documents** such as income statements and invoices. It combines OCR tools, PDF parsing libraries, and local LLMs (e.g., Mistral via Ollama) to deliver an end-to-end intelligent pipeline for financial document understanding.

---

## 🚀 Key Features

- 🔍 **Page filtering**: Identify income statement pages from multi-page earnings PDFs
- 📄 **Docling markdown conversion**: Extract structured tables from filtered PDFs
- 📊 **Data parsing**: Convert markdown tables into JSON and Pandas DataFrames
- 🧠 **Local LLM analysis**: Analyze trends, margins, and anomalies using Mistral via Ollama
- 🧾 **Invoice validation**: Use OCR and table parsers to process invoice line items and metadata
- 📦 **Backend comparison**: Evaluate different PDF/Markdown/OCR extraction tools

---

## 📁 Project Structure

```
📦 Financial_Document_Analysis/
├── data/                                   # PDF samples (invoices, earnings)
├── 3packages_backend_understanding.ipynb   # OCR and backend parser evaluation
├── financial_statement_validation.ipynb    # End-to-end income statement analyzer
├── requirements.txt                        # Python dependencies
└── README.md                               # Project documentation
```

---

## 🧪 Notebooks Summary

| Notebook | Description |
|----------|-------------|
| `financial_statement_validation.ipynb` | Parses and analyzes income statement tables using PyMuPDF, Docling, Pandas, and Mistral ,LLava models|
| `3packages_backend_understanding.ipynb` | Tests and compares tools like `pdfplumber`, `PyMuPDF`, and `docling` on sample finance and scanned PDFs |

---

## 🧰 Technology Stack

| Tool/Library | Purpose |
|--------------|---------|
| `pandas`     | DataFrame manipulation |
| `PyMuPDF`    | PDF text and page scanning |
| `PyPDF2`     | Extracting relevant pages from PDFs |
| `pdfplumber` | OCR-friendly table parsing (for invoices) |
| `docling`    | Markdown extraction from financial tables |
| `ollama`     | Local LLM inference with models like Mistral |
| `matplotlib` | (Optional) Data visualization |
| `requests`   | HTTP utility for backend logic (optional) |

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
#OR
conda create -n financial-env python=3.10 -y #Anaconda prompt
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
jupyter notebook financial_statement_validation.ipynb
```

### ▶️ Backend/OCR Evaluation

```bash
jupyter notebook 3packages_backend_understanding.ipynb
```

> 💡 You’ll need `docling` installed and `ollama` running with the `mistral` model.

---

## 🔌 LLM Setup (Ollama) and VLM (LLava)

Install and run Mistral locally:

```bash
the below packages all comes with ollama which you can install it from requirements.txt file make sure the ollama installed and later that only run this below commands
ollama pull mistral
ollama run mistral (optional it is just test model response to your prompts)
ollama pull llava
```

> The notebook sends cleaned financial data to the LLM using the `ollama` Python client to get natural language insights.

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
- Revenue slightly declined by 2%, but operating income rose sharply.
- Cost management improved significantly (Operating margin ↑).
- Overall profitability is up; red flags include declining other income.
- Recommend leadership to monitor revenue pressure while continuing cost controls.



**title: Income Statement Automation Pipeline**

# Income Statement Automation Pipeline

### End-to-End Overview using LLMs & VLMs

---

## Objective

**Automate** the extraction and analysis of income statement and invoice data from corporate earnings PDFs.

**Technologies Used:**

* LLMs (Language Models)
* VLMs (Vision-Language Models)
* Python Libraries (PyMuPDF, pdf2image, Docling, etc.)

---

## Step 1: Identify Relevant Pages

### 🎯 Goal: Locate Income Statement Pages

* Search for keywords:

  * "income statement"
  * "net income"
  * "gross profit"
* Include pages with ≥2 keyword matches.

**✅ Outcome:** Focuses parsing on financially relevant sections.

---

## Step 2: Filter the PDF

### 🧼 Goal: Create a trimmed-down version

* Use `PdfWriter` to extract only matched pages.
* Store result in a `temp/` folder.

**✅ Outcome:**

* Faster processing
* Reduced document size

---

## Step 3: Parse PDF to Markdown

### 📝 Goal: Use Docling for structured output

* Input: Filtered PDF
* Output: Markdown with headings, paragraphs, and tables

**✅ Outcome:** Enables precise and lightweight parsing of tables.

---

## Step 4: Extract Markdown Tables

### 📊 Goal: Identify tabular financial data

* Use pipe (`|`) and dash (`---`) markers to locate tables.
* Validate tables have ≥3 rows.

**✅ Outcome:** Only meaningful financial tables are captured.

---

## Step 5: Convert Table to JSON

### 🔄 Goal: Structure tabular data

* Skip header lines
* Parse remaining rows into a list of dictionaries

**Example:**

```json
{
  "Metric": "Net Income",
  "Q1 2025": "2300",
  "Q1 2024": "2200",
  "% Change": "4.5"
}
```

**✅ Outcome:** Ready for analysis or dashboarding.

---

## Step 6: Convert to Image (for VLM)

### 🖼️ Goal: Visual Input for VLMs

* Convert filtered PDF to PNG using `pdf2image` and Poppler.

**✅ Outcome:** Image input supports hybrid text + visual reasoning.

---

## Step 7: LLM + VLM Analysis

### 🤖 Goal: Generate insights automatically

* Input:

  * Cleaned DataFrame (from JSON)
  * Optional: PDF image (for VLMs like `llava`)
* Prompt guides the model to analyze:

  * Revenue/profit trends
  * Operational efficiency
  * Investment or leadership suggestions

**✅ Outcome:** Human-readable insights at scale.

---

## Step 8: Clean Up

### 🧹 Goal: Remove temp files

* Use `shutil.rmtree()` to delete intermediate outputs

**✅ Outcome:** Secure, lightweight, and production-ready pipeline.

---

## Summary: End-to-End Flow

| Step                | Tool/Technique      | Purpose                               |
| ------------------- | ------------------- | ------------------------------------- |
| Page Detection      | Keyword Matching    | Focus on income-related content       |
| PDF Filtering       | PyPDF2 / PdfWriter  | Reduce noise                          |
| Markdown Conversion | Docling             | Extract structured text               |
| Table Extraction    | Markdown Heuristics | Isolate financial tables              |
| JSON Conversion     | Custom Parser       | Structure for analysis                |
| Image Conversion    | pdf2image + Poppler | Enable VLM visual input               |
| Financial Insights  | LLM / VLM           | Automated reasoning & recommendations |
| Cleanup             | shutil              | Keep workspace tidy                   |

---

## Use Cases

### Who benefits from this pipeline?

* 💼 Financial Analysts
* 📈 Investors
* 🧪 LLM/VLM Researchers
* 🧠 AI-Powered Sales Teams





