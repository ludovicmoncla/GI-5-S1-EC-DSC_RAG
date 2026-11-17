# GI-5-S1-EC-DSC - Retrieval Augmented Generation (RAG)

This repository contains the tutorial files for the 2026-2027 Data Science course of 5GI INSA Lyon.


In this lab, you will explore Retrieval Augmented Generation (RAG) techniques, which integrate information retrieval with generative large language models (LLMs) to improve the quality of generated text based on relevant external documents.


## Session Schedule

This lab is organised into three two-hour sessions:

| Session | Date and time | Location | Format |
| --- | --- | --- | --- |
| Session 1 | Tuesday, December 1, 10:00–12:00 | Room Thorgal | NLP – Supervised lab: Retrieval-Augmented Generation (RAG) |
| Session 2 | Tuesday, December 8, 10:00–12:00 | Room Thorgal | NLP – Supervised lab: Retrieval-Augmented Generation (RAG) |
| Session 3 | Tuesday, December 15, 10:00–12:00 | Room Blake & Mortimer | NLP – Supervised lab: Retrieval-Augmented Generation (RAG) |

### Teamwork

You may work in groups of two or three. Group members may divide the tasks—for example, retrieval, generation, and evaluation—or use pair or group programming to work on the same code. Share your intermediate results regularly: every member must understand the complete pipeline and be able to explain the group's design choices and conclusions.


## Academic Integrity and Authorized Resources

To ensure fair evaluation and genuine learning, please follow these rules when completing the lab:

✅ You are allowed to:
* Search for information using search engines (Google, Bing, etc.)
* Consult official documentation for libraries and tools used in the lab
* Use educational or technical websites such as Stack Overflow, GeeksforGeeks, or academic blogs
* Discuss ideas and concepts with classmates at a high level
* Share code and written work with the members of your declared group, but not with other groups
* Ask the teacher questions during the lab sessions if you need clarification or guidance

🚫 You are not allowed to:
* Use generative AI tools (e.g., ChatGPT, Copilot, Gemini, Claude, etc.) to generate or modify code or written explanations
* Submit code, text, or analyses that were not written or understood by you
* Copy solutions directly from other students or online repositories

🧭 Important note

You are encouraged to understand, test, and experiment with the concepts presented in this lab.
External sources can help you learn — but all submitted work must reflect your own understanding and be authored by you.


## 1. Objective

This project explores the use of RAG to support decision-making and knowledge sharing in railway maintenance operations, using the SMRT Maintenance Logs dataset as a domain-specific knowledge base.

The dataset contains thousands of real-world maintenance records describing faults, diagnostics, and corrective actions across a wide range of train subsystems. By combining semantic retrieval with LLMs, the system must enable natural-language access to historical maintenance knowledge that would otherwise remain locked in unstructured logs.

The proposed RAG system will be designed to support three key user groups:
* Maintenance engineers, by retrieving similar past fault cases and summarizing proven corrective actions to accelerate troubleshooting and reduce downtime.
* Operations control centers, by providing rapid situational awareness and context when incidents occur, enabling informed operational decisions under time pressure.
* Knowledge transfer to junior staff, by transforming tacit, experience-based maintenance knowledge into explainable, searchable guidance derived from historical records.



## 2. Roadmap and Steps to Complete

![RAG Workflow](./assets/img/rag_workflow.png)

The project follows an incremental progression across the three sessions. Each session builds on the output of the previous one: first create a reliable retrieval baseline, then assemble and improve the complete RAG pipeline, and finally evaluate its quality and robustness.

### Session 1 — Build the retrieval baseline

**Objective:** transform the maintenance logs into a searchable knowledge base and verify that relevant records can be retrieved for a natural-language question.

1. Load and explore the dataset, identify the fields needed by the RAG system, and define the metadata to preserve for source tracking.
2. Clean and preprocess the documents, then split them into chunks.
3. Compute embeddings with `sentence-transformers` and index them in `ChromaDB`.
4. Implement a retrieval function that returns the top matching chunks, their similarity scores, and their metadata.
5. Reserve time to start the evaluation dataset: select real maintenance records, write questions that should retrieve them, and record their source IDs.
6. Manually inspect the retrieved results and have another group member validate the question–document associations.
7. Run the Session 1 experiments on chunking, embedding models, and retrieval preprocessing (Section 7.1).

**Expected outcome:** given a question, the system returns relevant maintenance records together with enough metadata to identify their origin. The group also has a first validated set of evaluation questions and relevant source IDs.

### Session 2 — Complete the RAG pipeline

Detailed objectives and instructions will be published at the beginning of Session 2.

### Session 3 — Evaluate the RAG system

Detailed objectives and instructions will be published at the beginning of Session 3.


## 3. Quick Start

Create a virtual environment and install the dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On Windows PowerShell, activate the environment with `.venv\Scripts\Activate.ps1` instead.

The notebooks provide code examples for discovering the key stages of a RAG workflow:

- [loading and exploring the dataset](./notebooks/1_load_dataset.ipynb);
- [computing embeddings](./notebooks/2_embeddings.ipynb);
- [creating and querying a vector database](./notebooks/3_vector_db.ipynb);
- generating answers with either [LM Studio](./notebooks/4_generation_llm_lmstudio.ipynb) or [Gemini and Gemma](./notebooks/4_generation_llm_gemini.ipynb); and
- [building an evaluation set and computing RAG metrics](./notebooks/5_evaluation.ipynb).

These notebooks are starting points, not a complete pipeline or a solution to submit. Run the examples, inspect and modify the code, and make sure you understand the role of each step. Then use the relevant ideas to design and implement your own end-to-end RAG pipeline. You may organize your implementation in one or more notebooks, Python modules, or a combination of both.

LLM access is only required from Session 2 onward. If the dataset cannot be downloaded, follow the access instructions in Section 4. Store API keys in environment variables or in a local `.env` file, and never commit them to a public repository.


## 4. Dataset

The [SMRT-Maintenance-Logs dataset](https://huggingface.co/datasets/lmoncla/SMRT-Maintenance-Logs) is a text dataset consisting of 10,785 real maintenance log entries from SMRT Trains.
Each entry in the dataset includes two key fields:
* `text` – A string combining a reported fault and the corresponding corrective action, separated by five tildes (`~~~~~`).
* `label` – A categorical label identifying the train component that was repaired or replaced.



## 5. LLM Access

The use of LLMs is required for the generation step of your RAG system. Several options are available to you:


### 5.1. LM Studio API for Local LLMs

The first option is to run small local LLMs on your own machine using [LM Studio](https://lmstudio.ai/). LM Studio allows you to run various open-source LLMs locally and provides an OpenAI-compatible API for easy integration.

See the example notebook demonstrating how to query local LLMs through the LM Studio API:
- [LLM generation with LM Studio](./notebooks/4_generation_llm_lmstudio.ipynb)

### 5.2. Gemini API for Gemini and Gemma Models

The second option is to use Google's Gemini and Gemma models through the [Gemini API](https://aistudio.google.com/).

Model availability and rate limits depend on the model, project, and usage tier, and may change over time. Check the [current model catalogue](https://ai.google.dev/gemini-api/docs/models) and your project's [active rate limits](https://aistudio.google.com/rate-limit?timeRange=last-28-days) before starting your experiments.

To use the API, you need a Google account and an API key from [Google AI Studio](https://aistudio.google.com/app/api-keys).

An example notebook demonstrating how to query Gemini and Gemma models through the Gemini API is provided:

- [LLM generation with Google's Gemini and Gemma models](./notebooks/4_generation_llm_gemini.ipynb)


## 6. Evaluation Protocol

Evaluation starts during Session 1, not after the RAG pipeline is complete. Before tuning a configuration, create a small development set; keep a separate final set unchanged for the comparison in Session 3. A practical starting target for each group is 15 answerable questions and 5 out-of-scope questions. Increase this number if time permits.

### 6.1. Build the evaluation dataset

Each answerable question must be linked to at least one relevant document that is present in the indexed corpus. Use the following process:

1. Select maintenance records covering several components and fault types.
2. Separate the reported fault from the corrective action at the `~~~~~` delimiter.
3. Write a natural-language question from the reported fault without copying the complete log or revealing the corrective action.
4. Record the ID of every document needed to answer the question.
5. Write a short reference answer using only those documents.
6. Ask another group member to verify the question, relevant source IDs, and reference answer.
7. Reserve some questions for the final evaluation and do not use them to select parameters or prompts.

Store at least the following fields:

| Field | Description |
| --- | --- |
| `question_id` | Stable identifier for the evaluation question |
| `question` | Natural-language maintenance question |
| `relevant_source_ids` | One or more source IDs that should be retrieved |
| `reference_answer` | Expected answer supported by the relevant sources |
| `answerable` | Whether the indexed corpus contains sufficient evidence |
| `category` | Component or fault family used to check dataset diversity |
| `split` | `development` for tuning or `final` for the held-out comparison |

Start with questions about a single known record, then add a few questions requiring several records. The following prompts are starting ideas and must be checked against the actual logs before being added to the evaluation dataset:

| Theme | Example question |
| --- | --- |
| Braking | How was an intermittent BCU brake fault diagnosed or corrected? |
| Pneumatic equipment | What inspections or repairs followed a reported air dryer fault? |
| Lighting | What corrective action was taken for a blown saloon light? |
| Air conditioning | How was air-conditioning condensation or water leakage handled? |
| Headlights | What actions were taken when a train headlight was not working? |
| Recurrent faults | Which corrective actions recur across similar faults affecting the same component? |

Also include out-of-scope questions—for example, a request for a future failure prediction or the live status of a train—to test whether the system abstains when no supporting document exists.

### 6.2. Measure retrieval and generation separately

**Retrieval evaluation** compares the ranked source IDs returned by the vector database with `relevant_source_ids`:

- **Hit@K:** proportion of questions with at least one relevant document in the top K.
- **Recall@K:** proportion of all relevant documents found in the top K.
- **MRR@K:** rewards systems that rank the first relevant document near the top.
- **Latency:** time required to retrieve the top K documents.

**Generation evaluation** uses both automatic measures and manual inspection:

- lexical or embedding similarity to the reference answer;
- correctness of the answer;
- faithfulness of claims and citations to the retrieved sources;
- citation coverage and validity;
- correct abstention on unanswerable questions;
- response time.

Automatic scores are indicators, not a substitute for reading a sample of the answers. Use the same evaluation questions and generation settings when comparing configurations.

The [evaluation notebook](./notebooks/5_evaluation.ipynb) provides a runnable example of the evaluation-set format, Hit@K, Recall@K, MRR@K, lexical F1, embedding similarity, citation checks, abstention accuracy, and a manual scoring grid.


## 7. Experiments

The experiments follow the same three-session progression as the implementation. Start each experiment from a documented baseline, change one factor at a time, and reuse the same test questions whenever possible. For every configuration, record the parameters, retrieval results, answer-quality measurements, and execution time so that the comparison is reproducible.

### 7.1. Session 1 — Retrieval experiments

1. **Chunk size and overlap**
    - Test small (50 tokens), medium (200 tokens), and large (500 tokens) chunks.
    - Try different overlap sizes and observe how much useful context is preserved.
    - Determine which chunk size and overlap maximize retrieval relevance.

2. **Embedding models**
    - Compare pre-trained `sentence-transformers` models such as `all-MiniLM-L6-v2` and `paraphrase-MiniLM-L12-v2`.
    - Measure retrieval quality, indexing time, query time, and storage requirements.
    - Identify the best trade-off between accuracy and efficiency.

3. **Retrieval quality and preprocessing**
    - Assess the relevance of retrieved documents before passing them to the LLM.
    - Test text normalization, stop-word removal, and other justified preprocessing choices.
    - Analyze which preprocessing choices improve retrieval and retain the best configuration for Session 2.

### 7.2. Session 2 — TBA

### 7.3. Session 3 — TBA


## 8. Deliverables

- A short technical report (3-4 pages)
- Code + notebook(s) with comments
- The evaluation dataset with questions, relevant source IDs, reference answers, categories, and splits
- A summary table and figures comparing experiments
