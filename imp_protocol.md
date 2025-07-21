# Interoperable Memory Protocol (IMP) — Specification v0.1

## Overview
IMP is a local API specification enabling any LLM interface or client to interact with a user-owned memory container. It defines a small set of endpoints to query, store, and inspect persistent memory—stored locally and encrypted by default.

## Core Endpoints

### `GET /memory/query?vector=...`
Returns a ranked list of matching memory entries based on vector similarity (cosine or dot-product).

### `POST /memory/store`
Adds a new signed memory record to the container. Accepts a complete entry in JSON format. Fields `timestamp`, `checksum`, and `signature` are required.

### `GET /memory/entry/:id`
Returns a raw memory entry by internal ID or hash reference.

### `GET /memory/audit`
Runs checksum validation on the container, returns list of any modified or unverifiable entries.

## Memory Entry Schema (v0.1)

```json
{
  "timestamp": "2025-07-21T13:04:00Z",
  "source": "ChatGPT-4o",
  "user": "kevinwellsphd@gmail.com",
  "content": "Let’s change the nature of how AI is right now...",
  "embedding": [0.123, 0.456, ...],
  "checksum": "cd89f134...",
  "signature": "OpenAI:3049a2c...",
  "mod_history": [],
  "tags": ["architecture", "local-ai", "protocol"]
}
