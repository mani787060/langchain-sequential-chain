# LangChain Sequential Chains (LCEL)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green)](https://www.langchain.com/)
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![Gemini](https://img.shields.io/badge/Model-Google%20Gemini-4285F4)](https://ai.google.dev/)

## 🏗️ Project Overview
This repository demonstrates how to build **Sequential AI Workflows**. In real-world applications, a single prompt is rarely enough. This project showcases how to break a complex problem into smaller, manageable steps—orchestrating a "pipeline" where the AI first generates a thought or plan, and then uses that result to perform a secondary action.

---

## 🛠️ Key Technical Implementations

### 1. Data Dependency Mapping
* **Output-to-Input Flow:** Configuring Chain B to wait for and ingest the result from Chain A, creating a seamless logical progression.
* **Variable Passing:** Managing dictionary inputs to ensure context is preserved across the entire sequence.

### 2. Multi-Stage Orchestration
* **Step 1 (Analysis):** The first model call handles the initial reasoning or extraction.
* **Step 2 (Synthesis):** The second model call takes that structured data and generates the final user-facing result.

### 3. Scalable LCEL Architecture
* **Modularity:** Each step in the sequence is its own independent chain, making it easy to swap prompts or models for specific stages without breaking the whole system.
* **Readability:** Using the `|` operator to visualize the data flow clearly within the code.

---

## 💻 Tech Stack
* **Language:** Python 3.9+
* **Orchestration:** LangChain (`langchain-core`, `langchain-google-genai`)
* **Model:** Google Gemini Pro
* **Environment:** `python-dotenv`

---

## 🚀 Getting Started

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-username/langchain-sequential-workflow-lcel.git](https://github.com/your-username/langchain-sequential-workflow-lcel.git)

2. **Install Dependencies:**
   ```bash
   pip install -U langchain-core langchain-google-genai python-dotenv

3. **Setup API Key:**
   Create a .env file in the root directory:
   ```bash
   GOOGLE_API_KEY=your_gemini_api_key_here

4. **Run the Workflow:**
   ```bash
   python sequential_chain.py
   
