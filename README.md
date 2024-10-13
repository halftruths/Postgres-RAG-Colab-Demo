# README.md

[Colab Demo Notebook](https://colab.research.google.com/drive/17_M4j1LR0BfY1aOrxYpvCLj1Rwyt1ey_?usp=sharing)

## Quick Start with Colab
To quickly test out the program, use the provided [Colab Notebook](https://colab.research.google.com/drive/17_M4j1LR0BfY1aOrxYpvCLj1Rwyt1ey_?usp=sharing):

This Colab environment is pre-configured for easy testing of the Retrieval-Augmented Generation (RAG) pipeline using PostgreSQL, pgVector, and various Language Models (LLMs). Follow the instructions below to start interacting with the system.

## How to Use the Colab Notebook

1. **Open the Colab Notebook**: 
   Click the link above to launch the notebook in Google Colab.

2. **Set Runtime (Optional)**: 
   Enable GPU for better performance on local inference (suggested for llama-8B, etc):
   - Default local model is llama3.2:3b
   - Go to `Runtime` > `Change runtime type`.
   - Set **Hardware accelerator** to `T4` and click **Save**. (Accelerate local inference, Requires Colab Pro)
   - Set Runtime to High-RAM Option (Reduce install time from 10min to 5min, Requires Colab Pro)

4. **Install Dependencies**:
   - Select 'Runtime->Run All' to install all necessary libraries and tools, including PostgreSQL, TimescaleDB, pgVector, and LLM integrations like OpenAI or Local Ollama.

5. **Configure Settings**:
   - Modify the configuration parameters if needed (e.g., self.LLM_MODE = LLM_Mode.OpenAI, self.PGAI_MODE = PGAI_Mode.Function) by editing the `CFG` class.
   - API keys for testing have been preloaded, may run out and require replacement with your own keys. For local inference (self.LLM_MODE = LLM_Mode.LocalOllama), Ollama will be automatically installed by default.

6. **Load Content**:
   - Use the "Load from URLs" tab in the Gradio interface to input Wikipedia URLs or other document sources.
   - Example URLs are pre-loaded for testing.

7. **Ask Questions**:
   - Switch to the "Ask Question" tab.
   - Type your question in the provided textbox and hit "Submit".
   - The system will retrieve relevant documents from the database and generate an answer using the selected LLM.

8. **Monitor Output**:
   The Gradio interface will display both the answer and the context retrieved from the database. You can adjust the number of chunks to fetch and whether to use context or not.

## Mode Selections Available
- **CFG.LLM_Mode**: Choose between `LocalOllama`, `OpenAI`, or `AnCo (Anthropic + Cohere)` models.
   - ```
     class LLM_Mode(Enum):
       LocalOllama = 1 # use local Ollama server
       OpenAI      = 2 # use Openai through pgai
       AnCo        = 3 # use Anthropic for chat and Cohere for embedding
     ```
- **CFG.PGAI_Mode**: Choose from PostgreSQL and pgVector using either SQL or stored function calls.
   - ```
     class PGAI_Mode(Enum):
       Disabled = 1 # never use pgai to access ai, use python ollama module instead
       Sql      = 2 # use SQL to access pgai functions
       Function = 3 # define postgres stored functions to access pgai functions
     ```

## Customization
To customize the setup (e.g., change models, vector embedding sizes), modify the respective sections in the notebook:
- To change Llama model when running local inference, change MODEL_NAME string
   - See 'self.CHAT_MODEL = "llama3.2:3b" #CHANGE THIS LINE TO SPECIFY LOCAL LLAMA MODEL'
- LLM configurations are located in the `CFG` class.
- Document loading and embedding processes are controlled by the `Vector_Store` class.

## Example Workflow

1. Load content using Wikipedia URLs:
   ```text
   https://en.wikipedia.org/wiki/World_War_II
   https://en.wikipedia.org/wiki/World_War_I
   ```
   Here, after loading the Wikipedia documents, embeddings are generated for the document chunks and then put in the vector store.
   
3. Ask a question related to the content:
   ```text
   How many lives were lost in World War Two?
   ```

The system will fetch relevant document chunks and use the context to generate a response using the selected LLM.

## License
This project is open-source and available under the MIT license.
