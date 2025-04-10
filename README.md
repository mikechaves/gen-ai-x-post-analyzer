# Gen AI Capstone: X Post Claim Analyzer

**Author:** Michael Chaves
**Date:** April 2025

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Project Overview

This project was developed as the Capstone for the **5-Day Gen AI Intensive Course with Google** (Spring 2025), hosted on Kaggle.

The goal is to explore how Generative AI can assist users in analyzing information encountered on social media platforms like X (formerly Twitter). Specifically, it focuses on identifying potentially verifiable factual claims within posts and attempting to find supporting or contradicting information using simulated external knowledge.

**Competition Link:** [Gen AI Intensive Course Capstone 2025Q1](https://www.kaggle.com/competitions/gen-ai-intensive-course-capstone-2025q1)

**Disclaimer:** This tool is an educational prototype using sample data and simulated knowledge sources. It demonstrates specific Gen AI techniques but is **NOT** a definitive fact-checker or truth detector.

## Goal

To build a prototype Gen AI assistant that:
1.  **Extracts** potentially verifiable factual claims from sample X posts.
2.  **Attempts Verification** by querying a simulated knowledge base using Function Calling.
3.  **Summarizes** the verification findings concisely and grounded in the available evidence.

## Technical Approach

The core workflow implemented in the accompanying Kaggle Notebook (`.ipynb` file) is:
1.  **Sample Data:** Uses a static list of sample posts for demonstration.
2.  **Claim Extraction:** A Generative Model (Google Gemini) is prompted using Few-Shot examples to identify factual claims and output them in a structured JSON format.
3.  **Simulated Verification:**
    * A small, hardcoded Python dictionary acts as a Knowledge Base (KB).
    * A Python function (`search_knowledge_base`) queries this KB.
    * This function is defined as a "tool" for the Gemini model using Function Calling.
    * For each extracted claim, the model decides whether to call the search function with relevant keywords.
    * The result from the KB search (or the model's decision not to call) is recorded.
4.  **Summarization:** A final call to the Gemini model generates a grounded summary sentence based *only* on the result of the verification step.

## Gen AI Capabilities Demonstrated

This project showcases the following key Generative AI capabilities:

* **Structured Output:** Using the LLM to generate output in a specific JSON schema for reliable parsing of extracted claims and keywords.
* **Few-Shot Prompting:** Providing examples within the prompt to improve the LLM's accuracy in identifying factual claims and adhering to the output format.
* **Function Calling:** Defining a Python function as a tool and enabling the LLM to decide when and how to call it to interact with the simulated knowledge base.
* **Document Understanding & Grounding:** Processing input text (posts, KB results) and ensuring the final summary is based strictly on the provided evidence from the verification step, preventing hallucination.

## Viewing the Notebook

The complete implementation, including code, detailed explanations, and outputs, can be viewed as a public Kaggle Notebook:

**➡️ https://www.kaggle.com/code/mikechaves/gen-ai-capstone-x-post-claim-analyzer**

## Running the Notebook Locally (Optional)

The notebook is best viewed and run on Kaggle. To run locally:

1.  **Dependencies:** Install necessary libraries:
    ```bash
    pip install google-generativeai transformers torch torchvision torchaudio # Add others if used
    ```
    (See `requirements.txt` if you create one).
2.  **API Key:** You will need a Google Gemini API Key. The notebook uses Kaggle Secrets; for local execution, you would typically set this as an environment variable (e.g., `GOOGLE_API_KEY`) and modify the code to read it using `os.environ.get("GOOGLE_API_KEY")`. **Do not hardcode your key.**
3.  **Internet Connection:** An internet connection is required the first time you run the code (or after clearing the cache) to download the `microsoft/deberta-v3-small` model and tokenizer files from the Hugging Face Hub via the `transformers` library.
4.  **Execution:** Run the cells sequentially in a Jupyter environment.

## Limitations

* Uses static, small sample data, not a real-time feed.
* Evidence search is **simulated** against a tiny, predefined knowledge base.
* **Not a truth detector**; findings are relative to the limited KB.
* Relies on LLM performance for all steps, which is not guaranteed to be perfect.

## License

This project (the code and documentation written by the author) is licensed under the **Apache License 2.0**. See the `LICENSE` file for details. Underlying libraries and models retain their original licenses.
