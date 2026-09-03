# Automated Evaluation of AI Legal Rights with Zero-Shot Classification & Rule Logic

An AI-powered legal assistance platform designed to help citizens understand legal rights through plain-language queries. The system combines **Zero-Shot Classification**, **semantic search**, **LLM-based response generation**, and a **Rule-Based Legal Engine** to produce structured, explainable, and actionable legal information.

## Overview

Legal information can be difficult for non-experts to understand because of complex terminology and uncertainty about which law applies to a particular situation. This project addresses that problem through an AI-assisted legal information platform where users can describe their situation in normal, everyday language.

The system interprets the query, identifies the relevant legal domain, retrieves supporting legal context, applies predefined legal rules, and generates a simplified response. The design combines the flexibility of AI models with the predictability of rule-based reasoning.

Example queries include:
- “My employer has not paid my salary.”
- “My landlord increased my rent without notice.”
- “I was scammed through an online payment.”
- “I received a defective product and the seller refused a refund.”

> **Disclaimer:** This project provides legal information and decision support for educational/research purposes. It is not a substitute for professional legal advice.

## Key Features

### Natural-Language Legal Queries
Users can describe their problems in plain language without knowing legal terminology or manually selecting a legal category.

### Zero-Shot Legal Domain Classification
A Legal-BERT-based zero-shot classification approach identifies the relevant legal domain without requiring task-specific labelled training examples for every category.

### Semantic Legal Search
The system retrieves contextually relevant legal information using semantic similarity rather than relying only on exact keyword matching.

### Rule-Based Legal Reasoning
Legal conditions are represented using an **If–Then** format, connecting user situations with applicable laws, sections, and actions.

### Confidence-Based Inference
The system evaluates AI confidence and rule-based evidence before selecting or assembling the final result.

### Explainable Legal Output
Results are presented in structured sections covering the legal summary, applicable laws, penalties, deadlines, required documents, authorities, and recommended actions.

### Voice Input
The interface supports speech-based query entry through browser speech capabilities where supported.

### Multilingual Interface
The project interface supports Hindi and Tamil along with English.

### Court and Legal Aid Locator
A location-based interface helps users find nearby courts and legal-aid resources.

### Legal Expense and Free Legal Aid Information
The platform includes supporting information about legal expenses and free legal-service eligibility.

### Downloadable Analysis
Users can save the generated legal analysis for later reference.

## System Architecture

```text
User
  |
  v
Frontend
  |
  v
API Gateway
  |
  v
Backend Server
  |-------------------|-------------------|
  v                   v                   v
Normal Logic       AI/NLP Engine       Redis Cache
  |                   |
  v                   v
User Database      NLP Pipeline
(MySQL/Postgres)       |
               +-------+-------+-----------+
               |       |       |           |
          Preprocessing  Intent  Semantic  LLM
                        Class.   Search   Generation
                                  |
                                  v
                           Legal Knowledge
                              / Retrieval
                                  |
                                  v
                         Rule-Based Validation
                                  |
                                  v
                           Inference / Decision
                                  |
                                  v
                           Final Legal Output
```

## Main AI Pipeline

### 1. Preprocessing
The raw query is cleaned and normalized using operations such as tokenization, normalization, punctuation handling, and stop-word processing. A spaCy-based NLP pipeline is used for input preparation.

### 2. Intent Classification
The cleaned query is passed to the zero-shot classification stage. A Legal-BERT-based transformer/NLI approach compares the query with candidate legal-domain descriptions and returns the most relevant domain with a confidence score.

### 3. Semantic Search
The query is represented as a semantic embedding and matched against the legal knowledge base to retrieve relevant statutory context even when the wording differs from source documents.

### 4. Response Generation
The classified intent and retrieved context are supplied to an LLM to produce a readable legal explanation. The response can contain rights, applicable laws, penalties, deadlines, required documents, authorities, and recommended next steps.

### 5. Rule-Based Validation
The generated result is checked against predefined legal rules represented through deterministic If–Then conditions. This adds a structured validation layer and improves explainability.

### 6. Inference and Final Decision
The inference layer compares AI-side results with rule-based evidence and uses confidence and consistency information to select or assemble the final response. Low-confidence situations can trigger clarification rather than overconfident guidance.

## Technologies Used

| Component | Technology / Approach | Purpose |
|---|---|---|
| Frontend | HTML, CSS, JavaScript | User interaction and result presentation |
| Backend | Python, Flask / REST APIs | Request processing and orchestration |
| NLP Preprocessing | spaCy / NLTK | Text cleaning and normalization |
| Classification | Legal-BERT / Zero-Shot NLI | Legal domain classification |
| Embeddings | Sentence-BERT / Sentence Transformers | Semantic representation |
| Retrieval | FAISS / vector similarity search | Relevant legal-context retrieval |
| Response Generation | GPT-4 / Llama 3 | Natural-language response generation |
| Rule Engine | Python If–Then logic | Legal validation and statutory mapping |
| Cache | Redis | Faster access to frequently used information |
| Database | MySQL / PostgreSQL | User and application data |
| Map Services | OpenStreetMap + Leaflet.js | Court and legal-aid location features |

## Supported Legal Domains

The prototype covers:
- Housing and Tenancy
- Employment and Salary
- Consumer Protection
- Cyber Fraud and Online Fraud
- Family and Matrimonial Issues
- Constitutional and Civil Rights

The modular design allows additional domains to be added through new intent labels, legal rules, and knowledge-base content.

## Installation and Setup

### 1. Clone the Repository

Replace the URL and folder name with the final GitHub repository details:

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
cd <YOUR-REPOSITORY-FOLDER>
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the Application

Configure model settings, API credentials, database settings, and other environment variables required by the final implementation.

Example:

```text
MODEL_NAME=...
LLM_API_KEY=...
DATABASE_URL=...
REDIS_URL=...
```

Do not commit API keys or other secrets to GitHub.

### 5. Run the Application

For a Flask-based implementation:

```bash
python app.py
```

Use the production server command defined by the project when deploying.

## Usage

1. Open the web application.
2. Enter a legal situation in everyday language or use voice input where supported.
3. Submit the query.
4. The system preprocesses the text and identifies the most relevant legal domain.
5. Relevant legal context is retrieved and checked against the rule base.
6. The inference layer prepares the final response.
7. Review the legal summary, applicable provisions, deadlines, action plan, and supporting information.
8. Use the court/legal-aid features or download the analysis when required.

## Project Structure

```text
Automated-Legal-Rights-Evaluation/
|
├── app.py / server.py
├── frontend/
├── models/
├── rules/
├── knowledge_base/
├── preprocessing/
├── retrieval/
├── inference/
├── database/
├── static/
├── templates/
├── tests/
├── requirements.txt
├── README.md
└── .env.example
```

Adjust the structure to match the final repository.

## Evaluation and Results

| Metric | Result |
|---|---:|
| Combined Model Accuracy | **95%** |
| Zero-Shot Classification Accuracy | **94%** |
| Rule-Based Engine Accuracy | **96%** |
| Average End-to-End Response Time | **2.35 s** |
| Unit Tests Passed | **86 / 86** |
| Overall Test Pass Rate | **99.4%** |
| Legal Rules Encoded | **52** |
| Legal Knowledge-Base Entries | **62** |

The hybrid approach combines the flexibility of zero-shot classification with the consistency of structured legal rules. In validation, it achieved 95% combined accuracy while keeping average end-to-end latency at approximately 2.35 seconds.

## Limitations

The current prototype is limited to the legal domains and rules encoded in the knowledge base. Legal content also requires regular review because legislation and judicial interpretations can change.

The platform is intended for legal information and decision support rather than professional legal advice. Complex, highly fact-specific disputes still require consultation with a qualified legal professional.

Although the interface supports multiple languages, the underlying legal NLP coverage should not be assumed to be fully multilingual unless the corresponding models and legal content have been implemented and validated.

## Future Enhancements

- Expansion to additional Indian legal domains
- Broader regional-language legal analysis
- Automated monitoring of legislative changes
- Model optimisation and improved caching
- Multi-turn conversational legal assistance
- Cross-browser voice support
- Integration with official legal-aid and government portals
- Advanced legal analytics and research capabilities

## Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Implement and test your changes.
4. Update documentation where necessary.
5. Submit a pull request with a clear description.

## Authors and Acknowledgements

**Avjot Singh Chawla**  
B.Tech, Computer Science and Engineering  
SRM Institute of Science and Technology

**Tanushree Sunil Borase**  
B.Tech, Computer Science and Engineering  
SRM Institute of Science and Technology

**Project Guide:**  
Dr. Thamizhamuthu R  
Assistant Professor, Department of Computing Technologies  
SRM Institute of Science and Technology

---

**Project Highlights:** AI + Rule-Based Legal Reasoning · Zero-Shot Classification · Semantic Search · Explainable Outputs · 95% Combined Accuracy
