**Autonomous Insurance Claims Processing Agent**
_Overview_

This project implements a lightweight autonomous agent that processes First Notice of Loss (FNOL) documents for insurance claims.

_The agent_:

Extracts key claim fields from FNOL PDFs

Detects missing mandatory information

Applies predefined business routing rules

Produces an explainable routing decision in structured JSON format

The solution is implemented in Python and designed to run easily in Google Colab or a local environment.

**Problem Statement**

Insurance FNOL documents are typically unstructured (PDF/TXT) and require manual review to:

Extract claim details

Validate completeness

Decide how the claim should be processed

The goal of this project is to automate the initial intake stage of claims processing using deterministic, explainable logic.

**Features**

📄 PDF text extraction using pdfplumber

🧾 Structured field extraction via regex patterns

⚠️ Mandatory field validation

🧠 Rule-based claim routing

📝 Human-readable reasoning for each decision

📦 JSON output compatible with downstream systems

_Input_

FNOL documents in PDF or TXT format

Example: ACORD Automobile Loss Notice

_Extracted Fields_
Policy Information

Policy Number

Policyholder Name

Incident Information

Date of Loss

Location

Description of Accident

Claim Details

Claim Type

Estimated Damage

Mandatory Fields

Policy Number

Policyholder Name

Date of Loss

Description

Claim Type

Estimated Damage

_Routing Rules_
Condition	Route
Any mandatory field missing	Manual Review
Description contains “fraud”, “staged”, “inconsistent”	Investigation Flag
Claim type = injury	Specialist Queue
Estimated damage < $25,000	Fast-track
Otherwise	Standard Processing
**Output Format**

The agent produces the following JSON structure:

{
  "extractedFields": {},
  "missingFields": [],
  "recommendedRoute": "",
  "reasoning": ""
}

Project Structure
├── main.ipynb              # Google Colab notebook
├── README.md               # Project documentation


(Colab version keeps everything in a single notebook for simplicity.)

How to Run (Google Colab)

Open Google Colab

Upload the notebook

Run the following steps in order:

Install dependencies

Upload FNOL PDF

Execute extraction, validation, and routing cells

View final JSON output

Dependencies
pip install pdfplumber


Python version: 3.8+

Design Decisions

Rule-based routing was chosen for transparency and explainability

Regex-based extraction provides deterministic behavior suitable for structured forms like ACORD

Modular functions allow easy extension with:

NLP libraries (spaCy)

LLM-based extraction

API deployment (FastAPI)

Limitations

Regex patterns may require tuning for different FNOL templates

Handwritten or scanned PDFs are not supported (OCR not included)

No ML model training (intentionally out of scope)

Possible Enhancements

LLM-powered field extraction for unstructured text

OCR support using Tesseract

REST API using FastAPI

Confidence scoring for extracted fields

Unit tests and CI pipeline

Conclusion

This project demonstrates how insurance FNOL intake can be automated using:

Clean Python code

Deterministic business rules

Explainable decision-making

It mirrors real-world claims triage workflows while remaining lightweight, transparent, and extensible.

Author

Kavya Junuthula
