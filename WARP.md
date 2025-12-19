# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository Purpose

This is a **Copier template** for bootstrapping Python projects with modern tooling (`uv`, Ruff, pre-commit). It is NOT a Python project itself—it's a template that generates new Python projects.

## Architecture

### Template Structure
- **Root level**: Contains the Copier configuration (`copier.yaml`), README, and license
- **`template/` directory**: Contains all files that will be copied to generated projects
  - Pre-configured dotfiles: `.ruff.toml`, `.pre-commit-config.yaml`, `.editorconfig`, `.gitignore`
  - VS Code workspace settings in `.vscode/`

### Copier Configuration (`copier.yaml`)
The template is driven by `copier.yaml` which defines:
- **User prompts**: `project_name`, `project_description`, `init_git_repo`, `init_uv_environment`, etc.
- **Conditional workflows**: Different setup paths depending on whether UV is used
- **Post-generation tasks** (`_tasks`): Automated setup including:
  - Installing UV via `proto` (version pinned to 0.9.15)
  - Initializing UV projects with `uv init`
  - Installing tools (Ruff, pre-commit) via `uv tool install` or `pipx`
  - Setting up git hooks and running initial pre-commit checks

## Common Commands

### Testing the Template
Generate a test project locally:
```bash
copier copy . /tmp/test-project
```

Update an existing project generated from this template:
```bash
copier update /path/to/generated-project
```

### Modifying the Template

When changing template files in `template/`:
```bash
# Test changes by generating a new project
copier copy . /tmp/test-output

# Verify the generated project structure
ls -la /tmp/test-output
```

When modifying `copier.yaml`:
- User prompts go in the top section (before `_tasks`)
- Conditional logic uses Jinja2 syntax: `{% if condition %}...{% endif %}`
- Task commands use `when:` clauses to control execution

### Validation

After template changes, validate by generating a project and checking:
```bash
# Generate project
copier copy . /tmp/validation-test

# Verify generated files exist
cd /tmp/validation-test
ls -la

# Check if UV environment was created (if selected)
ls .venv

# Verify pre-commit is functional
pre-commit run --all-files
```

## Template Configuration Standards

### Ruff Configuration (`.ruff.toml`)
- Line length: 88 characters
- Selected rules: F (Pyflakes), E (pycodestyle errors), I (isort), T (flake8-type-checking), ANN (annotations)
- Format style: double quotes, space indentation

### Pre-commit Hooks (`.pre-commit-config.yaml`)
- Ruff for linting and formatting (v0.14.10)
- Standard hooks: trailing whitespace, EOF fixer, YAML checker, large file checker
- Prettier for YAML/JSON formatting (v2.2.1)

### EditorConfig (`.editorconfig`)
- Default: UTF-8, LF line endings, 4-space indentation
- YAML/JSON: 2-space indentation
- Markdown: preserve trailing whitespace

## Key Implementation Details

### UV vs Non-UV Paths
The template supports two modes:
1. **With UV** (`init_uv_environment: true`):
   - Uses `uv init` to create project structure
   - Tools installed via `uv tool install`
   - Creates `.venv` automatically

2. **Without UV** (`init_uv_environment: false`):
   - Manual git initialization
   - Tools installed via `pipx`
   - User manages their own virtual environment

### Proto Integration
The template pins UV version using `proto pin uv 0.9.15`. If modifying UV version requirements, update this line in `copier.yaml` tasks.

### Generated Project Types
When UV is enabled, three project types are supported:
- **app**: Application with standard structure
- **lib**: Library/package for distribution
- **script**: Simple script-based project

The `uv_use_package` flag determines whether to scaffold as a full Python package.

## Modifying Generated Projects

When adding new files to `template/`:
- Static files are copied as-is
- Jinja2 templating is available using `{{variable}}` syntax
- Conditional file inclusion can be configured in `copier.yaml` using `_exclude` or file suffixes

When adding new dependencies or tools to generated projects:
- Add installation commands to `_tasks` in `copier.yaml`
- Use conditional `when:` clauses to respect user choices
- Maintain both UV and non-UV code paths

## Language and Comments
The README is in Russian. When making changes that affect user-facing documentation, maintain Russian language for consistency with existing content.
