# uv + Ruff + prek Copier template

A small Copier template for bootstrapping Python projects with:

- **uv** for Python, dependency, environment, and lockfile management
- **Ruff** for linting and formatting
- **prek** for Git hooks
- **pytest** for tests

## One-time template setup

From PowerShell, initialize this directory as a versioned template:

```powershell
Set-Location path\to\python-uv-ruff-prek-template
.\initialize-template.ps1
```

The script initializes Git, creates an initial commit, and tags it as `v0.1.0`.

## Create a project

From the directory where you want the project created:

```powershell
uvx copier copy --trust path\to\python-uv-ruff-prek-template my-project
```

`--trust` is required because the template runs post-generation tasks. Those tasks:

1. initialize the generated Git repository;
2. run `uv sync`;
3. install the prek Git hook;
4. run all hooks once.

## Use the generated project

```powershell
Set-Location my-project
uv run ruff check .
uv run ruff format --check .
uv run pytest
uv run prek run --all-files
```

## Update a generated project

After changing this template, commit the change and create a newer tag, for example:

```powershell
git add .
git commit -m "Update project template"
git tag v0.2.0
```

Then, from a clean generated project:

```powershell
uvx copier update --trust
```
