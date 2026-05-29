# 🤝 Contributing Guide — How to Commit & Create Pull Requests

> A beginner-friendly guide for the **Git & GitHub: Version Control for Your Programming Journey** session.
> Presented by **Arden Diago (2547112)** & **Hari P (2547120)** — MCA A, Christ University.

---

## 📋 Table of Contents

- [Before You Start](#-before-you-start)
- [Forking & Cloning](#-forking--cloning)
- [Branching — The Right Way](#-branching--the-right-way)
- [Making Changes & Staging](#-making-changes--staging)
- [Writing a Good Commit Message](#-writing-a-good-commit-message)
- [Pushing Your Branch](#-pushing-your-branch)
- [Creating a Pull Request](#-creating-a-pull-request)
- [PR Etiquette & Best Practices](#-pr-etiquette--best-practices)
- [After Your PR is Merged](#-after-your-pr-is-merged)
- [Common Mistakes to Avoid](#-common-mistakes-to-avoid)

---

## ⚙️ Before You Start

Make sure Git is set up on your machine with your identity:

```bash
# Check if Git is installed
git --version

# Set your name and email (only needed once)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Verify your config
git config --list
```

---

## 🍴 Forking & Cloning

### If you're contributing to someone else's project:

**Step 1 — Fork the repository**

Click the **Fork** button (top-right on the GitHub repo page).  
This creates your own copy of the project under your GitHub account.

**Step 2 — Clone your fork**

```bash
git clone https://github.com/YOUR-USERNAME/REPO-NAME.git
cd REPO-NAME
```

**Step 3 — Add the original repo as upstream**

```bash
git remote add upstream https://github.com/ORIGINAL-OWNER/REPO-NAME.git

# Verify both remotes exist
git remote -v
# origin    https://github.com/YOUR-USERNAME/REPO-NAME.git (fetch)
# upstream  https://github.com/ORIGINAL-OWNER/REPO-NAME.git (fetch)
```

> `origin` = your fork | `upstream` = the original project

---

### If you're on the same team with direct repo access:

```bash
git clone https://github.com/OWNER/REPO-NAME.git
cd REPO-NAME
```

---

## 🌿 Branching — The Right Way

> ⚠️ **Golden Rule: NEVER commit directly to `main`. Always work on a branch.**

**Step 1 — Make sure your main is up to date**

```bash
git checkout main
git pull origin main        # or: git pull upstream main (if using a fork)
```

**Step 2 — Create a new branch**

```bash
# Create and switch in one command
git switch -c your-branch-name

# Examples of good branch names:
git switch -c feature/add-login-page
git switch -c fix/null-pointer-auth
git switch -c docs/update-readme
git switch -c chore/cleanup-unused-imports
```

### Branch Naming Convention

| Prefix | When to Use | Example |
|--------|-------------|---------|
| `feature/` | New functionality | `feature/user-profile` |
| `fix/` | Bug fixes | `fix/login-crash` |
| `docs/` | Documentation only | `docs/api-reference` |
| `chore/` | Maintenance tasks | `chore/upgrade-dependencies` |
| `hotfix/` | Urgent production fix | `hotfix/payment-gateway` |

---

## 📝 Making Changes & Staging

Make your code changes, then stage them for commit.

```bash
# See what files have changed
git status

# See exactly what changed line-by-line
git diff

# Stage specific files
git add src/auth.js
git add README.md

# Stage everything in the current directory
git add .

# Unstage a file you accidentally staged
git restore --staged filename.js

# Stage only parts of a file (interactive)
git add -p filename.js
```

> 💡 **Tip:** Review `git diff --staged` before committing to make sure you're only committing what you intend to.

```bash
# See staged changes (what will go into the next commit)
git diff --staged
```

---

## ✍️ Writing a Good Commit Message

This is one of the most important skills in Git. A good commit message tells your teammates (and future you) **what changed and why**.

### The Format

```
<type>(<scope>): <short summary>

<optional body — explain WHY, not WHAT>

<optional footer — reference issues>
```

### Types

| Type | When to Use |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes |
| `style` | Formatting, missing semicolons (no logic change) |
| `refactor` | Code restructuring (no feature or bug fix) |
| `test` | Adding or updating tests |
| `chore` | Build process, dependency updates |

### Examples

```bash
# ✅ Good commit messages
git commit -m "feat(auth): add JWT-based login endpoint"
git commit -m "fix(ui): resolve header overlap on mobile screens"
git commit -m "docs: update installation steps in README"
git commit -m "refactor(api): extract rate limiter into middleware"

# ❌ Bad commit messages — never do these
git commit -m "fix"
git commit -m "updated stuff"
git commit -m "asdfghjkl"
git commit -m "final version"
git commit -m "final FINAL version"
```

### Multi-line Commit (with body)

```bash
git commit -m "fix(auth): handle expired token edge case

Previously, the app would crash silently when a JWT token
expired mid-session. Now it clears the token and redirects
the user to the login page with an appropriate error message.

Closes #42"
```

> 💡 **Rule of thumb:** If you can't summarize your commit in one line, you're probably committing too much. Break it into smaller commits.

---

## 🚀 Pushing Your Branch

Once you've made your commits, push your branch to GitHub:

```bash
# Push your branch for the first time
git push -u origin your-branch-name

# After the first push, you can just use:
git push
```

> The `-u` flag sets up tracking so future `git push` and `git pull` know which branch to use automatically.

### Keeping Your Branch Up to Date

If `main` has been updated while you were working, sync your branch:

```bash
# Option 1: Merge main into your branch
git checkout main
git pull origin main
git checkout your-branch-name
git merge main

# Option 2: Rebase (creates cleaner linear history)
git checkout your-branch-name
git rebase main

# If there are conflicts, resolve them, then:
git add .
git rebase --continue
```

---

## 📬 Creating a Pull Request

A **Pull Request (PR)** is a formal request to merge your branch into the main codebase.

### Via GitHub Web UI

1. Go to the repository on GitHub
2. You'll see a banner: **"Your branch had recent pushes"** → click **Compare & pull request**
3. Or go to **Pull requests** tab → **New pull request**
4. Set:
   - **base:** `main` (where you want to merge INTO)
   - **compare:** `your-branch-name` (your work)
5. Fill in the PR form (see below)
6. Click **Create Pull Request**

### Via GitHub CLI

```bash
# Create a PR from your current branch
gh pr create --title "feat(auth): add JWT login" --body "Adds token-based authentication"

# Create with a template interactively
gh pr create

# Create as a draft (not ready for review yet)
gh pr create --draft

# View your open PRs
gh pr list

# Check status of your PR
gh pr status
```

---

### Writing a Good PR Description

Use this template when creating your PR:

```markdown
## What does this PR do?
<!-- Brief description of the changes -->

## Why is this needed?
<!-- Context and motivation -->

## How was it tested?
<!-- What testing did you do? -->

## Screenshots (if UI changes)
<!-- Attach before/after screenshots -->

## Checklist
- [ ] Code follows the project's style guide
- [ ] Self-reviewed my own code
- [ ] Added/updated comments where needed
- [ ] No console.log or debug statements left in
- [ ] Tested locally and it works
- [ ] Linked to the related issue (if any)

## Related Issues
Closes #<issue-number>
```

---

## 🤝 PR Etiquette & Best Practices

### As the PR Author

- Keep PRs **small and focused** — one feature or fix per PR
- Don't open a PR with 30 files changed if it can be split into smaller ones
- Respond to review comments **within 24 hours**
- Don't dismiss reviewer comments — discuss and explain your reasoning
- Mark conversations as resolved **only after** you've addressed them
- Don't force-push to a branch that's already in review (it breaks the reviewer's context)

### As a Reviewer

- Be respectful — critique the code, not the person
- Use **suggestions** in GitHub to propose exact changes
- Distinguish between blocking issues and minor nits:
  - `blocking:` This must be fixed before merging
  - `nit:` Minor suggestion, up to you
  - `question:` Just asking for clarity
- Approve only when you'd be comfortable with it in production

---

## ✅ After Your PR is Merged

Clean up your local environment:

```bash
# Switch back to main
git checkout main

# Pull the merged changes
git pull origin main

# Delete your local branch (it's been merged, no longer needed)
git branch -d your-branch-name

# Delete the remote branch (GitHub may do this automatically)
git push origin --delete your-branch-name

# Sync your fork's main with upstream (if using a fork)
git pull upstream main
git push origin main
```

---

## 🚫 Common Mistakes to Avoid

| ❌ Mistake | ✅ What to Do Instead |
|-----------|----------------------|
| Committing directly to `main` | Always create a branch first |
| Vague commit messages like `"fix"` | Write descriptive messages: `"fix(auth): handle null token"` |
| One giant commit with 50 file changes | Make small, focused commits |
| Not pulling latest `main` before branching | Always `git pull` before creating a branch |
| Committing `.env` files or API keys | Add sensitive files to `.gitignore` |
| Force pushing to a shared branch | Never `git push --force` on `main` or in-review branches |
| Ignoring merge conflicts | Resolve them carefully, test after resolving |
| Opening a PR without testing locally | Always test before raising a PR |

---

## 🔖 Quick Reference Card

```bash
# --- Full Contribution Workflow ---

# 1. Clone / update
git clone <url>                         # first time
git pull origin main                    # every time after

# 2. Branch
git switch -c feature/your-feature

# 3. Work
git status                              # check what changed
git add .                               # stage everything
git diff --staged                       # review before committing
git commit -m "feat: describe change"   # commit with good message

# 4. Push
git push -u origin feature/your-feature

# 5. PR
gh pr create                            # via CLI
# or go to GitHub.com and click "Compare & pull request"

# 6. After merge
git checkout main
git pull origin main
git branch -d feature/your-feature
```

---

## 📚 Further Reading

- [GitHub Docs — About Pull Requests](https://docs.github.com/en/pull-requests)
- [Conventional Commits Specification](https://www.conventionalcommits.org)
- [Git Flight Rules](https://github.com/k88hudson/git-flight-rules) — What to do when things go wrong
- [Oh Shit, Git!](https://ohshitgit.com) — Plain English fixes for common Git mistakes

---

*Made with ❤️ for the MCA batch at Christ University, Bangalore.*  
*Session by Arden Diago & Hari P — Git & GitHub: Version Control for Your Programming Journey*

wassssaaaapppp
