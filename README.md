# AutoQGen: Scalable Multiple-Choice Question Generation from Large Texts

AutoQGen is a minimum viable product (MVP) designed to generate **high-quality multiple-choice questions (MCQs)** from large text documents such as textbooks, research papers, and training manuals. 

The project is inspired by the concepts in the *Savaal* research paper but focuses on **scalability, creativity, and modularity** rather than direct replication. Its goal is to provide a foundation for building automated quiz generation systems that can support education, training, and assessment at scale.


## Features

-   **PDF Ingestion**: Processes text directly from PDF documents.
-   **Scalable Pipeline**: Handles large documents by chunking text to fit within LLM context windows.
-   **Semantic Search (RAG)**: Uses sentence embeddings to find the most conceptually relevant passages for each question, a core technique of modern Retrieval Augmented Generation (RAG) systems.
-   **Cost-Efficient Processing**: Implements **batching** for API calls to reduce costs and **caching** for intermediate results (like embeddings) to make subsequent runs instantaneous.
-   **Advanced Quality Control**: Employs a three-layer cascade to ensure question quality:
    1.  A fast, non-LLM **pre-filter** for basic syntax checks.
    2.  An **AI quality score** to judge conceptual depth and clarity.
    3.  A **semantic verification** step to ensure the answer is supported by the source text.
-   **Difficulty Control**: Generates questions with "easy," "medium," and "hard" difficulty levels based on Bloom's Taxonomy.
-   **Explainable Output**: The final JSON output includes the source passages used to generate each question, ensuring transparency and verifiability.

## System Architecture: The Pipeline

The system processes documents in a multi-stage pipeline designed for quality and efficiency:

**➡️ Stage 0: Caching & Pre-processing**
-   Upon first run, the system extracts text from the PDF, splits it into manageable chunks, and generates numerical embeddings for each chunk.
-   These expensive results are **cached**. On subsequent runs, the system loads the cached data instantly, saving significant time and cost.

**➡️ Stage 1: Concept Extraction & Synthesis**
-   The text chunks are grouped into **batches** and sent to a cost-effective LLM (`gpt-3.5-turbo` or `gpt-4o-mini`) in a single API call to extract key concepts.
-   The raw concepts are then synthesized by a second LLM call to create a final, deduplicated list of core topics.

**➡️ Stage 2: Question Generation (RAG)**
-   For each concept, the system uses **semantic search** to retrieve the most relevant source passages (the "Retrieval" step).
-   A powerful LLM (`gpt-4o`) is then prompted with the concept, the retrieved passages, and a difficulty level to generate a high-quality question (the "Augmented Generation" step).

**➡️ Stage 3: Quality Control Cascade**
-   Each generated question is passed through a rigorous three-layer filter:
    1.  **Pre-filter**: A fast, local check for formatting and length.
    2.  **AI Score**: A cost-effective LLM scores the question's quality.
    3.  **Semantic Verification**: A final check confirms the answer is semantically similar to the source text.
-   Only questions that pass all three checks are included in the final output.


## Quick Start

Follow these steps to get the project running quickly:

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/AutoQGen.git
cd AutoQGen
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Create a `.env` file with your OpenAI API key (required)**  
Create a file named `.env` in the project root and add the following line:
```
OPENAI_API_KEY=your_openai_api_key_here
```

4. **Run the most recent iteration (itr) file**  
The project’s main pipeline lives in the latest iteration notebook (for example `itr_2.ipynb`). 


5. **Where output appears**  
By default the notebook writes generated MCQs to `quiz_output.json`. Check or change the output path in the notebook variables if needed.



## How It Works

1. **Text Preprocessing:** The input document is split into manageable chunks.
2. **Question Generation:** Each chunk is processed by an NLP model to generate MCQs.
3. **Answer Validation:** Generated questions are checked for quality and correctness.
4. **Aggregation:** Final set of MCQs is compiled and saved.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request. For major changes, open an issue first to discuss your ideas.

## License

MIT License – feel free to use and extend this project!
