# 🚀 GitHub for DevOps

> **Hands-on Git & GitHub learning for DevOps Engineers** — covering version control workflows, branching, merging, Python scripting with Pylint, and GitHub Actions CI/CD pipelines.

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-blue?logo=githubactions&logoColor=white)](https://github.com/imVikash-ai/github-for-devops/actions)
[![Python](https://img.shields.io/badge/Python-3.x-green?logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Repo Size](https://img.shields.io/github/repo-size/imVikash-ai/github-for-devops)](https://github.com/imVikash-ai/github-for-devops)

---

## 📋 Table of Contents

- [About](#-about)
- [Repository Structure](#-repository-structure)
- [What You'll Learn](#-what-youll-learn)
- [Getting Started](#-getting-started)
- [Git Commands Reference](#-git-commands-reference)
- [GitHub Actions CI/CD](#-github-actions-cicd)
- [Python Scripts](#-python-scripts)
- [Branching Strategy](#-branching-strategy)
- [Contributing](#-contributing)
- [Author](#-author)

---

## 📖 About

This repository is a **practical DevOps learning lab** built to help developers and DevOps engineers get hands-on experience with:

- Core **Git** version control workflows
- **GitHub** collaboration patterns (branches, pull requests, merges)
- **GitHub Actions** — CI/CD automation pipelines
- **Python** scripting with code quality tools like **Pylint**

Every file in this repo was created as part of a real learning journey — commands were run, files were committed, branches were created, and pipelines were triggered. This makes it an ideal reference for anyone starting out in DevOps.

---

## 📁 Repository Structure

```
github-for-devops/
│
├── .github/
│   └── workflows/          # GitHub Actions CI/CD pipeline definitions (YAML)
│
├── demo.py                 # Python demo module used to test Pylint linting
├── testing.py              # Python file for hands-on testing practice
├── this_is_from_dev.txt    # File created from the dev branch (branch practice)
├── git_commands.txt        # Log of Git commands practiced during learning
└── README.md               # You are here!
```

---

## 🎯 What You'll Learn

| Topic | Description |
|---|---|
| 🔧 **Git Basics** | `init`, `add`, `commit`, `status`, `restore` and more |
| 🌿 **Branching** | Create, switch, and merge branches (`dev`, `master`) |
| 🔄 **GitHub Workflow** | Push, pull, fork, and pull request flow |
| ⚡ **GitHub Actions** | Write and trigger CI/CD pipelines using YAML |
| 🐍 **Python + Pylint** | Write clean Python code and auto-lint it in CI |
| 🛡️ **Code Quality** | Enforce standards on every push using automated checks |

---

## 🚀 Getting Started

### Prerequisites

- [Git](https://git-scm.com/downloads) installed on your machine
- A [GitHub](https://github.com) account
- [Python 3.x](https://www.python.org/downloads/) installed

### 1. Clone the Repository

```bash
git clone https://github.com/imVikash-ai/github-for-devops.git
cd github-for-devops
```

### 2. Set Up Git Identity (first time only)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### 3. Explore the Repo

```bash
ls -a          # See all files including hidden ones like .git
git log        # View commit history
git status     # Check working tree status
```

---

## 📝 Git Commands Reference

A quick reference of the core Git commands practiced in this repository:

```bash
# Initialize a repository
git init

# Check status of working directory
git status

# Stage a specific file
git add testing.py

# Stage all changes
git add .

# Unstage a file (keep changes)
git rm --cached testing.py

# Commit staged changes
git commit -m "your commit message"

# Restore a deleted/modified file from the last commit
git restore testing.py

# View full command history
history
```

> See [`git_commands.txt`](./git_commands.txt) for the exact commands practiced during this session.

---

## ⚡ GitHub Actions CI/CD

This repository uses **GitHub Actions** to automate code quality checks on every push.

### Workflow Location

```
.github/workflows/
```

### What the Pipeline Does

On every `push` or `pull_request`, the CI pipeline:

1. ✅ Checks out the repository code
2. ✅ Sets up Python environment
3. ✅ Installs dependencies (Pylint)
4. ✅ Runs **Pylint** on Python files to enforce code quality

### Sample Workflow YAML

```yaml
name: Python Lint CI

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs:
  lint:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install Pylint
        run: pip install pylint

      - name: Run Pylint
        run: pylint demo.py testing.py
```

> View live workflow runs: [Actions Tab](https://github.com/imVikash-ai/github-for-devops/actions)

---

## 🐍 Python Scripts

### `demo.py` — Pylint Demo Module

A simple, well-documented Python module used to demonstrate that the GitHub Actions linting pipeline works correctly.

```python
"""Demo module for testing Pylint."""

def my_function():
    """Return the value 5."""
    a = 5
    return a

my_function()
```

Run it locally:
```bash
python demo.py
```

Lint it locally:
```bash
pip install pylint
pylint demo.py
```

### `testing.py` — Practice Script

A Python file used for hands-on Git practice — staging, committing, unstaging, and restoring files.

---

## 🌿 Branching Strategy

This repo demonstrates a simple **feature branch workflow**:

```
master  ←─── main production branch
  │
  └── dev  ←─── development / feature branch
```

**Branch workflow practiced:**

```bash
# Create and switch to a new branch
git checkout -b dev

# Make changes and commit
git add .
git commit -m "changes from dev branch"

# Push branch to remote
git push origin dev

# Merge into master via Pull Request on GitHub
```

> The file `this_is_from_dev.txt` was created on the `dev` branch and later merged into `master` — a real example of the branch → PR → merge flow.

---

## 🤝 Contributing

Contributions are welcome! If you'd like to add more Git examples, workflows, or DevOps scripts:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Commit (`git commit -m "Add: your feature"`)
5. Push to your branch (`git push origin feature/your-feature`)
6. Open a **Pull Request**

---

## 👨‍💻 Author

**Vikash** — [@imVikash-ai](https://github.com/imVikash-ai)

> Learning DevOps one commit at a time. 🚀

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">
  <sub>Built with ❤️ for DevOps learners everywhere</sub>
</div>