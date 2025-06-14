![githubbanner](https://github.com/user-attachments/assets/ec29fb84-2a87-43f1-acff-c5d907f77512)

# Retrieval Engine for Cognitive Agents

RECA is a flexible, lightweight memory and retrieval system designed to empower AI agents with real-time recall, long-term memory, and contextual search. Built for developers building autonomous tools, chat interfaces, personal assistants, or multi-agent systems - RECA enables your agents to remember what matters and find what they need, when they need it.

> Memory is not storage. It’s context, grounding, and cognition.

---

## 🧠 What is RECA?

RECA helps agents:

- Remember past messages, actions, or plans  
- Search over documents, web content, or APIs  
- Store knowledge as structured objects  
- Retrieve relevant info via semantic or keyword matching  
- Build and update memory on the fly  
- Inject memory into LLM prompts dynamically

RECA powers recall-aware agents. Instead of generating in isolation, they generate with purpose.

---

## ⚙️ Installation

RECA requires Python 3.10+ and uses Poetry for dependency management.

```
# Clone the repo
cd reca  
poetry install  
```

Or install it directly into your Poetry project:

```
poetry add reca  
```

---

## 🧱 MemoryObjects

![post2](https://github.com/user-attachments/assets/249b2d90-d669-44cf-a625-458d396edc09)

The basic unit in RECA is a `MemoryObject`. Each object contains:

- `text`: the content  
- `timestamp`: creation or modification time  
- `source`: where it came from (file, agent, API, etc)  
- `tags`: optional labels  
- `embedding`: optional vector for semantic search

```
from reca.memory.schema import MemoryObject  
from datetime import datetime  

obj = MemoryObject(  
    text="Bananas are high in potassium.",  
    timestamp=datetime.utcnow(),  
    source="notes.txt",  
    tags=["nutrition"]  
)  
```

---

## 📦 Using Memory

```
from reca.memory.core import Memory  
mem = Memory()  

mem.insert("Elephants have excellent memory.")  
results = mem.search("Which animals have strong memory?")  

print(results[0].text)  
```

---

## 🔍 Hybrid Retrieval

Mix local memory with external retrievers:

```
from reca.retrievers.hybrid import HybridRetriever  
from reca.retrievers.local import LocalRetriever  
from reca.retrievers.wikipedia import WikipediaRetriever  

hybrid = HybridRetriever([  
    LocalRetriever(mem),  
    WikipediaRetriever()  
])  

answers = hybrid.search("What is quantum entanglement?")  
```

---

## 📄 Document Parsing

Split PDFs or markdown into memory-ready chunks:

```
from reca.parsers.markdown import parse_markdown  
chunks = parse_markdown("docs/overview.md")  

for c in chunks:  
    mem.insert(c)  
```

Supported formats include `.md`, `.txt`, `.pdf`, and `.json`.

---

## 🧠 Embedding Models

RECA supports pluggable embedding backends. Use OpenAI or local transformers:

```
from reca.models.embedding import OpenAIEmbedder  
mem = Memory(embedder=OpenAIEmbedder())  
```

You can also add your own model:

```
from reca.models.embedding import CustomEmbedder  

class MyEmbedder(CustomEmbedder):  
    def embed(self, text):  
        return my_custom_embedding(text)  
```

---

## 📡 Web Retrieval

Search web content on-the-fly:

```
from reca.retrievers.web import WebRetriever  

web = WebRetriever()  
results = web.search("Latest news on GPT-5")  
```

RECA includes pluggable retrievers for:

- Wikipedia  
- Arxiv  
- DuckDuckGo  
- Local browser history  
- Custom endpoints

---

## 🧪 Testing

Run tests locally using Poetry:

```
poetry run pytest  
```

---

## 🧩 Extend RECA

To add a custom retriever:

1. Subclass `BaseRetriever`  
2. Implement `.search(query)`  
3. Return a list of `MemoryObject`

To add a memory backend:

1. Subclass `MemoryBase`  
2. Implement `.insert()`, `.search()`, and `.delete()`

---

## 🚀 Use Cases

- Conversational agents with memory  
- Retrieval-augmented generation (RAG)  
- Autonomy stacks and planners  
- Personal assistants that retain facts  
- AI tools that need context over time

---

## 🤝 Contributing

Interested in extending RECA? PRs are welcome!

You can contribute:

- New retrievers  
- New backends (e.g., Redis, Qdrant)  
- Parser support for new formats  
- Improvements to documentation  
- Agent integrations and demos

---

## 📜 License

RECA is released under the MIT License. See `LICENSE` for details.

Developed independently. No affiliation with upstream projects or repositories.
