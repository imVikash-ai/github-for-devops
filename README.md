# 🛠️ GitHub for DevOps

A hands-on learning repository covering **Git & GitHub fundamentals** from a DevOps perspective — including version control workflows, branching strategies, and GitHub Actions CI/CD pipelines.

---

## 📌 About

This repo documents my practical learning journey with Git and GitHub as core DevOps tools. It covers everything from basic git commands to automating workflows with GitHub Actions.

---

## 📂 Repository Structure

```
github-for-devops/
│
├── .github/
│   └── workflows/          # GitHub Actions CI/CD pipeline configs
│
├── demo.py                 # Demo Python script for version control practice
├── testing.py              # Script used for staging, committing & restoring practice
├── this_is_from_dev.txt    # File created from dev branch (branching practice)
└── git_commands.txt        # Personal reference sheet of practiced Git commands
```

---

## 🧠 What I Learned

### 🔹 Git Basics
| Command | Description |
|---|---|
| `git init` | Initialize a new Git repository |
| `git status` | Check the state of the working directory |
| `git add .` | Stage all changes |
| `git add <file>` | Stage a specific file |
| `git commit -m "message"` | Commit staged changes |
| `git rm --cached <file>` | Unstage a file (keep on disk) |
| `git restore <file>` | Restore a deleted or modified file |
| `git log` | View commit history |

### 🔹 Branching & Merging
| Command | Description |
|---|---|
| `git branch` | List all branches |
| `git branch <name>` | Create a new branch |
| `git checkout <branch>` | Switch to a branch |
| `git checkout -b <branch>` | Create and switch to a new branch |
| `git merge <branch>` | Merge a branch into current branch |
| `git branch -d <branch>` | Delete a branch |

### 🔹 Remote & Collaboration
| Command | Description |
|---|---|
| `git remote add origin <url>` | Connect local repo to GitHub |
| `git push origin <branch>` | Push branch to remote |
| `git pull origin <branch>` | Pull latest changes |
| `git clone <url>` | Clone a remote repository |
| `git fetch` | Fetch remote changes without merging |

### 🔹 GitHub Actions (CI/CD)
- Wrote and tested workflow `.yml` files inside `.github/workflows/`
- Learned how to trigger pipelines on `push` and `pull_request` events
- Understood jobs, steps, and runners in GitHub Actions

---

## ⚡ Quick Git Setup (Reference)

```bash
# Configure Git identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Initialize & first commit
git init
git add .
git commit -m "initial commit"

# Connect to GitHub & push
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin master
```

---

## 🔄 Branching Workflow Practiced

```
master (main branch)
   │
   ├── dev branch → created file: this_is_from_dev.txt
   │                              ↓
   └──────────── merged back into master
```

---

## 👨‍💻 Author

**Vikash Kumar** — DevOps & Gen AI Engineer


---

## 📄 License

This project is licensed under the MIT License.
