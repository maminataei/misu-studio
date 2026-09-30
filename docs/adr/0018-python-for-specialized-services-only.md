# ADR-0018: Python for Specialized Services Only

**Status:** Accepted  
**Date:** 2026-09-30

## Context

Python has strong AI, media, and automation ecosystems. The canonical editor
logic, however, must execute in browsers and servers with identical behavior.
A Python control plane would duplicate or remotely call critical TypeScript
map logic.

## Decision

Keep the beta editor, core, API, worker, CLI, and SDKs TypeScript-first. Python
MAY be introduced later behind explicit service contracts for AI inference,
specialized media processing, or import automation.

## Consequences

Python services cannot become schema authorities or bypass typed commands.
Their inputs and outputs use versioned contracts, and failure degrades only the
optional capability they serve.

## Rejected alternatives

- FastAPI/Pydantic as the primary control plane.
- Duplicated Python and TypeScript command engines.
- Python executed in the browser through Pyodide.

## References

- [FastAPI OpenAPI and JSON Schema](https://fastapi.tiangolo.com/tutorial/first-steps/)
- [SQLAlchemy asyncio](https://docs.sqlalchemy.org/en/20/orm/extensions/asyncio.html)
