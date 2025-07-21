# Memory Agent Outline

## Purpose
The agent is a lightweight background service that manages local AI memory, handling reads, writes, integrity checks, and secure API communication between local apps and the user-owned container.

## Architecture

- Language: Python or Rust
- Database: SQLite for core store
- Vector Index: ChromaDB or FAISS for embedding retrieval
- Crypto: libsodium or PyNaCl for signing and encryption

## Agent Responsibilities

-  `store(entry)`: Validate, hash, sign, and write new memory
-  `query(vector)`: Return nearest neighbors by vector similarity
-  `audit()`: Verify integrity of all entries
-  `encrypt()` and `decrypt()`: Wrap entries for backup or export

## API Surface

- `POST /memory/store`
- `GET /memory/query`
- `GET /memory/audit`
- `GET /memory/entry/:id`

## Startup Behavior
- Loads keys from `~/.aimemory/keys/`
- Initializes DB and vector index if missing
- Starts local server on port 11773

## Security
- All records signed
- Optional auto-encryption for rest state
- Zero cloud syncing by default
