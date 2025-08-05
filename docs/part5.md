# Part 5: Deploying the Site with GitHub Actions

To make your MkDocs site live, you’ll publish it to **GitHub Pages**. This section walks you through setting up a **GitHub** repository and automating the deployment process using **GitHub Actions**.

---

## 1. Create the GitHub Actions Workflow File

In Visual Studio Code:

 1. In your project's root directory, create a new folder named `.github`.
 2. Inside the `.github` folder, create another folder named `workflows`.
 3. Inside the `workflows` folder, create a file named `ci.yml` and paste in the following code:

```yaml title="ci.yml"
name: ci
on:
  push:
    branches:
      - master
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Configure Git Credentials
        run: |
          git config user.name github-actions[bot]
          git config user.email 41898282+github-actions[bot]@users.noreply.github.com
      - uses: actions/setup-python@v5
        with:
          python-version: 3.x
      - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV
      - uses: actions/cache@v4
        with:
          key: mkdocs-material-${{ env.cache_id }}
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```


!!! warning 

    The file path must be exactly **.github/workflows/ci.yml** for GitHub to recognize it.


## 2. Create a New GitHub Repository

Go to [github](https://github.com/) and create a new repository (public repository).
!!! warning 

    Do **not** initialize it with a `README` or `license`.


## 3. Link Your Local Project to the Repository

Before you proceed, stop the local server by pressing `Ctrl+C` in your terminal. 

### 3.1 Create a .gitignore File

Create a new file named `.gitignore` in your project's root directory and add in the following content in it.
```yaml
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
pip-wheel-metadata/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py,cover
.hypothesis/
.pytest_cache/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
.python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.
#Pipfile.lock

# PEP 582; used by e.g. github.com/David-OConnor/pyflow
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/
```
> This file tells Git to ignore certain files and folders, preventing them from being committed to your repository.

### 3.2 Initialize the Repository

Now, initialize a Git repository in your project folder and push your code to a new repository on GitHub.

```bash
# Initializes a new Git repository.
git init

# Stages all the files, including the new .github folder.
git add .

# Shows which files are about to be committed.
git status

# Creates the first commit.
git commit -m "Initial commit of MkDocs project."

# Connects your local repository to a remote repository on GitHub.
# (Paste the remote URL from your new GitHub repository in the below command.) 
git remote add origin https://github.com/your-username/your-repo-name.git


# Pushes your code to the 'main' branch on GitHub.
git push -u origin main

```

>Go to your GitHub repository and refresh the page to see your files.

## 4. Configure GitHub Pages

 1. On your GitHub repository, go to **Settings** > **Pages**.
 2. Under **Source**, select:
    * Deploy from a branch
    * Branch: **gh-pages**
 3. Save your changes.


# 5. Watch the Action Deploy Your Site
GitHub Actions will automatically build and deploy your site.

The deployment may take a couple of minutes — once complete, a live URL will appear under **Settings → Pages**, which you can click to view your published site.

---

# Conclusion
You’ve **successfully** completed the setup. 

Your **documentation site** is now fully **functional**, **version-controlled**, and **hosted** using **GitHub Pages**. With this foundation in place, you can confidently add new content, customize the theme, and manage updates with ease.


---
⬅️ **Previous:** [Create and Configure the Project](part4.md)
