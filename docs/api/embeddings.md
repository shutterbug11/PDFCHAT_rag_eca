# Embeddings API

This page documents the vector embeddings and database management using ChromaDB and Nomic.

## VectorStore

The `VectorStore` class manages the initialization and persistence of the Chroma vector database.

```python
class VectorStore:
    """Manages vector embeddings and database operations."""

    def __init__(self, embedding_model: str = "nomic-embed-text", persist_directory: str = "data/vectors"):
        """Initialize with embedding model and storage path."""
```

### Constructor Parameters

- `embedding_model` (str): Name of the Ollama embedding model (default: "nomic-embed-text").
- `persist_directory` (str): Path to store the vector database (default: "data/vectors").

### Methods

#### create_vector_db

```python
def create_vector_db(self, documents: List, collection_name: str = "local-rag") -> Chroma:
    """Create vector database from documents with persistence."""
```

**Parameters:**
- `documents` (List): List of processed `Document` objects.
- `collection_name` (str): Name of the Chroma collection.

**Returns:**
- `Chroma`: Initialized vector database instance.

#### delete_collection

```python
def delete_collection(self) -> None:
    """Delete vector database collection."""
```

**Description:**
- Removes the current collection from the database. Useful for resetting or cleaning up.

## Usage Example

```python
from src.core.embeddings import VectorStore

# Initialize
store = VectorStore(persist_directory="./my_vectors")

# Create DB from docs
# documents = ...
# vector_db = store.create_vector_db(documents=documents, collection_name="test_collection")

# Cleanup
# store.delete_collection()
```