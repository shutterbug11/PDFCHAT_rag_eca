# LLM Manager API

This page documents the Language Model management components built on top of LangChain and Ollama.

## LLMManager

The `LLMManager` class handles configuration and prompt management for Ollama models.

```python
class LLMManager:
    """Manages LLM configuration and prompts."""
    
    def __init__(self, model_name: str = "llama2"):
        """Initialize LLM manager with model name."""
```

### Constructor Parameters

- `model_name` (str): Name of the Ollama model to use (default: "llama2").
- **Initializes**: `ChatOllama` instance from `langchain_ollama`.

### Methods

#### get_query_prompt

```python
def get_query_prompt(self) -> PromptTemplate:
    """Get query generation prompt."""
```

**Returns:**
- `PromptTemplate`: A template that instructs the LLM to generate alternative versions of the user's question to improve retrieval (Multi-Query approach).

#### get_rag_prompt

```python
def get_rag_prompt(self) -> ChatPromptTemplate:
    """Get RAG prompt template."""
```

**Returns:**
- `ChatPromptTemplate`: A template for the final answer generation, enforcing the constraint to use "ONLY" the provided context.

## Usage Example

```python
from src.core.llm import LLMManager

# Initialize manager
manager = LLMManager(model_name="qwen3:8b")

# access underlying LangChain LLM
llm = manager.llm

# Get prompts for chains
query_prompt = manager.get_query_prompt()
rag_prompt = manager.get_rag_prompt()
```