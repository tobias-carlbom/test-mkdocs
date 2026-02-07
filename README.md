**Folder structure:**

```
test/
├── .github/
│   └── workflows/
│       └── docs.yml
├── docs/
│   ├── index.md
│   ├── project1/
│   │   └── docs.md
│   └── project2/
│       └── docs.md
├── project1/
│   └── program.py
├── project2/
│   └── program.js
├── README.md
└── mkdocs.yml
```

---

**`mkdocs.yml`**

```yaml
site_name: Test Documentation
theme:
  name: material
markdown_extensions:
  - pymdownx.highlight
  - pymdownx.superfences
  - pymdownx.snippets:
      base_path: .
nav:
  - Home: index.md
  - Project1: project1/docs.md
  - Project2: project2/docs.md
```

---

**`docs/index.md`**

```markdown
# Test Documentation

- [Project1](project1/docs.md)
- [Project2](project2/docs.md)
```

---

**`docs/project1/docs.md`**

````markdown
# Project1 - program.py

## method_one

Does the first thing.

```python
--8<-- "project1/program.py:method_one"
```

## method_two

Does the second thing.

```python
--8<-- "project1/program.py:method_two"
```

## method_three

Does the third thing.

```python
--8<-- "project1/program.py:method_three"
```
````

---

**`docs/project2/docs.md`**

````markdown
# Project2 - program.js

## methodOne

Does the first thing.

```javascript
--8<-- "project2/program.js:methodOne"
```

## methodTwo

Does the second thing.

```javascript
--8<-- "project2/program.js:methodTwo"
```

## methodThree

Does the third thing.

```javascript
--8<-- "project2/program.js:methodThree"
```
````

---

**`project1/program.py`**

```python
# --8<-- [start:method_one]
def method_one():
    return "one"
# --8<-- [end:method_one]

# --8<-- [start:method_two]
def method_two():
    return "two"
# --8<-- [end:method_two]

# --8<-- [start:method_three]
def method_three():
    return "three"
# --8<-- [end:method_three]
```

---

**`project2/program.js`**

```javascript
// --8<-- [start:methodOne]
function methodOne() {
    return "one";
}
// --8<-- [end:methodOne]

// --8<-- [start:methodTwo]
function methodTwo() {
    return "two";
}
// --8<-- [end:methodTwo]

// --8<-- [start:methodThree]
function methodThree() {
    return "three";
}
// --8<-- [end:methodThree]
```

---

**`.github/workflows/docs.yml`**

```yaml
name: Deploy Docs
on:
  push:
    branches: [main]
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - run: pip install mkdocs mkdocs-material pymdown-extensions
      - run: mkdocs gh-deploy --force
```
