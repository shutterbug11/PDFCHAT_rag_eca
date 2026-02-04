# Document Processing API

This page documents the document processing components of Ollama PDF RAG.

## DocumentProcessor

The `DocumentProcessor` class handles PDF loading and text splitting.

```python
class DocumentProcessor:
    """Handles PDF document loading and processing."""
    
    def __init__(self, chunk_size: int = 7500, chunk_overlap: int = 100):
        """Initialize document processor with chunking parameters."""
```

### Constructor Parameters

- `chunk_size` (int): Number of characters per chunk (default: 7500).
- `chunk_overlap` (int): Number of overlapping characters (default: 100).
- **Initializes**: `RecursiveCharacterTextSplitter`.

### Methods

#### load_pdf

```python
def load_pdf(self, file_path: Path) -> List:
    """Load PDF document."""
```

**Parameters:**
- `file_path` (Path): Path to the PDF file.

**Returns:**
- `List`: List of raw loaded documents (pages) using `UnstructuredPDFLoader`.

#### split_documents

```python
def split_documents(self, documents: List) -> List:
    """Split documents into chunks."""
```

**Parameters:**
- `documents` (List): List of loaded documents.

**Returns:**
- `List`: List of split and chunked documents, ready for embedding.

## Usage Example

```python
from src.core.document import DocumentProcessor
from pathlib import Path

# Initialize
processor = DocumentProcessor(chunk_size=5000)

# Load and split
# raw_docs = processor.load_pdf(Path("docs/manual.pdf"))
# chunks = processor.split_documents(raw_docs)

# print(f"Created {len(chunks)} chunks")
```