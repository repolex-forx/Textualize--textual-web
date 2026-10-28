# Repolex Knowledge Graph of Textualize/textual-web

RDF knowledge graph data for [Textualize/textual-web](https://github.com/Textualize/textual-web), parsed by [repolex](https://repolex.ai).

> **Note**: This data is experimental and subject to change without notice.

## How to use this data

The easiest way to get started is to install the [rlex](https://github.com/repolex-ai/rlex) query tool:

```bash
cargo install --git https://github.com/repolex-ai/rlex
```

Verify the install:

```bash
rlex --help
```

**rlex is designed to be used primarily by LLMs in a terminal.** Start up your favorite AI assistant and ask it to use rlex. It handles the SPARQL — you just ask questions in plain English.

To load this repo's data:

```bash
rlex download Textualize/textual-web
```

Consult `rlex --help` for other options, including SPARQL queries, HTTP server, and interactive visualization.

## Data structure

All data is stored as gzip-compressed [N-Quads](https://www.w3.org/TR/n-quads/) (`.nq.gz`), a standard RDF format that can be loaded into any triplestore or graph database.

```
.
├── aggregate
│   ├── ast
│   │   └── 7d6741c9f7869881722d7d8dcf70a286cc270db9
│   │       └── chunk-001.nq.gz
│   └── repolex
│       └── 7d6741c9f7869881722d7d8dcf70a286cc270db9
│           └── chunk-001.nq.gz
├── blob
│   ├── 03510f2d51369f292a204a4d960473379eca7414.nq.gz
│   ├── 076ca022d2f1a6c346dc207c8dc5c2ca8257ba26.nq.gz
│   ├── 2291fc02248b63ffc91914bda2ccd7db134b8f23.nq.gz
│   ├── 3674e03ad51a13dd80634dd071523160291e012e.nq.gz
│   ├── 36baa45c165f4d095c65770e02bb7d361422f683.nq.gz
│   ├── 4545493da3fd1cce3223c247f0ea2fb65cfc21da.nq.gz
│   ├── 46af91b02a433c5f5c6108dee29836ca1da5b9d9.nq.gz
│   ├── 4ee93ddb02a45e2f55d1acf8295d7ed428409c76.nq.gz
│   ├── 538dddc3dc544eb3b644744b6fc90206833b01ea.nq.gz
│   ├── 5495ac05811c26c3baa98458254daa9d3da8bd66.nq.gz
│   ├── 57cde07c7f482c540ec4b8b8d03aa536f381d45b.nq.gz
│   ├── 7441e1cb45d28d2b03d1874eba66b0b76595fd1c.nq.gz
│   ├── 77c0d2393c59261b93be0278b47b250ea4d8293a.nq.gz
│   ├── 79e0f0382d7931c2913486eafd2b8dfec5af0f52.nq.gz
│   ├── 86a13fd7263d4a1be2e50852962e45f9673397db.nq.gz
│   ├── 88715a01f20805d9ef8a723e0b6d5b12ebb9333a.nq.gz
│   ├── 88ac493500d550ff722dc2ea41f7b8303dc594dd.nq.gz
│   ├── 962307dfdda246907be29b3edbc16db8f66ae3e0.nq.gz
│   ├── 978dd2babe01629df6fd26061a984d3cd2c7f5be.nq.gz
│   ├── 9b3f6ea988deda1c03cd5d20dde4b2112c13f042.nq.gz
│   ├── a3aae5e86d9b4b8193fb206eba3bdfd8b7dfd64f.nq.gz
│   ├── a6dbb2204975228068e2623d8394786beadd5f13.nq.gz
│   ├── b27f3f9b62cdf01078f94599f4f8b2d6ec59e6ae.nq.gz
│   ├── b536e294a17224a67e3999b5f713fbf3b274826d.nq.gz
│   ├── c0fe9ac00dd461af8b2964710cb5ad3281a4ae37.nq.gz
│   ├── c74e3a8d3c72b1a2a7b0598240bc46594b07f360.nq.gz
│   ├── d11eb2d5782dbb7df351d10f3e7d87fc19229a1f.nq.gz
│   ├── d511cf9e2919584f944f84c2b900b20df907bbe7.nq.gz
│   ├── d59728a593f6edb79a388603df655820d3ad29c2.nq.gz
│   ├── e69de29bb2d1d6434b8b29ae775ad8c2e48c5391.nq.gz
│   ├── f15619bf5f614d0c496934ffa92a49440b83978b.nq.gz
│   ├── f494185ab9096b3866a085cf5c88a702c2468f43.nq.gz
│   ├── f6ecde269ddaadd15ab1fe806acc8129b5ebbac8.nq.gz
│   ├── f714c8ac2b7618fe9ba9ed7cd3435d87f85efba3.nq.gz
│   └── ffe3d76ba3408195024525cf08437379e5967bee.nq.gz
├── branch
│   └── branch.nq.gz
├── commit
│   └── commit.nq.gz
├── filetree
│   └── 7d6741c9f7869881722d7d8dcf70a286cc270db9.nq.gz
├── issue
│   └── issue.nq.gz
├── pr
│   └── pr.nq.gz
└── tag
    └── tag.nq.gz

13 directories, 43 files
```

| Directory | What it contains |
|-----------|-----------------|
| `blob/` | Per-file AST graphs, content-addressed by git blob SHA. Each file in the source repo gets its own graph. |
| `aggregate/ast/` | Combined AST graph per parsed commit. Merges all blob graphs for a snapshot of the entire codebase at that point. |
| `aggregate/lsp/` | Language Server Protocol enrichment: resolved symbols, definitions, references, and type information. |
| `aggregate/dataflow/` | Interprocedural data flow edges between functions and modules. |
| `aggregate/repolex/` | Combined graph (AST + LSP + dataflow) per commit. |
| `commit/` | Git commit metadata (author, date, message, parent links). |
| `branch/` | Branch metadata. |
| `tag/` | Tag metadata. |
| `filetree/` | File tree snapshots per commit (which files existed and their blob SHAs). |
| `audit/` | Code architecture and graph audit reports per commit. |

## Source repository

[Textualize/textual-web](https://github.com/Textualize/textual-web)

---
*Parsed on 2026-10-28 by [repolex](https://repolex.ai)*
