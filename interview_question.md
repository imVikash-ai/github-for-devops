# 🐙 Git & GitHub - Scenario Based Interview Questions & Answers

> A structured Q&A guide covering Git & GitHub scenarios — merge conflicts, reverting commits, squashing, code review, CI/CD, forking, tagging, and submodules.


## 1. Scenario: Handling Merge Conflicts

**Question:** You are working in a team and while merging a feature branch into the main branch, you encounter a merge conflict. How would you resolve it?

**Answer:** When you encounter a merge conflict, the first step is to identify the conflicting files. Git will mark the conflict sections in these files, showing the differences between the branches. You can open each conflicting file in a text editor and look for conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`). These markers indicate the conflicting changes from each branch.

To resolve the conflict, you need to decide which changes to keep, either from your branch, the branch you are merging from, or a combination of both. After editing the files to resolve the conflicts, remove the conflict markers and save the changes. Next, add the resolved files to the staging area using `git add file`. Then, commit the changes with a meaningful commit message using `git commit`. Finally, you can complete the merge using `git merge --continue` if you are in the middle of a merge process. After resolving the conflict and committing the changes, make sure to inform your team and document the resolution if necessary.

---

## 2. Scenario: Reverting a Faulty Commit

**Question:** You realize that a commit you pushed to the main branch introduced a bug. How would you revert that commit without affecting subsequent commits?

**Answer:** To revert a specific commit without affecting subsequent commits, you can use the `git revert` command. First, identify the hash of the faulty commit using `git log`. Once you have the commit hash, run `git revert <commit-hash>`. This creates a new commit that undoes the changes introduced by the faulty commit while preserving the history of other commits.

For example, if the commit hash is `abc123`, you would run `git revert abc123`. Git will generate a new commit that reverses the changes from `abc123`. After reverting the commit, push the changes to the remote repository using `git push`. This ensures the bug is fixed without disrupting the history or the work of other team members.

---

## 3. Scenario: Squashing Commits Before Merging

**Question:** Your team prefers a clean commit history. Before merging a feature branch into the main branch, how would you squash multiple commits into one?

**Answer:** To squash multiple commits into one before merging, you can use an interactive rebase. First, check out your feature branch using `git checkout <feature-branch>`. Then, initiate an interactive rebase against the main branch with `git rebase -i main`. Git will open an editor with a list of commits from the feature branch. To squash commits, change the word `pick` to `squash` (or `s` for short) for each commit you want to squash into the previous one. Save and close the editor. Git will then combine the commits and prompt you to edit the commit message for the squashed commit. After finalizing the commit message, save and close the editor.

Finally, push the squashed commit to the remote repository using `git push --force` (use force push with caution, especially if others are working on the branch). This results in a single, clean commit on the feature branch that can be merged into the main branch.

---

## 4. Scenario: Code Review Workflow

**Question:** How would you manage a code review process using GitHub to ensure high code quality and collaboration within your team?

**Answer:** To manage a code review process on GitHub, follow these steps:

1. **Create a Pull Request (PR):** After completing work on a feature or bug fix, push the changes to a new branch and create a pull request against the main branch. Provide a clear and detailed description of the changes in the PR.
2. **Assign Reviewers:** Assign team members as reviewers for the PR. Choose individuals familiar with the codebase or the specific area of the changes.
3. **Review Changes:** Reviewers go through the changes, leaving comments and suggestions directly on the code lines in the PR. They can request changes if they find issues or approve the PR if it meets the standards.
4. **Address Feedback:** The author of the PR addresses the feedback by making additional commits to the PR branch. This might involve fixing bugs, improving code quality, or implementing suggestions.
5. **Re-review:** Reviewers check the updated changes to ensure all feedback has been addressed. If everything is satisfactory, they approve the PR.
6. **Merge:** Once the PR has the required approvals and passes any automated checks (such as CI tests), it can be merged into the main branch. Use the "Squash and Merge" or "Rebase and Merge" options to keep the commit history clean.
7. **Close PR:** After merging, close the PR and delete the feature branch if it's no longer needed.

Using this workflow ensures a collaborative and thorough review process, helping maintain high code quality and team cohesion.

---

## 5. Scenario: Handling Sensitive Information

**Question:** A teammate accidentally committed sensitive information (e.g., passwords, API keys) to the repository. How would you remove this information from the Git history?

**Answer:** To remove sensitive information from the Git history, you need to rewrite the repository history. One way to do this is using the git filter-branch command or the BFG Repo-Cleaner tool.

1. **Using git filter-branch:** Identify the sensitive file or information and its commit history. Run the following command to rewrite the history and remove the sensitive data:

```bash
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch path/to/sensitive/file' \
--prune-empty --tag-name-filter cat -- --all
```

2. **Using BFG Repo-Cleaner:**

Download and install BFG Repo-Cleaner. Then, run the following commands:

```bash
bfg --delete-files path/to/sensitive/file
git reflog expire --expire=now --all && git gc --prune=now --aggressive
```

After rewriting the history, force-push the changes to the remote repository with:

```bash
git push --force --all
```

and

```bash
git push --force --tags
```

Inform your team to re-clone the repository to ensure they have the updated history without the sensitive information.

---

## 6. Scenario: Rebasing vs. Merging

**Question:** Your team is debating whether to use rebase or merge for integrating changes from one branch to another. What are the pros and cons of each approach?

**Answer:**

**Merging:**

- **Pros:** Maintains the complete history of changes, showing exactly how branches have diverged and converged. It's safer for collaboration as it doesn't rewrite history, reducing the risk of conflicts.
- **Cons:** Can result in a more cluttered commit history with merge commits, which might make it harder to follow the linear progression of changes.

**Rebasing:**

- **Pros:** Creates a cleaner, linear commit history by applying changes from one branch onto another. This makes it easier to follow the project's development. Useful for keeping feature branches up-to-date with the main branch.
- **Cons:** Rewrites history, which can cause issues if not used carefully, especially in a shared repository. It can be disruptive if team members have already based their work on the commits being rebased.

In general, use rebasing for private branches or when you want to clean up a branch's commit history before merging. Use merging for integrating feature branches into the main branch to preserve the full context and history of changes.

---

## 7. Scenario: Continuous Integration (CI) with GitHub Actions

**Question:** How would you set up a CI pipeline using GitHub Actions to automatically run tests and build the project on every push and pull request?

**Answer:** To set up a CI pipeline with GitHub Actions, follow these steps:

1. **Create a Workflow File:** In your repository, create a directory called `.github/workflows` if it doesn't exist. Inside this directory, create a YAML file, e.g., `ci.yml`.

2. **Define the Workflow:** Open the `ci.yml` file and define the workflow:

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
      - name: Build project
        run: npm run build
```

3. **Push the Workflow File:** Commit and push the `ci.yml` file to your repository. GitHub Actions will automatically trigger the workflow on every push and pull request to the specified branches.

This workflow checks out the code, sets up the environment (e.g., Node.js), installs dependencies, runs tests, and builds the project. You can customize the steps according to your project's requirements.

---

## 8. Scenario: Forking Workflow for Open Source Contributions

**Question:** You want to contribute to an open-source project hosted on GitHub. Describe the forking workflow and how you would manage your contributions.

**Answer:** The forking workflow for contributing to an open-source project involves the following steps:

1. **Fork the Repository:** On GitHub, navigate to the repository you want to contribute to and click the "Fork" button. This creates a copy of the repository under your GitHub account.

2. **Clone the Forked Repository:** Clone your forked repository to your local machine using:

```bash
git clone https://github.com/imVikash-ai/github-for-devops.git
```

3. **Create a New Branch:** Create a new branch for your changes to keep your work organized and isolated:

```bash
git checkout -b feature-branch
```

4. **Make Changes and Commit:** Make your changes in the new branch. Stage and commit your changes with descriptive commit messages:

```bash
git add .
git commit -m "Description of changes"
```

5. **Push Changes to Fork:** Push your branch to your forked repository on GitHub:

```bash
git push origin feature-branch
```

6. **Create a Pull Request (PR):** On GitHub, navigate to the original repository and click "New Pull Request". Select the branch you pushed to your forked repository and create a PR. Provide a detailed description of your changes and why they are necessary.

7. **Respond to Feedback:** The repository maintainers will review your PR. Address any feedback or requested changes by making additional commits to your branch and pushing them to your forked repository. The PR will automatically update.

8. **Merge and Cleanup:** Once your PR is approved and merged, you can delete your feature branch both locally and on GitHub. Sync your fork with the upstream repository to keep it up-to-date.

This workflow ensures a clean and organized contribution process, making it easier for maintainers to review and merge your changes.

---

## 9. Scenario: Tagging Releases

**Question:** How would you create and manage tags in Git for marking release versions of your project?

**Answer:** Tags in Git are used to mark specific points in the repository's history, typically used for release versions. There are two types of tags: lightweight and annotated.

1. **Creating a Tag:**
   - **Lightweight Tag:** It's like a branch that doesn't change. Use it for temporary markers:

```bash
git tag v1.0
```

   - **Annotated Tag:** It includes metadata such as the tagger's name, email, date, and a message. Use it for release versions:

```bash
git tag -a v1.0 -m "Release version 1.0"
```

2. **Pushing Tags to Remote:** After creating a tag, push it to the remote repository:

```bash
git push origin v1.0
```

To push all tags:

```bash
git push origin --tags
```

3. **Listing Tags:** To see a list of tags in the repository:

```bash
git tag
```

4. **Checking Out a Tag:** To view the state of the repository at a specific tag:

```bash
git checkout v1.0
```

5. **Deleting a Tag:** To delete a tag locally:

```bash
git tag -d v1.0
```

To delete a tag from the remote repository:

```bash
git push origin --delete v1.0
```

---

## 10. Scenario: Git Submodules

**Question:** Your project depends on another Git repository. How would you include this dependency using Git submodules and manage it?

**Answer:** Git submodules allow you to include and manage external repositories within your project. Here's how to use them:

1. **Add a Submodule:** Navigate to your project's root directory and add the external repository as a submodule:

```bash
git submodule add https://github.com/username/repository-name.git path/to/submodule
```

2. **Initialize and Update Submodules:** When you clone a repository with submodules, initialize and update them:

```bash
git submodule init
git submodule update
```

Alternatively, you can use a single command to clone and update submodules:

```bash
git clone --recurse-submodules https://github.com/imVikash-ai/github-for-devops.git
```

3. **Commit Changes:** When you add or update submodules, commit the changes to the main repository:

```bash
git add path/to/submodule
git commit -m "Add/update submodule"
```

4. **Update Submodule:** To update the submodule to the latest commit on its main branch:

```bash
cd path/to/submodule
git pull origin main
cd ../..
git add path/to/submodule
git commit -m "Update submodule"
```

5. **Removing a Submodule:** To remove a submodule, follow these steps:
   - Delete the relevant section from the `.gitmodules` file.
   - Delete the relevant section from `.git/config`.
   - Remove the submodule directory and the entry in the index:

```bash
git rm --cached path/to/submodule
rm -rf path/to/submodule
rm -rf .git/modules/path/to/submodule
```

   - Commit the changes:

```bash
git commit -m "Remove submodule"
```

Using Git submodules allows you to manage dependencies cleanly, keeping the external code separate from your main project while maintaining the ability to track and update it as needed.

---

> 📝 *Notes compiled from Git & GitHub scenario-based interview preparation resources.*