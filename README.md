# BI Migration AI Demo

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110%2B-009688?logo=fastapi)
![Claude API](https://img.shields.io/badge/Claude-API-8B5CF6?logo=anthropic)
![Neo4j](https://img.shields.io/badge/Neo4j-Graph-008CC1?logo=neo4j)
![License](https://img.shields.io/badge/License-MIT-green)

An AI-powered BI migration platform that automates the translation of dashboards and reports across Business Intelligence tools. Powered by FastAPI, Claude AI agents, and a Neo4j lineage graph for full impact analysis.

---

## Description

Migrating dashboards across BI platforms (e.g., Tableau to Power BI, Looker to Metabase) is labor-intensive, error-prone, and slow. **BI Migration AI Demo** solves this by combining:

- **Claude API agents** to parse, translate, and rewrite dashboard definitions
- **Neo4j lineage graphs** to map field-level and report-level dependencies
- **FastAPI** as the orchestration layer for async migration workflows

The result: end-to-end automated migration with impact analysis, validation, and audit trails.

---

## Features

- Automated translation of dashboard/report definitions across BI tools
- Field-level lineage tracking with Neo4j graph database
- AI agent orchestration via Claude API for semantic understanding
- Impact analysis: detect what breaks before migration runs
- REST API with async job queue via FastAPI
- Validation reports comparing source vs. translated output
- Modular architecture - plug in new source/target BI connectors

---

## Architecture

```
┌────────────────────────────────────────────────────────┐
│                    FastAPI REST Layer                  │
│          /migrate  /lineage  /validate  /status        │
└───────────────────────┬────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
 ┌─────────────┐ ┌─────────────┐ ┌─────────────────┐
 │ Claude API  │ │   Neo4j     │ │  BI Connectors  │
 │  Agents     │ │  Lineage    │ │ Tableau/Looker/ │
 │ (translate  │ │   Graph     │ │ Power BI / etc. │
 │  validate)  │ │ (deps/impact│ │                 │
 └─────────────┘ └─────────────┘ └─────────────────┘
```

**Flow:**
1. Ingest source BI definition (JSON/YAML/PBIX)
2. Claude agent parses schema and field references
3. Neo4j stores lineage: tables -> fields -> reports -> dashboards
4. Claude agent translates definition to target BI format
5. Validation agent compares source and output semantics
6. Impact analysis flags broken dependencies before deployment

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| API Framework | FastAPI (async) |
| AI / LLM | Anthropic Claude API |
| Graph Database | Neo4j (py2neo / neo4j-driver) |
| Language | Python 3.10+ |
| Data Models | Pydantic v2 |
| Background Jobs | FastAPI BackgroundTasks / Celery |
| Testing | pytest + httpx |

---

## Usage

### Prerequisites

- Python 3.10+
- Neo4j running locally or via AuraDB
- Anthropic API key

### Installation

```bash
git clone https://github.com/Sandyyy123/bi-migration-ai-demo.git
cd bi-migration-ai-demo
pip install -r requirements.txt
```

### Configuration

```bash
cp .env.example .env
# Edit .env:
# ANTHROPIC_API_KEY=your_key
# NEO4J_URI=bolt://localhost:7687
# NEO4J_USER=neo4j
# NEO4J_PASSWORD=your_password
```

### Run the API

```bash
uvicorn app.main:app --reload --port 8000
```

### Migrate a Dashboard

```bash
curl -X POST http://localhost:8000/migrate \
  -H "Content-Type: application/json" \
  -d '{
    "source_tool": "tableau",
    "target_tool": "power_bi",
    "definition_path": "examples/sample_dashboard.json"
  }'
```

### Run Tests

```bash
pytest tests/ -v
```

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

*Built with FastAPI, Claude API, and Neo4j as a portfolio demonstration of AI-driven data engineering automation.*
