# Google ADK Guide

A comprehensive, beginner-friendly guide to building AI Agents with the **Google Agent Development Kit (ADK)**. 

The live documentation site is automatically built and hosted:
👉 **Live Documentation Site**: [https://onerenix.github.io/google-adk-guide/](https://onerenix.github.io/google-adk-guide/)

---

## Technical Stack & How It Was Created

This documentation site was created using **MkDocs** and the **Material for MkDocs** theme. Here is the step-by-step layout of how it was built:

### 1. Scaffolding with MkDocs
1. **Initialize Project**: A clean repository directory was created, containing the standard MkDocs directories:
   - `docs/index.md` for the main documentation guide.
   - `docs/stylesheets/extra.css` for custom styling (such as the interactive hover effect cards and custom navigation).
   - `docs/images/` for user interface screenshots, logs, and flow architecture diagrams.
2. **Configure mkdocs.yml**: Created the site structure [mkdocs.yml](file:///Users/ultrenzv/Documents/DEV/ai_demo/google-adk-docs/mkdocs.yml) using the `material` theme, primary/accent colors (indigo), navigation sections, search plugins, and registered extensions (like `md_in_html` to support Markdown rendering inside HTML tag blocks).
3. **Create Requirements**: Lock the required versions in `requirements.txt` to ensure build environment stability:
   ```text
   mkdocs-material>=9.5.0
   ```

### 2. Setting Up the CI/CD Pipeline
An automated deployment workflow was created under `.github/workflows/deploy.yml`:
- **Trigger**: Every push to the `main` branch.
- **Actions**:
  1. Checks out the repository code.
  2. Sets up Python 3.x and caches the Material package dependencies.
  3. Installs dependencies from `requirements.txt`.
  4. Runs `mkdocs gh-deploy --force` which builds the static site into `site/` and automatically pushes the compiled assets to a dedicated `gh-pages` branch.

### 3. Deploying to GitHub and GitHub Pages
1. **Git Initialization**: The folder was initialized as a git repository (`git init`), all static resources staged, and the first commit made.
2. **GitHub Repository Creation**: Created a new public remote repository on GitHub using the GitHub CLI:
   ```bash
   gh repo create google-adk-guide --public
   ```
3. **Pushing Code**: Pushed the local repository to GitHub. The push triggered the deployment workflow on GitHub Actions.
   - **Initial Deployment Run**: [GitHub Actions Run 26311457075](https://github.com/OneRenix/google-adk-guide/actions/runs/26311457075) (Completed successfully in 16s).
4. **Enabling GitHub Pages**: Enabled the GitHub Pages service on the repository to serve the documentation from the root (`/`) of the generated `gh-pages` branch:
   ```bash
   echo '{"source": {"branch": "gh-pages", "path": "/"}}' | gh api --method POST repos/OneRenix/google-adk-guide/pages --input -
   ```

---

## Local Development

You can run and preview the documentation site locally.

### 1. Prerequisites
Ensure you have Python installed. We recommend using `uv` for fast package management:

```bash
# Install uv if you haven't already
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. Install Dependencies
```bash
uv pip install -r requirements.txt
```

### 3. Run the Development Server
Launch the live-reloading MkDocs server:
```bash
uv run mkdocs serve
```
The site will be available locally at **`http://127.0.0.1:8000/`**. Any modifications will automatically refresh in the browser.

### 4. Build Static Site Manually
To test the production build locally:
```bash
uv run mkdocs build
```

---

## Acknowledgement

This documentation guide and repository were scaffolded, structured, and styled in collaboration with Google's **Antigravity** AI assistant.
