# Graph RAG — Schema-Only Q&A System with Neo4j

**Overview**  
Graph RAG lets users query a **database schema** stored in Neo4j using natural language (Arabic or English). The system transforms user queries into **safe Cypher** commands, executes them on the schema graph (no row data), and returns clear, context-aware answers with minimal setup.

---

## ⭐ Highlights
- **Semantic UI Schema View**: Schema represented as `:Table` nodes in Neo4j with columns stored in `t.columns` (JSON).  
- **Automatic FK Detection**: Deduces and creates `:FK` relationships from column names/descriptions.  
- **FAISS-based Semantic Indexing**: Enables similarity search across table and column descriptions using embeddings.  
- **LLM-Driven Query Translation**: Uses Groq LLM to convert natural language questions into schema-only Cypher, with strict validation to prevent write/delete operations.  
- **Stepwise Orchestration**: Managed end-to-end via LangGraph—intent detection → Cypher generation → execution → result processing → answer generation.  
- **Conversational Memory**: Remembers recent queries (last 3) and summarizes previous interactions to support follow-up questions.

---

##  Table of Contents
1. [Getting Started](#getting-started)  
2. [Prerequisites](#prerequisites)  
3. [Installation](#installation)  
4. [Configuration](#configuration)  
5. [Usage Examples](#usage-examples)  
6. [Project Structure](#project-structure)  
7. [Best Practices](#best-practices)  
8. [Contributing](#contributing)  
9. [License](#license)

---

## Getting Started

1. **Create `schema.json`** — describe your database schema:
   ```json
   {
     "tables": {
       "users": {
         "columns": [
           { "name": "id", "data_type": "integer", "description": "Primary Key" },
           { "name": "email", "data_type": "text", "description": "User email" }
         ]
       }
     }
   }
