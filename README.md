# AG2 Documentation in Chinese

https://ag2.cn

AG2 documentation is based on the sphinx documentation system and uses the myst-parser to render markdown files. It uses the [pydata-sphinx-theme](https://pydata-sphinx-theme.readthedocs.io/en/latest/) to style the documentation.

### Prerequisites

You can install them by running the following command from the root of the python repository:

```bash
uv sync --all-extras
source .venv/bin/activate
```

- `uv` is a package manager that assists in creating the necessary environment and installing packages to run AutoGen.
- [Install `uv`](https://docs.astral.sh/uv/getting-started/installation/).
- `uv sync --all-extras` will create a `.venv` directory at the current level and install packages from the current directory along with any other dependencies. The `all-extras` flag adds optional dependencies.
- `source .venv/bin/activate` activates the virtual environment.

## Building Docs

To build the documentation, run the following command from the root of the python repository:

```bash
poe --directory . docs-build
```

To serve the documentation locally, run the following command from the root of the python repository:

```bash
poe --directory . docs-serve
```

[!NOTE]
Sphinx will only rebuild files that have changed since the last build. If you want to force a full rebuild, you can delete the `./docs/build` directory before running the `docs-build` command.

## Versioning the Documentation

The current theme - [pydata-sphinx-theme](https://pydata-sphinx-theme.readthedocs.io/en/latest/) - supports [switching between versions](https://pydata-sphinx-theme.readthedocs.io/en/stable/user_guide/version-dropdown.html) of the documentation.

To version the documentation, you need to create a new version of the documentation by copying the existing documentation to a new directory with the version number. 

### Version

git checkout 
