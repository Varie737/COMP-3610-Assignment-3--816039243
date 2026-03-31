# COMP3610 Assignment 3: LLM Applications and Distributed Computing

This repository contains my submission for **COMP 3610 Assignment 3**.

## Project Overview

The assignment is based on two main sources of information:

- **Structured data:** NYC Yellow Taxi Trip Records for January 2024
- **Document corpus:** Transportation-policy and taxi-related PDF documents curated for the RAG system

The notebook builds on the previous assignment work with the same taxi dataset and extends it using Spark, document retrieval, and LLM-based query handling.

## Main Features

### Part 1: Distributed Data Processing with Spark
- Created a SparkSession with custom configuration
- Loaded the January 2024 NYC Yellow Taxi Parquet data into Spark
- Cleaned invalid records and engineered new features such as:
  - `trip_duration_minutes`
  - `trip_speed_mph`
  - `pickup_hour`
  - `pickup_day_of_week`
  - `tip_percentage`
- Performed Spark SQL analysis to answer business questions
- Demonstrated Spark performance optimization using:
  - caching
  - partitioned Parquet output
  - partition pruning
  - execution-plan inspection with `explain()`

### Part 2: RAG Pipeline over Transportation Documents
- Collected and stored transportation-policy PDFs in the `docs/` folder
- Extracted text from PDFs using `PyPDF`
- Split documents into chunks with `RecursiveCharacterTextSplitter`
- Generated embeddings with `sentence-transformers/all-MiniLM-L6-v2`
- Stored embeddings in persistent ChromaDB collections with metadata
- Built a complete RAG pipeline:
  - query
  - retrieve relevant chunks
  - augment prompt
  - generate grounded answer with citations
- Evaluated retrieval and answer quality on a 10-question test set

### Part 3: Integrated Analytics Application
- Built an LLM-powered query router for:
  - `DATA`
  - `DOCUMENT`
  - `HYBRID`
- Built a data-query handler that translates natural language into Spark SQL
- Combined Spark analytics and document retrieval into an end-to-end question-answering system

## Repository Structure
├── assignment3.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── docs/
    ├── strategic_plan_2025.pdf
    ├── tlc_annual_report_2024.pdf
    ├── NYC_tlc_rules.pdf
    ├── Taxi_Regulation_in_the_Age_of_Uber.pdf
    ├── electrification_in_motion_report_2024.pdf
    ├── tlc_congestion_study_report.pdf
    ├── Assessing_the_NYC_Congestion_Pricing_Policy.pdf
    ├── Analysis_and_prediction_of_New_York_City_taxi_and_Uber_demands.pdf
    └── Taxi_Commission_policy_brief_2.9.23.pdf

## Instructions
1. Install the requirements, i.e use pip install -r requirements.txt
2. Insert the API KEY (in the notebook you should see this)
   `LLM_API_KEY = os.getenv("SYNAPSE_API_KEY", "<INSERT KEY HERE>")`
3. Ensure Java version is 8, 11 or 17. If not set it to one of these versions (this code was run in google colab so the java version was already compatible but eg code was commented on how to do this)
4. Run the code.

## Notes
- If local testing is done on Windows, Hadoop Windows utilities (winutils.exe) may be required, but it was not used in this notebook since colab was used. . The assignment code itself remains standard Spark code.
- The NYC taxi dataset is downloaded programmatically inside the notebook.
- The original PDF documents used for the RAG pipeline are stored in the docs/ directory.
- ChromaDB is used as the persistent vector store for embeddings.

## Results Summary
- The Spark analytics section successfully answered descriptive and aggregate questions about taxi demand, fares, trip speeds, and revenue.
- The RAG evaluation achieved a 50% combined retrieval-and-answer accuracy on the final 10-question test set.
- The query router achieved 100% accuracy on the 15-question routing test set.
- The integrated application successfully handled DATA, DOCUMENT, and HYBRID queries end-to-end.

## AI ASSISTANCE DISCLOSURE
AI (Chat GPT) was used in the process of creating this assignment for help understanding th project requirements, debugging, understanding the results and with the structure of code. All AI generated code was understood before submission.
