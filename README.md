# README.md

[Colab Demo Notebook](https://colab.research.google.com/drive/17_M4j1LR0BfY1aOrxYpvCLj1Rwyt1ey_?usp=sharing)

## Quick Start with Colab
To quickly test out the program, use the provided Colab notebook:

This Colab environment is pre-configured for easy testing of the Retrieval-Augmented Generation (RAG) pipeline using PostgreSQL, pgVector, and various Language Models (LLMs). Follow the instructions below to start interacting with the system.

## How to Use the Colab Notebook

1. **Open the Colab Notebook**: 
   Click the link above to launch the notebook in Google Colab.

2. **Set Runtime**: 
   Enable GPU for better performance on local inference (requires colab-pro, suggested for llama-8B, etc):
   - Go to `Runtime` > `Change runtime type`.
   - Set **Hardware accelerator** to `GPU` and click **Save**.

3. **Install Dependencies**:
   Run the first cell to install all necessary libraries and tools, including PostgreSQL, TimescaleDB, pgVector, and LLM integrations like OpenAI or Local Ollama.

4. **Configure Settings**:
   - Modify the configuration parameters if needed (e.g., LLM Mode, API keys) by editing the `CFG` class.
   - Ensure you set up your API keys if you are using external services like OpenAI or Anthropic. For local inference, ensure your runtime supports Ollama.

5. **Load Content**:
   - Use the "Load from URLs" tab in the Gradio interface to input Wikipedia URLs or other document sources.
   - Example URLs are pre-loaded for testing.

6. **Ask Questions**:
   - Switch to the "Ask Question" tab.
   - Type your question in the provided textbox and hit "Submit".
   - The system will retrieve relevant documents from the database and generate an answer using the selected LLM.

7. **Monitor Output**:
   The Gradio interface will display both the answer and the context retrieved from the database. You can adjust the number of chunks to fetch and whether to use context or not.

## Mode Selections Available
- **LLM Modes**: Choose between `LocalOllama`, `OpenAI`, or `AnCo (Anthropic + Cohere)` models.
- **PGAI Modes**: Interact with PostgreSQL and pgVector using either SQL or stored function calls.

## Customization
To customize the setup (e.g., change models, vector embedding sizes), modify the respective sections in the notebook:
- LLM configurations are located in the `CFG` class.
- Document loading and embedding processes are controlled by the `Vector_Store` class.

## Example Workflow

1. Load content using Wikipedia URLs:
   ```text
   https://en.wikipedia.org/wiki/World_War_II
   https://en.wikipedia.org/wiki/World_War_I
   ```
   
2. Ask a question related to the content:
   ```text
   How many lives were lost in World War Two?
   ```

The system will fetch relevant document chunks and use the context to generate a response using the selected LLM.

## Testing Functions
Several test functions are included to validate the system:
- `test_load_urls()`: Test loading documents into the database.
- `test_fetch_documents()`: Test fetching documents by keywords and embeddings.
- `test_rag()`: Run a full RAG chain to see how the system retrieves and generates answers.

## License
This project is open-source and available under the MIT license.
