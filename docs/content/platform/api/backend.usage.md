---
title: Platform Backend Usage
---

# Platform Backend Usage

## CLI

Run the server in the background:

```bash
python -m backend.cli start
```

Stop the server:

```bash
python -m backend.cli stop
```

Populate the database with a sample graph and execution:

```bash
python -m backend.cli test.populate-db http://0.0.0.0:8000
```

## Programmatic usage

Create a graph and execute it via the REST API:

```python
import requests

server = "http://0.0.0.0:8000"

# Example payload structure; adapt to your Block catalog
graph = {
  "name": "Sample Graph",
  "description": "Echo input",
  "nodes": [
    {"id": "n1", "block_id": "input", "input_default": {}},
    {"id": "n2", "block_id": "echo", "input_default": {"input": "Hello"}}
  ],
  "links": [{"source_id": "n1", "source_name": "output", "sink_id": "n2", "sink_name": "input"}]
}

r = requests.post(f"{server}/graphs", headers={"Content-Type": "application/json"}, json=graph)
r.raise_for_status()
graph_id = r.json()["id"]

# Execute
exec_r = requests.post(f"{server}/graphs/{graph_id}/execute", json={"input": "Hello"})
exec_r.raise_for_status()
```