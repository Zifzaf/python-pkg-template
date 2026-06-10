# python-pkg-template

A lightweight copier template for Python packages. Generates the same toolchain used in this project: `uv`, `pyproject.toml`, a strict pre-commit stack, pytest, and GitHub Actions CI.

## Prerequisites

```bash
pip install copier
```

You also need [uv](https://docs.astral.sh/uv/getting-started/installation/) installed for managing the generated project.

## Generate a new project

```bash
copier copy /path/to/python-pkg-template /path/to/new-project
```

Or directly from GitHub (once the template repo is pushed):

```bash
copier copy gh:your-org/python-pkg-template ./new-project
```

Copier will ask:

| Question | Default | Notes |
|---|---|---|
| `project_name` | — | Display name, hyphens OK (e.g. `my-package`) |
| `package_name` | derived | Python import name, underscores (e.g. `my_package`) |
| `description` | — | One-line description, goes into `pyproject.toml` and `__init__.py` |
| `author_name` | — | |
| `author_email` | — | |
| `python_version` | `3.12` | |
| `line_length` | `120` | Applied to black, isort, and flake8 |

## What gets generated

```
new-project/
├── my_package/
│   └── __init__.py
├── tests/
│   ├── __init__.py
│   └── conftest.py
├── .github/
│   └── workflows/
│       └── pre-commit.yml
├── .gitignore
├── .pre-commit-config.yaml
├── .python-version
└── pyproject.toml
```

## Bootstrap the generated project

```bash
cd new-project
git init
uv sync
uv run pre-commit install --hook-type commit-msg
uv run pre-commit install
```

Run the test suite:

```bash
uv run pytest
```

## Update an existing project

When the template itself is updated, pull in the changes with:

```bash
copier update
```

Copier uses the `.copier-answers.yml` file (auto-generated at copy time) to replay your answers. Review the diff and resolve any conflicts before committing.

## Pre-commit hooks included

| Hook | Purpose |
|---|---|
| commitizen | Enforces conventional commit messages |
| prettier | Formats TOML and other non-Python files |
| isort | Sorts imports |
| black | Formats Python code |
| flake8 | Lints Python code |
| mypy | Static type checking |
| add-trailing-comma | Normalises trailing commas |
| autoflake | Removes unused imports and variables |
| pre-commit-hooks | JSON/XML/YAML checks, EOF fixer, trailing whitespace |
