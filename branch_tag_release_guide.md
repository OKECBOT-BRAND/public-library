# 🌿 Branch, Tag & Release Management Guide

## 🎯 Understanding the Basics

### What is a Branch?
A **branch** is like a separate timeline for your code. It allows you to work on features or fixes without affecting the main codebase.

**Think of it like this:**
- `main` = The official, production-ready code
- `testing` = Where code is tested before production
- `development` = Where new features are integrated
- `feature/your-feature` = Your personal workspace for a new feature

### What is a Tag?
A **tag** is a snapshot of your code at a specific point in time, usually marking a release version (like `v1.2.3`). Tags are permanent markers that help you:
- Track which version is in production
- Roll back to a specific version if needed
- Reference specific code versions in bug reports

### What is a Release?
A **release** is a packaged version of your application that's ready for users. It's typically created from a tag and includes:
- Compiled application files
- Release notes
- Version number

---

## 📋 Branch Strategy Rules

### 🚫 What Not To Do
- ❌ **NEVER** push directly to `main`, `develop`, or other developers' branches
- ❌ **NEVER** force push to shared branches
- ❌ **NEVER** commit to someone else's branch without explicit permission
- ❌ **NEVER** merge your own PR without review (unless you have maintainer privileges)

### ✅ What To Do
- ✅ **ALWAYS** create a new branch for each feature, bug fix, or issue
- ✅ **ALWAYS** use descriptive branch names
- ✅ **ALWAYS** push your branch and create a Pull Request for review
- ✅ **ALWAYS** keep your branch updated with the target branch

## 🌿 Working with Branches
### Required Protected Branches
development → testing → main

### 1. 🏗️ Development Branch (`development`)
**Purpose:** Integration branch for all incoming changes

**Protection Rules:**
- ✅ **Require pull request reviews** before merging
  - Minimum: 1 approved review
  - Dismiss stale pull request approvals when new commits are pushed
- ✅ **Require conversation resolution** before merging
- ✅ **Include administrators** - even admins must follow these rules
- ❌ **Allow force pushes** - disabled
- ❌ **Allow deletions** - disabled

**Who Can Merge:**
- Repository maintainers
- Code owners
- Users with write access

---

### 2. 🧪 Testing Branch (`testing`)
**Purpose:** Quality assurance and validation environment

**Protection Rules:**
- ✅ **Require pull request reviews** before merging
  - Minimum: 2 approved reviews (including QA lead)
  - Required reviewers: QA team members
- ✅ **Require signed commits**
- ✅ **Require linear history**
- ❌ **Allow force pushes** - disabled
- ❌ **Allow deletions** - disabled

**Who Can Merge:**
- QA team members
- Release managers
- Product lead

---

### 3. 🚀 Main Branch (`main`)
**Purpose:** Production-ready code only

**Protection Rules:**
- ✅ **Require pull request reviews** before merging
  - Minimum: 1 approved review
  - Required reviewers: Product lead + Tech lead
- ✅ **Require signed commits**
- ✅ **Require linear history**
- ✅ **Lock branch** - prevents all pushes without proper access
- ❌ **Allow force pushes** - disabled
- ❌ **Allow deletions** - disabled

**Who Can Merge:**
- Product lead only
- Emergency: Tech lead (with post-merge review)



### Checking Which Branch You're On

```bash
# See current branch
git branch

# The branch with * is your current branch
# Example output:
#   development
# * feature/user-authentication  ← You're here
#   main
```

Or use:
```bash
git status
# Shows: "On branch feature/user-authentication"
```

### Viewing All Branches

```bash
# Local branches only
git branch

# All branches (local + remote)
git branch -a

# Remote branches only
git branch -r
```

### Switching Between Branches

```bash
# Switch to a different branch
git checkout main
git checkout development
git checkout feature/your-feature-name

# Or using newer syntax
git switch main
git switch development
```

### Creating a New Branch

```bash
# Method 1: Create and switch in one command
git checkout -b feature/your-feature-name

# Method 2: Create from a specific branch
git checkout development
git pull origin development
git checkout -b feature/your-feature-name

# Method 3: Using newer syntax
git switch -c feature/your-feature-name
```

### Pushing Your Branch to Remote

```bash
# First time pushing a new branch
git push -u origin feature/your-feature-name

# Subsequent pushes (after -u is set)
git push
```

### Updating Your Branch with Latest Changes

```bash
# Fetch latest changes from remote
git fetch origin

# Update your branch with changes from development
git checkout feature/your-feature-name
git rebase origin/development

# Or merge instead of rebase (if preferred)
git merge origin/development
```

### Deleting Branches

```bash
# Delete local branch (after merging)
git branch -d feature/your-feature-name

# Force delete (if branch not fully merged)
git branch -D feature/your-feature-name

# Delete remote branch
git push origin --delete feature/your-feature-name
```

---

## 🏷️ Working with Tags

### Viewing Tags

```bash
# List all tags
git tag

# List tags matching a pattern
git tag -l "v1.*"

# View tag details
git show v1.2.3
```

### Creating a Tag

```bash
# Lightweight tag (just a pointer)
git tag v1.2.3

# Annotated tag (recommended - includes message)
git tag -a v1.2.3 -m "Release version 1.2.3"

# Tag a specific commit
git tag -a v1.2.3 <commit-hash> -m "Release version 1.2.3"
```

### Pushing Tags to Remote

```bash
# Push a specific tag
git push origin v1.2.3

# Push all tags
git push origin --tags

# Push all tags (alternative)
git push --tags
```

### Checking Out a Tag

```bash
# View code at a specific tag (creates detached HEAD)
git checkout v1.2.3

# Create a branch from a tag
git checkout -b hotfix-from-v1.2.3 v1.2.3
```

### Deleting Tags

```bash
# Delete local tag
git tag -d v1.2.3

# Delete remote tag
git push origin --delete v1.2.3
# Or
git push origin :refs/tags/v1.2.3
```

---


## 🚀 Working with Releases

### Understanding the Release Process

In this project, releases follow this flow:

```
feature/bugfix branch
        ↓
   development (integration)
        ↓
     testing (QA validation)
        ↓
      main (production)
        ↓
    Tag created (v1.2.3)
        ↓
   Release published
```

### Creating a Release (Product Lead Only)

**Step 1:** After code is merged to `main`:

```bash
# Switch to main branch
git checkout main
git pull origin main

# Create an annotated tag
git tag -a v1.2.3 -m "Release version 1.2.3 - [Brief description]"

# Push tag to remote
git push origin v1.2.3
```

**Step 2:** Create Release on GitHub:
1. Go to your repository on GitHub
2. Click "Releases" → "Create a new release"
3. Select the tag you just created (v1.2.3)
4. Add release title and description
5. Attach build artifacts if needed
6. Click "Publish release"

### Version Numbering Convention

Use **Semantic Versioning** (SemVer): `MAJOR.MINOR.PATCH`

- **MAJOR** (1.0.0): Breaking changes
- **MINOR** (0.1.0): New features (backward compatible)
- **PATCH** (0.0.1): Bug fixes

Examples:
- `v1.0.0` - First stable release
- `v1.1.0` - Added new features
- `v1.1.1` - Bug fix release
- `v2.0.0` - Major update with breaking changes

---

### Common Workflows

#### Starting a New Feature
```bash
git checkout development
git pull origin development
git checkout -b feature/my-new-feature
# ... make changes ...
git add .
git commit -m "feat: add new feature"
git push -u origin feature/my-new-feature
```

#### Updating Your Feature Branch
```bash
git checkout feature/my-new-feature
git fetch origin
git rebase origin/development
git push --force-with-lease
```

#### Checking Out a Specific Release
```bash
# See what releases are available
git tag -l

# Checkout a specific release version
git checkout v1.2.3

# Or create a branch from that release
git checkout -b investigate-v1.2.3 v1.2.3
```


*Okecbot Product Development Team | Abuja, Nigeria | Built by DCSSP*  
*Last updated: November 07, 2025*