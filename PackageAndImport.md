# 📘 Notes: Python Package Names vs. Import Names

![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)
![PyPI](https://img.shields.io/pypi/v/python-dotenv?label=PyPI%20example)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

---

## 1. Key Difference
- **PyPI/Distribution name** → what you install with `pip install ...` or `uv add ...`  
- **Import name** → the actual top-level module/folder you `import` in Python  

👉 They don’t have to match. Example:  
- Install: `pip install python-dotenv`  
- Import: `from dotenv import load_dotenv`

---

## 2. Why They Differ
- Author chooses **project name** in `pyproject.toml` (distribution).  
- Author chooses **package folder name** inside `src/` (import).  
- Examples:  
  - `python-dotenv` → `import dotenv`  
  - `beautifulsoup4` → `import bs4`  
  - `Pillow` → `import PIL`

---

## 3. How to Create a Similar Package

### Project Structure
```
my-project/
├─ pyproject.toml        # [project].name = "python-helloenv"
├─ src/
│  └─ helloenv/          # import name = helloenv
│     ├─ __init__.py
│     └─ core.py
```

### pyproject.toml
```toml
[project]
name = "python-helloenv"   # install with pip/uv
version = "0.1.0"
```

### Import Example
```python
from helloenv import load_env
```

---

## 4. Installing Locally

**With uv**
```bash
uv pip install -e .
uv run python example.py
```

**With pip**
```bash
pip install -e .
python example.py
```

---

## 5. Building & Publishing

- Build distribution:
  ```bash
  uv build
  ```
  or
  ```bash
  python -m build
  ```

- Publish:
  ```bash
  uv publish
  ```
  or
  ```bash
  twine upload dist/*
  ```

---

## 6. Quick Checklist ✅
- `pyproject.toml` → sets distribution name  
- `src/<folder>` → sets import name  
- Install name can differ from import name  
- Examples:  
  - `python-dotenv` vs. `dotenv`  
  - `Pillow` vs. `PIL`  
  - `beautifulsoup4` vs. `bs4`
