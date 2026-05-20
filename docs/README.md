# Developer Documentation

Welcome to the Agent Finder documentation codebase. This guide outlines how to get started, run the development server locally, and publish documentation updates.

---

## 1. Getting Started

To develop the docs, you need Python 3.x and a Git client.

1.  **Clone the Repository**:
    ```bash
    git clone <repo_url>
    cd agent-finder
    ```

2.  **Create a Virtual Environment**:
    We use a local Python virtual environment to isolate documentation dependencies.
    ```bash
    python3 -m venv .venv
    ```

3.  **Activate the Virtual Environment** (Optional):
    *   On Linux/macOS: `source .venv/bin/activate`
    *   On Windows: `.venv\Scripts\activate`

4.  **Install Dependencies**:
    Install the required documentation packages (such as `mkdocs` and the `mkdocs-material` theme):
    ```bash
    .venv/bin/pip install -r requirements-docs.txt
    ```

---

## 2. Local Development

We use a live-reloading development server to preview modifications instantly in the browser.

Start the local server:
```bash
.venv/bin/mkdocs serve
```

*   Once running, open **[http://127.0.0.1:8000/](http://127.0.0.1:8000/)** in your browser.
*   Any change made to markdown files inside the `docs/` directory will trigger an automatic rebuild and refresh your browser tab.

---

## 3. Deployment

### Manual Deployment (Current)

If you have push permissions to the main repository, you can build and deploy the live site directly using:

```bash
.venv/bin/mkdocs gh-deploy
```

This command builds the static assets, commits them to a local `gh-pages` branch, and pushes it to GitHub.

---

### Automated Deployment (Planned GitHub Action)

We are transitioning deployment to an automated CI/CD pipeline using **GitHub Actions** (modeled directly on the `adk-docs` pipeline). Once active, pushing or merging to the `main` branch will automatically trigger a build and deploy.

To activate this automation, create a file at `.github/workflows/publish-docs.yaml` with this optimized definition:

```yaml
name: Publish Docs

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          
      - uses: actions/setup-python@v6
        with:
          python-version: 3.x
          
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
      
      - name: Cache Material Theme Assets
        uses: actions/cache@v5
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
            
      - name: Install Dependencies
        run: pip install -r requirements-docs.txt
        
      - name: Deploy to GitHub Pages
        run: mkdocs gh-deploy --force
```

---

## 4. Writing Guidelines & Style
When authoring or updating documentation, we strictly adhere to an **anti-hype, high-density, clinical tone**:
*   **Clear and Concise**: Explain the technical parameters directly. Never use marketing superlatives (*"revolutionary"*, *"groundbreaking"*).
*   **Grounded Examples**: Always use valid code blocks with domain-anchored URNs and standard media types (`application/mcp-server+json`).
*   Refer to the `.scratchpad/style_guide_and_spec_alignment.md` handbook for specific phrase mappings and theme visual design guidelines.
