# Repository Guidelines

## Project Structure & Module Organization
`src/open_deep_research/` holds the current LangGraph workflows, tools, and configuration objects; group new nodes beside related modules. Keep `src/legacy/` untouched unless backporting fixes. Prototype in `examples/`. Benchmarks and regression data live under `tests/`, especially `tests/expt_results/`. Shared defaults for LangGraph Studio run through `langgraph.json`.

## Build, Test, and Development Commands
Create an environment with `uv venv` and install dependencies via `uv sync`. Use `uv run pytest` for unit and integration suites, `uv run ruff check .` for linting, and `uv run mypy src` when type coverage matters. Launch LangGraph Studio with `uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev --allow-blocking`.

## Coding Style & Naming Conventions
Target Python ≥3.10, four-space indentation, and descriptive typing. Modules stay lowercase_with_underscores; classes use `CapWords`; async nodes and tool functions prefer verb-based snake_case. Keep docstrings concise in Google style (Ruff `D401`), run `ruff --fix` for import order, and centralize tunable constants in `configuration.py`.

## Testing Guidelines
Keep runnable tests under `tests/` with `test_*.py` naming. Exercise new graph paths via `pytest`, and mirror `tests/run_evaluate.py` when adding evaluation scripts. If you adjust retrieval or summarization logic, refresh the JSONL fixtures in `tests/expt_results/` to surface regressions. Note the exact `uv run ...` commands in PR descriptions.

## Commit & Pull Request Guidelines
Craft commits with imperative summaries (`Add`, `Fix`, `Update`) and optional prefixes (`fix:`, `feat:`) consistent with existing history. Reference related issues via `(#123)` when available. Pull requests should include: a concise change overview, configuration or `.env` tweaks, test evidence (commands + results), and LangGraph Studio screenshots if behavior changed.

## Configuration & Secrets
Copy `.env.example` to `.env`, supply model and search keys, and never commit populated secrets. Favor provider aliases exposed in `configuration.py`, documenting any new variables there and in the README. Activate the UV virtualenv (`source .venv/bin/activate`) before running commands to avoid system package bleed-through.

## Architecture & Research Workflow
The blog outlines a three-phase loop—Scope → Research → Report. Preserve the scoping chat-to-brief translator so the research brief stays the source of truth throughout the run. Supervisors should only parallelize topics that benefit from isolated context windows, keeping report writing single-threaded to avoid disjoint sections. Ensure sub-agents prune tool outputs, cite sources, and return compressed findings; this context engineering prevents token bloat and keeps downstream LLM calls affordable while maintaining quality.
