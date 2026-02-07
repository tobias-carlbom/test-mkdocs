# test-mkdocs


**Your repo structure when done:**

```
test/
├── .github/
│   └── workflows/
│       └── docs.yml
├── docs/
│   ├── index.md
│   ├── program-py.md
│   └── program-js.md
├── mkdocs.yml
├── Program.py
└── program.js
```

---

**Step 1: Create `Program.py`**

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

**Step 2: Create `program.js`**

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

**Step 3: Create `mkdocs.yml`**

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
  - Program.py: program-py.md
  - program.js: program-js.md
```

---

**Step 4: Create `docs/index.md`**

```markdown
# Test Documentation

- [Program.py](program-py.md)
- [program.js](program-js.md)
```

---

**Step 5: Create `docs/program-py.md`**

````markdown
# Program.py

## method_one

Does the first thing.

```python
--8<-- "Program.py:method_one"
```

## method_two

Does the second thing.

```python
--8<-- "Program.py:method_two"
```

## method_three

Does the third thing.

```python
--8<-- "Program.py:method_three"
```
````

---

**Step 6: Create `docs/program-js.md`**

````markdown
# program.js

## methodOne

Does the first thing.

```javascript
--8<-- "program.js:methodOne"
```

## methodTwo

Does the second thing.

```javascript
--8<-- "program.js:methodTwo"
```

## methodThree

Does the third thing.

```javascript
--8<-- "program.js:methodThree"
```
````

---

**Step 7: Create `.github/workflows/docs.yml`**

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

---

**Step 8: Enable GitHub Pages**

1. Push all files to your `main` branch
2. Wait for the Action to run (check Actions tab)
3. Go to Settings → Pages
4. Under "Source" select branch `gh-pages`, folder `/ (root)`
5. Save

Your docs will be live at: `https://yourusername.github.io/test/`

---

**Step 9: Making changes**

**To update code:**

1. Edit `Program.py` or `program.js` directly in GitHub
2. Keep the `--8<-- [start:name]` and `--8<-- [end:name]` markers around each method
3. Commit
4. The Action runs automatically and docs update with the new code

**To update method descriptions:**

1. Edit `docs/program-py.md` or `docs/program-js.md`
2. Change the text above each code block
3. Commit
4. Docs rebuild automatically

**To add a new method:**

1. Add the method to your source file with markers:
```python
# --8<-- [start:method_four]
def method_four():
    return "four"
# --8<-- [end:method_four]
```

2. Add a new section in the corresponding docs file:
````markdown
## method_four

Description of method_four.

```python
--8<-- "Program.py:method_four"
```
````

3. Commit both files

**To add a new file:**

1. Create the new source file with markers (e.g. `utils.py`)
2. Create `docs/utils.md` with sections for each method
3. Add to `mkdocs.yml` nav:
```yaml
nav:
  - Home: index.md
  - Program.py: program-py.md
  - program.js: program-js.md
  - utils.py: utils.md
```
4. Commit all files

---

**Troubleshooting:**

If docs don't update, go to the Actions tab in your repo to see if the build failed and why.
