---
name: graphify
description: "any input (code, docs, papers, images) - knowledge graph - clustered communities - HTML + JSON - audit report"
trigger: /graphify
---

## Overview

graphify transforms folders of files into navigable knowledge graphs with community detection, honest audit trails, and three outputs: interactive HTML, GraphRAG-ready JSON, and GRAPH_REPORT.md.

## Core Commands

```
/graphify                                    # full pipeline on current directory
/graphify <path>                             # pipeline on specific path
/graphify <path> --mode deep                 # thorough extraction, richer edges
/graphify <path> --update                    # incremental re-extraction
/graphify <path> --cluster-only              # rerun clustering only
/graphify <path> --no-viz                    # report + JSON only
/graphify <path> --svg                       # export graph.svg
/graphify <path> --graphml                   # export for Gephi/yEd
/graphify <path> --neo4j                     # generate Cypher file
/graphify <path> --neo4j-push bolt://...     # push to Neo4j directly
/graphify <path> --mcp                       # start MCP stdio server
/graphify <path> --watch                     # auto-rebuild on changes
/graphify add <url>                          # fetch URL, add to corpus
/graphify query "<question>"                 # BFS traversal
/graphify query "<question>" --dfs           # DFS traversal
/graphify path "NodeA" "NodeB"                # shortest path
/graphify explain "NodeName"                 # node explanation
```

## Purpose

graphify builds on Andrej Karpathy's /raw workflow. It delivers three capabilities Claude alone cannot:

1. **Persistent graph** stored in `graphify-out/graph.json` across sessions
2. **Honest audit trail** with EXTRACTED, INFERRED, or AMBIGUOUS tags on every edge
3. **Cross-document discovery** via community detection finding unexpected connections

Use cases: new codebases, reading lists, research corpora, personal /raw folders.

## Key Features

- **Entity & relationship extraction** from code (AST), docs, papers, images
- **Community detection** with cohesion scoring
- **God nodes** (high-degree connectors) and surprising connections
- **Multiple export formats**: Obsidian vault, HTML, JSON, SVG, GraphML, Cypher
- **Incremental updates** for fast re-extraction of changed files
- **Query interface** with BFS/DFS traversal and shortest-path finding
- **MCP server** for agent-to-agent graph access
- **File watching** with auto-rebuild on code changes

## Output Structure

```
graphify-out/
  ├── obsidian/          # Obsidian vault (recommended interface)
  ├── graph.html         # Browser-based visualization
  ├── graph.json         # Persistent graph + communities
  ├── graph.svg          # Embeddable SVG
  ├── graph.graphml      # Gephi/yEd format
  ├── cypher.txt         # Neo4j import
  ├── GRAPH_REPORT.md    # Full audit report
  └── cost.json          # Token usage tracking
```

## Audit Trail System

Every edge carries:
- **Relation type**: calls, implements, references, cites, conceptually_related_to, shares_data_with, semantically_similar_to
- **Confidence tag**: EXTRACTED (explicit), INFERRED (reasonable inference), AMBIGUOUS (uncertain)
- **Confidence score**: 1.0 for EXTRACTED, 0.4–0.9 for INFERRED, 0.1–0.3 for AMBIGUOUS
- **Source location**: file, line number, or null

## Extraction Logic

**Code files** → AST extraction (deterministic, free):
- Functions, classes, imports, dependencies
- No semantic edges re-extracted; AST handles structural links

**Docs/papers/images** → Claude semantic extraction (parallel subagents):
- Named concepts, entities, citations
- Rationale stored as attributes on nodes, not separate nodes
- Vision-based analysis for UI, charts, diagrams, handwritten content
- File type restricted to: code, document, paper, image

**Deep mode** (--mode deep):
- Aggressive INFERRED edges for indirect dependencies and latent couplings
- Uncertain inferences marked AMBIGUOUS

**Semantic similarity**:
- Added when 2+ concepts solve the same problem without structural link
- Marked INFERRED with confidence_score 0.6–0.95
- Cross-cutting only; avoids trivial similarities

**Hyperedges** (sparse):
- Groups of 3+ nodes in shared flow or pattern
- Examples: classes implementing a protocol, auth flow functions, paper section concepts
- Maximum 3 per chunk

## Query Modes

| Mode | Flag | Use Case |
|------|------|----------|
| BFS (default) | _(none)_ | "What is X connected to?" — broad, nearest neighbors first |
| DFS | `--dfs` | "How does X reach Y?" — trace specific path/chain |

## Performance Notes

- **Parallel extraction**: AST runs simultaneously with semantic subagents (Part A + Part B)
- **Caching**: Unchanged files skipped on --update; cache survives across runs
- **Chunk size**: 20–25 files per subagent; images get individual chunks (vision context)
- **Token budgeting**: Default query budget 2000 tokens; use --budget N to override
- **Graph scale**: HTML viz skipped for >5000 nodes; use Obsidian vault instead
- **Token reduction**: Automatic benchmark for corpora >5000 words

## Installation Check

```bash
python3 -c "import graphify" 2>/dev/null || \
  pip install graphifyy -q --break-system-packages
```

## Honesty Rules

- Never invent edges; use AMBIGUOUS if uncertain
- Always show corpus size warnings
- Display token costs in reports
- Never hide cohesion scores
- Warn before HTML viz on large graphs
