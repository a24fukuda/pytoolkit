# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Architecture

PyToolkit is a collection of Python utility libraries organized as git submodules, each providing specific functionality:

- **metadata**: pyproject.toml metadata parser with PEP 621 compliance and TypedDict-based type safety
- **option**: Rust-inspired Option type for handling optional values (Some/Nothing pattern)
- **result**: Rust-inspired Result type for error handling (Ok/Err pattern)
- **async-worker**: Asynchronous worker implementation
- **template**: Base template for new modules

Each submodule is an independent Python package with its own pyproject.toml, tests, and development workflow.

## Development Commands

### Dependency Management
All projects use `uv` for dependency management and Python 3.13+.

```bash
# Install dependencies in a submodule
cd <submodule>
uv sync

# Install development dependencies
uv sync --group dev
```

### Testing and Quality Assurance
Each submodule follows the same testing and quality patterns:

```bash
# Run tests
uv run pytest

# Type checking
uv run pyright

# Linting
uv run ruff check

# Fix linting issues
uv run ruff check --fix

# Code formatting
uv run ruff format
```

### Building
```bash
# Build package
uv build
```

## Versioning System

The project uses a date-based versioning scheme: `vYYYY.MM.DD.XX`
- `v`: Fixed prefix
- `YYYY`: Year (4 digits)
- `MM`: Month (2 digits, 01-12)
- `DD`: Day (2 digits, 01-31)
- `XX`: Same-day update number (2 digits, starting from 01)

### Submodule Version Update Workflow

When updating versions across submodules:

1. Update `pyproject.toml` version in each submodule
2. For each submodule:
   ```bash
   cd <submodule>
   uv sync
   git add .
   git commit -m "バージョンを更新"
   git tag v<new-version>
   git push origin main
   git push origin v<new-version>
   ```
3. Return to main project and commit submodule updates

## Submodule Management

### Key Commands
```bash
# Check submodule status
git submodule status

# Update all submodules
git submodule update --remote

# Initialize submodules when cloning
git submodule update --init --recursive
```

### Current Submodules
- async-worker: Asynchronous worker utilities
- metadata: pyproject.toml parsing with strict typing
- option: Optional value handling with functional programming support
- result: Error handling with explicit success/failure types
- template: Base template for new packages

## Code Patterns

The functional programming modules (option/result) follow these patterns:
- Abstract base classes prevent direct instantiation
- Generic types with TypeVar for type safety
- Functional methods: `map()`, `and_then()`, `unwrap()`, `unwrap_or()`
- Immutable designs using frozen dataclasses where applicable

The metadata parser uses:
- TypedDict for strict type checking
- ReadOnly fields for immutability
- PEP 621 compliance for pyproject.toml structure

## Language and Documentation

- All READMEs are in Japanese
- Code comments and docstrings are in Japanese
- Commit messages are in Japanese with specific format including Claude Code attribution