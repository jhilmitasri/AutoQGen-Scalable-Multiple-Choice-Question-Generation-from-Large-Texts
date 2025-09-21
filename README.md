# AutoQGen: Scalable Multiple-Choice Question Generation from Large Texts

AutoQGen is a minimum viable product (MVP) designed to generate **high-quality multiple-choice questions (MCQs)** from large text documents such as textbooks, research papers, and training manuals. 

The project is inspired by the concepts in the *Savaal* research paper but focuses on **scalability, creativity, and modularity** rather than direct replication. Its goal is to provide a foundation for building automated quiz generation systems that can support education, training, and assessment at scale.

## Features

- **Scalable Processing:** Efficiently handles large volumes of text by chunking and parallel processing.
- **Creative Question Generation:** Uses advanced NLP models to generate diverse and challenging MCQs.
- **Modular Design:** Easily customizable components for text preprocessing, question generation, and answer validation.
- **Multi-Domain Support:** Applicable to various subjects and document types.
- **User-Friendly Interface:** Simple command-line tools and clear documentation for quick setup.


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
