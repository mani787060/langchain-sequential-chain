# LangChain Sequential Chains using LCEL

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green.svg)](https://www.langchain.com/)
[![Google Gemini](https://img.shields.io/badge/LLM-Google%20Gemini-4285F4.svg)](https://ai.google.dev/)
[![LCEL](https://img.shields.io/badge/Workflow-LCEL-orange.svg)](https://python.langchain.com/docs/concepts/lcel/)

A practical Generative AI project demonstrating **sequential LLM workflows using LangChain Expression Language (LCEL)**. The application uses Google Gemini to generate a detailed report on a given topic and then transforms that report into a concise five-point summary.

## 📌 Project Overview

A single LLM call is not always enough to complete a multi-step task. Sometimes, an application must first generate detailed content and then use that output to perform another operation.

This project demonstrates how to connect multiple prompt-model-parser stages into a single sequential pipeline using LangChain's `|` operator.

The workflow follows two main stages:

1. **Report Generation:** Generate a detailed report on a given topic.
2. **Summary Generation:** Use the generated report as input to create a five-point summary.

For the current example, the topic is **Unemployment in India**.

## 🎯 Project Objectives

- Understand sequential execution in LangChain.
- Learn how LangChain Expression Language (LCEL) connects components.
- Pass the output of one LLM stage into the next stage.
- Work with reusable prompt templates.
- Integrate Google Gemini through LangChain.
- Convert detailed LLM-generated content into a concise summary.
- Visualize the chain's structure using LangChain's graph functionality.

## ⚙️ How the Workflow Works

<pre>
Input Topic
    |
    v
Prompt 1: Generate a Detailed Report
    |
    v
Google Gemini
    |
    v
String Output Parser
    |
    v
Prompt 2: Generate a Five-Point Summary
    |
    v
Google Gemini
    |
    v
String Output Parser
    |
    v
Final Five-Point Summary
</pre>

### Stage 1: Detailed Report Generation

The first prompt receives a topic through the `topic` variable.

```python
prompt1 = PromptTemplate(
    template="Generate a detailed report on {topic}",
    input_variables=["topic"]
)
```

The model uses this prompt to generate a detailed report about the specified topic.

### Stage 2: Five-Point Summary Generation

The second prompt receives the first stage's output through the `text` variable.

```python
prompt2 = PromptTemplate(
    template="Generate a 5 pointer summary from the following text \n {text}",
    input_variables=["text"]
)
```

This stage converts the detailed report into a more concise, five-point summary.

### Stage 3: Sequential Chain Composition

The components are connected using LCEL:

```python
chain = prompt1 | model | parser | prompt2 | model | parser
```

The pipe (`|`) operator connects each component, passing its output to the next component.

The `StrOutputParser` converts model responses into plain strings, allowing the generated report to be passed into the second prompt.

### Stage 4: Execute the Chain

```python
result = chain.invoke({"topic": "Unemployment in India"})
print(result)
```

The chain executes both stages in sequence and prints the final summary.

### Stage 5: Visualize the Workflow

```python
chain.get_graph().print_ascii()
```

This displays an ASCII representation of the connected chain components, helping you understand the workflow structure.

## 🧠 Key Concepts Demonstrated

| Concept | Description |
|---|---|
| Sequential workflow | Executes multiple AI processing steps in order. |
| LangChain Expression Language | Connects prompts, models, and parsers into a pipeline. |
| `PromptTemplate` | Defines reusable prompts with input variables. |
| `ChatGoogleGenerativeAI` | Integrates the Google Gemini language model. |
| `StrOutputParser` | Converts model output into a plain string. |
| `chain.invoke()` | Executes the workflow with the provided input. |
| `get_graph()` | Exposes the structure of the composed chain. |

## 🛠️ Tech Stack

- **Language:** Python
- **LLM framework:** LangChain
- **Workflow composition:** LangChain Expression Language (LCEL)
- **Language model integration:** `langchain-google-genai`
- **Model:** `gemini-3.1-flash-lite-preview`
- **Prompt management:** `langchain-core`
- **Environment variable management:** `python-dotenv`

> **Note:** The configured Gemini model is a preview model. Its availability may change, so check Google's current model documentation if you encounter a model-access error.

## 📂 Repository Structure

```text
langchain-sequential-chain/
│
├── sequential_chain.py   # Sequential LCEL workflow
├── README.md             # Project documentation
└── .env                  # Local API key configuration (not committed)
```

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/mani787060/langchain-sequential-chain.git
cd langchain-sequential-chain
```

### 2. Create a Virtual Environment

**Windows:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
python -m pip install --upgrade pip
pip install langchain-core langchain-google-genai python-dotenv
```

### 4. Configure Your Google Gemini API Key

Obtain an API key through [Google AI Studio](https://aistudio.google.com/).

Create a file named `.env` in the project root:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
```

Replace the placeholder with your actual API key.

**Security reminder:** Never commit your real API key to GitHub. Add `.env` to your `.gitignore` file.

Example `.gitignore` entry:

```gitignore
.env
.venv/
__pycache__/
*.pyc
```

### 5. Run the Application

```bash
python sequential_chain.py
```

The script generates the report, passes it into the summary stage, and prints the final five-point summary. It also prints the chain's graph representation.

## 💡 Example Use Case

**Input topic:**

```text
Unemployment in India
```

**Expected output format:**

The application generates a concise summary containing five key points extracted from the detailed report, such as major factors, economic effects, challenges, and possible approaches to addressing unemployment.

*The exact content is generated dynamically by the language model and may vary between executions.*

## 🔍 Sequential Chains vs. Single LLM Calls

| Single LLM call | Sequential LCEL workflow |
|---|---|
| Performs one main generation step. | Connects multiple dependent steps. |
| Suitable for straightforward prompts. | Suitable for multi-stage processing. |
| Output is typically the result of one prompt. | Earlier output becomes input for a later stage. |
| Less orchestration is needed. | Makes multi-step workflows explicit and modular. |

## 🌱 Possible Improvements

This project can be extended by:

- Accepting topics from user input instead of hardcoding the topic.
- Adding exception handling for API and model errors.
- Using structured output for consistent summaries.
- Saving generated reports and summaries to files.
- Measuring execution time and token usage.
- Adding a third stage for fact-checking or extracting key statistics.
- Building a simple web interface for interactive use.

## 📚 Learning Resources

- [LangChain Documentation](https://python.langchain.com/docs/introduction/)
- [LangChain Expression Language](https://python.langchain.com/docs/concepts/lcel/)
- [Google Gemini API Documentation](https://ai.google.dev/gemini-api/docs)
- [Python Documentation](https://docs.python.org/3/)

## 👨‍💻 Author

**Mani Ratan**

- GitHub: [@mani787060](https://github.com/mani787060)
- LinkedIn: [Connect on LinkedIn](https://www.linkedin.com/in/mani-ratan-159963289/)

---

If you find this project useful for learning LangChain and Generative AI, consider giving the repository a ⭐.

**Learning goal:** Understand how multiple LLM operations can be composed into a single, reusable sequential workflow using LCEL.
