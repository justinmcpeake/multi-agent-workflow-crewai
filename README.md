# Multi-Agent Workflow — CrewAI

A multi-agent orchestration pattern using CrewAI. Specialist agents handle discrete tasks; a verification agent audits outputs before they reach the human review stage.

## The Pattern

Most AI outputs benefit from a second pass. This architecture separates task execution from quality control:

- **Research Agent** — retrieves and synthesises relevant context
- **Draft Agent** — produces the initial output
- **Verify Agent** — checks for hallucination, gaps, and factual consistency
- **Review Gate** — presents verified output to human; human approves or rejects

No output bypasses the Review Gate. Human-in-the-loop is not optional.

## Why This Matters

Single-agent pipelines fail silently. When one model both produces and evaluates its own output, errors compound. Separating roles — and adding an independent verification step — catches the categories of failure that matter most in professional environments.

## Stack

- **Framework:** CrewAI (Python)
- **LLM:** Ollama (Llama 3) — local; or Groq API (dev/iteration)
- **Abstraction:** LiteLLM (hot-swap between Ollama and Groq without code changes)
- **Language:** Python 3.11+

## Agent Architecture

```
Task input
    ↓
Research Agent → context package
    ↓
Draft Agent → initial output
    ↓
Verify Agent → consistency check + confidence score
    ↓
Human Review Gate → approve / reject / revise
    ↓
Final output (draft only — no autonomous send)
```

## Status

**Pattern documented.** Implementation is running in Fortress development environment. Cleaned standalone version will be published here.

## Author

Justin McPeake — [LinkedIn](https://www.linkedin.com/in/justin-mcpeake-85492140b)
Part of the [Fortress](https://github.com/justinmcpeake/fortress-architecture) private AI platform.
