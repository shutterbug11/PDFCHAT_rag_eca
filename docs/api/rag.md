# RAG Pipeline API

This page documents the RAG (Retrieval Augmented Generation) pipeline components used in the application.

## RAGPipeline

The `RAGPipeline` class orchestrates the retrieval and generation process using LangChain components.

```python
class RAGPipeline:
    """Manages the RAG (Retrieval Augmented Generation) pipeline."""
    
    def __init__(self, vector_db: Any, llm_manager: LLMManager):
        """Initialize RAG pipeline components."""
```

### Constructor Parameters

- `vector_db`: Initialized VectorStore or Chroma instance.
- `llm_manager`: Instance of `LLMManager` for handling model interactions.

### Main Methods

#### get_response

```python
def get_response(self, question: str) -> str:
    """Get response for a question using the RAG pipeline."""
```

**Parameters:**
- `question` (str): The user's query.

**Returns:**
- `str`: The generated answer based on retrieved documents.

**Internal Logic:**
1. Uses a `MultiQueryRetriever` to generate alternative versions of the question.
2. Retrieves relevant documents from the vector database.
3. passes context and question to the LLM via a prompt chain.
4. Returns the final string response.

### Internal Configuration

The pipeline automatically sets up:

1. **Retriever**: `MultiQueryRetriever` using the configured LLM.
2. **Chain**: A LangChain `RunnablePassthrough` sequence combining retrieval, prompting, and generation.

## Usage Example

```python
from src.core.rag import RAGPipeline
from src.core.llm import LLMManager
from src.core.embeddings import VectorStore

# Initialize dependencies
llm_manager = LLMManager(model_name="qwen3:8b")
# Assuming vector_db is already created
vector_store = VectorStore(embedding_model="nomic-embed-text")
vector_db = vector_store.create_vector_db([]) 

# Create pipeline
rag_pipeline = RAGPipeline(vector_db=vector_db, llm_manager=llm_manager)

# Query
answer = rag_pipeline.get_response("What are the key findings?")
print(answer)
```