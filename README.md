[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/vgbm4cZ0)
ADGM-Compliant Corporate Agent (Offline Rule-Based Version)
Overview
This project is an AI-powered Corporate Agent designed to assist in ADGM-compliant business incorporation and document review — without requiring an API key or internet-based LLM.

It automatically:
1. Reads the official ADGM Data Sources PDF to extract required documents.
2. Accepts .docx legal documents from the user.
3. Classifies documents against the ADGM checklist.
4. Flags compliance issues using a rule-based engine.
5. Inserts inline review notes in the .docx files.
6. Generates a JSON report summarizing findings.
7. Provides a zipped package with reviewed documents and the report.

Features
1. PDF-based checklist extraction → no manual hardcoding of document names.
2. Rule-based compliance checks:
3. Jurisdiction clause validation (ADGM Courts vs UAE Federal Courts).
4. Signature section detection.
5. Ownership percentage validation.
6. Offline processing → no OpenAI API key required.
7. JSON output + annotated .docx review files.
8. Google Colab ready → run from anywhere, no local setup needed.

Folder Structure
.
├── Data Sources.pdf               # Official ADGM reference PDF (uploaded in Colab)
├── sample_docs/                   # Auto-generated test documents
├── reviewed_package.zip           # Output package (reviewed docs + report)
├── report.json                    # JSON compliance report
├── main_notebook.ipynb            # Colab notebook with full pipeline
└── README.md                      # Project documentation

How It Works

1. Checklist Extraction – Reads Data Sources.pdf and extracts document names like:
      Articles of Association
      Memorandum of Association
      Board Resolution
      UBO Declaration Form
      Register of Members and Directors

2. Document Upload & Classification – User uploads .docx files, which are matched against the checklist using fuzzy matching.

3. Rule-Based Compliance Check – Detects:
      Incorrect jurisdiction references.
      Missing signature lines.
      Invalid ownership percentages.

4. Review Notes Insertion – Adds REVIEW NOTE paragraphs into .docx with compliance suggestions.

5. Report & Package Output – Produces:
      report.json summarizing the review.
      reviewed_package.zip containing reviewed .docx files + the JSON report.

How to Run (Google Colab):
Step 1 – Open Colab
    Go to Google Colab

Step 2 – Upload the Notebook
    Upload the main_notebook.ipynb file from this repository into Colab.

Step 3 – Install Dependencies
    Run the first cell in the notebook:
      !pip install python-docx gradio pypdf2 scikit-learn rapidfuzz

Step 4 – Create Sample Docs
    Run the cell that generates sample_docs/ (5 .docx test files with intentional mistakes).
    This step also creates sample_adgm_docs.zip for download if you want the test docs locally.

Step 5 – Upload ADGM Data Sources PDF
    Run the upload cell.
    Choose your Data Sources.pdf file (provided in this repo or from ADGM).

Step 6 – Extract Checklist
    The notebook will read the PDF and print the list of required document types.

Step 7 – Run the Processing
    Either:
      Test with the generated sample docs (sample_docs/), OR
      Upload your own .docx files via the Gradio UI cell.

Step 8 – Get Results
    The script outputs:
        report.json – Compliance review summary.
        reviewed_package.zip – Reviewed .docx files with notes + report.

Testing

You can test using:
    The auto-generated sample docs (contains deliberate compliance mistakes).
    Your own .docx files.

When testing with sample docs, expect the JSON report to flag:
    Wrong jurisdiction clauses.
    Missing signatures.
    Ownership over 100%.

