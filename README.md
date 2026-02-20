# oTree project template

A modern, minimal [oTree](https://www.otree.org/) project template with modern Python tooling via [uv](https://docs.astral.sh/uv/).

## Prerequisites

Install `uv` (if you haven't already):

- **macOS / Linux:**
  ```sh
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- **Windows:**
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```

## Getting started

1. **Get the template** — either clone the repository:
   ```sh
   git clone https://github.com/mrpg/otree-uv my_project
   cd my_project
   ```
   or download and unzip it ([releases](https://github.com/mrpg/otree-uv/releases)), then open a terminal in the resulting folder.

2. **Install dependencies:**
   ```sh
   uv sync
   ```
   This creates a virtual environment and installs oTree and all dev tools automatically. No manual `pip install` or `venv` setup needed.

3. **Run the development server:**
   ```sh
   uv run otree devserver
   ```
   Then open [http://localhost:8000](http://localhost:8000) in your browser.

## Creating apps

Create a new oTree app with:
```sh
uv run otree startapp my_app
```

Then register it in `settings.py` under `SESSION_CONFIGS`.

## Code quality

This template includes [black](https://black.readthedocs.io/), [isort](https://pycqa.github.io/isort/), and [ruff](https://docs.astral.sh/ruff/) for formatting and linting, wired up via [pre-commit](https://pre-commit.com/).

Set up the git hooks once after cloning:
```sh
uv run pre-commit install
```

After that, formatting and linting run automatically on every commit. To run them manually at any time:
```sh
uv run pre-commit run --all-files
```

## Deployment on Heroku

The template is ready for Heroku out of the box. Heroku detects `uv.lock` and uses uv to install dependencies, and reads the Python version from `.python-version`.

### First-time setup

```sh
heroku create my-otree-app
heroku addons:create heroku-postgresql
```

### Environment variables

```sh
heroku config:set OTREE_ADMIN_PASSWORD=choose_a_password
heroku config:set OTREE_PRODUCTION=1
```

`DATABASE_URL` is set automatically by the Heroku Postgres addon above.

### Deploy

```sh
git push heroku main
```

The `Procfile` runs oTree's production server as a single `web` dyno — no Redis or worker dyno needed in oTree 5.
