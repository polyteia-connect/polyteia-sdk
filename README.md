# 📦 gOS API TOOLKIT

A lightweight Python SDK for interacting with the gOS API — designed for seamless data integration, resource management, and automation within the Polyteia platform or similar data environments.

---

## 🚀 Features

- 🔐 Organization, workspace, and user management
- 📊 Datasets creation, upload, metadata updates
- 📈 Insights management
- 🏷️ Tagging system for resources
- 📁 File upload/download
- 🔁 Centralized error handling with
- ⚙️ Extensible for additional API commands

---

## 📦 Installation

### Install via pip :

```bash
pip install git+https://github.com/polyteia-de/gOS-api-toolkit.git
```

### Install locally for development:

```bash
git clone https://github.com/polyteia-de/gOS-api-toolkit.git
cd gOS-api-toolkit
pip install -e .
```

---

## 📁 Project Structure

```
gos-api-toolkit/
│
├── gos_api_sdk/              # SDK source package
│   ├── __init__.py
│   └── api_utils.py          # Core API functions
│
├── requirements.txt          # Runtime dependencies
├── dev-requirements.txt      # Linting, testing, dev tools
├── setup.py                  # Package metadata/setup
├── pyproject.toml            # Build backend & versioning
├── .gitignore                # Local tests (excluded from Git)
```

---

## 🔧 Requirements

### ⚙️ Runtime Dependencies

The SDK depends on a few core libraries to handle HTTP requests and data serialization:

* `requests` – for communicating with the API
* `pyarrow` – for working with Arrow and Parquet file formats
* `polars` – for efficient DataFrame processing

These dependencies are **automatically installed** when the SDK is installed via pip:

```bash
pip install git+https://github.com/polyteia-de/gOS-api-toolkit.git
```

If needed (e.g. in a minimal environment or container), you can manually install runtime dependencies with:

```bash
pip install -r requirements.txt
```

### 🛠 Install Development Dependencies

To contribute to the SDK or run tests, you’ll need additional tools.

Install them using:

```bash
pip install -r dev-requirements.txt
```

This includes:

* `bump-my-version` – version bumping for releases
* More tools will be added later

These tools ensure the SDK maintains a clean, consistent, and reliable codebase.

---

## 🧪 Usage Example

```python
from gos_api_sdk import api_utils as api

# Authenticate
access_token = api.get_org_access_token(org_id="org_xyz", PAK="your_pak")

# Create a dataset
ds_id = api.create_dataset(
    solution_id="sol_123",
    name="Haushaltsdaten",
    description="Finanzdaten der Kommune",
    source="demo_source",
    slug="haushalt-daten",
    access_token=access_token
)

# Upload data
upload_token = api.generate_upload_token(
    ds_id,
    content_type="application/vnd.apache.parquet",
    access_token=access_token
)
api.upload_file(upload_token, df, access_token=access_token)
```

---

## ⚠️ Error Handling

All functions use `handle_api_response()` for:

* Safe JSON parsing
* Status code validation
* Nested key validation (e.g. `data.token`)
* Descriptive exception messages

### Example Error

```bash
[Generate upload token] ❌ Missing key 'data.token': Validation failed (id must be a valid ID)
```

---

## 🧼 Linting & Code Style

```bash
black .
isort .
flake8 .
mypy gos_api_sdk/
```

---

## 🔖 Versioning

Managed via `bump-my-version`:

```bash
bump-my-version bump patch  # or minor / major
```

---

## ✅ Testing

Tests can be placed in `gos_api_sdk/testing/`:

```bash
pytest gos_api_sdk/testing/
```

> Note: this folder is excluded via `.gitignore`.

---

## 🛠 Roadmap

* OAuth flow support
* Async client (`httpx`)
* CLI wrapper
* pdoc/mkdocs auto-docs

---

## 🤝 Contributing

Pull requests are welcome! Please follow existing patterns and run formatters before submitting:

```bash
black .
flake8 .
```

---

## 📝 License

MIT License (or specify your internal license here)

---

```

---

This file is **fully plug-and-play** — just copy it to your project root as `README.md`. Let me know if you’d like a separate CONTRIBUTING.md, `docs/` setup, or `mkdocs.yml` scaffold.
```
