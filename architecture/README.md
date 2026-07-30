# IPV7 architecture

This directory contains the IPV7 architecture model written with
[LikeC4](https://likec4.dev/).

## Structure

```text
architecture/
├── specification.c4
├── model/
│   ├── systems.c4
│   └── relationships.c4
└── views/
    ├── static.c4
    ├── components.c4
    └── dynamic.c4
```

LikeC4 merges every `.c4` file into one architecture model. Files are separated
by responsibility so the model can grow without turning into one large source
file.

## Initial views

| View | C4 level | Purpose |
| --- | --- | --- |
| `ipv7_context` | Context | Show who uses IPV7 and which external systems it depends on |
| `ipv7_containers` | Container | Show deployable runtimes and persistent infrastructure |
| `mcp_backend_components` | Component | Entry view showing shared security, RAG and governed-action branches |
| `rag_runtime_components` | Component | Explain authentication and the ACL-aware retrieval path |
| `knowledge_base_components` | Component | Explain ingestion, reconciliation and derived-index maintenance |
| `governed_actions_components` | Component | Explain scoped credentials, bound plans and user confirmation |
| `rag_query_flow` | Scenario | Follow one grounded question end to end |
| `governed_action_flow` | Scenario | Follow one confirmed Google Workspace action |
| `synchronization_flow` | Scenario | Follow one source change into the knowledge index |

## C4 levels

The model follows the four C4 levels:

1. **Context** — IPV7, its users and external systems.
2. **Container** — deployable runtimes and persistent infrastructure.
3. **Component** — focused internal views for RAG, the knowledge base and
   governed actions.
4. **Code** — intentionally deferred until implementation modules and their
   boundaries exist. Code diagrams should be generated from or checked against
   the real codebase instead of being invented during architecture design.

Dynamic views are complementary scenarios. They are not a replacement for the
Code level.

## Modelling principles

- C4 containers represent deployable units or data stores, not every logical
  processing step.
- RAG stages are components inside the MCP backend.
- Google Workspace remains an external source of truth.
- The knowledge index is derived and disposable.
- Security decisions and user confirmation stay visible in the governed-actions
  component view.
- Zooming into the MCP Backend first opens a compact entry view where the RAG
  and governed-action branches are both visible. Each branch links to its
  focused component view.
- RAG runtime, knowledge-base maintenance and governed actions use separate
  component views to avoid an overloaded MCP Backend diagram.
- Runtime, synchronization, and action scenarios use separate dynamic views.

## Commands

```bash
npm run architecture:dev
npm run architecture:validate
npm run architecture:build
```
