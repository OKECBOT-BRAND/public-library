# Development Workflow

## Branching Strategy

### Main Branches

We maintain three main branches with specific purposes and protection rules:

#### 1. 🏗️ Development (`development`)
- **Purpose**: Integration branch for all new features and bug fixes
- **Flow**: Features are merged here first for integration testing
- **Protection**:
  - Requires pull request reviews (minimum 1 approval)
  - Requires conversation resolution
  - No direct pushes - all changes must go through PRs
  - Administrators must follow these rules

#### 2. 🧪 Testing (`testing`)
- **Purpose**: Quality assurance and pre-production validation
- **Flow**: Code moves here after passing initial development testing
- **Protection**:
  - Requires 2 approvals (including QA lead)
  - Requires signed commits
  - Requires linear history
  - No force pushes or deletions

#### 3. 🚀 Main (`main`)
- **Purpose**: Production-ready code only
- **Flow**: Code moves here after thorough testing and approval
- **Protection**:
  - Requires Product Lead + Tech Lead approval
  - Requires signed commits
  - Locked branch (no direct pushes)
  - No force pushes or deletions

## Branch Approval Requirements

### Review and Merge Process

| Branch | Approvals Required | Required Reviewers | Additional Requirements |
|--------|-------------------|-------------------|-------------------------|
| `development` | 1+ | Any team member with write access | - All CI tests must pass<br>- No merge conflicts<br>- Documentation updated |
| `testing` | 2+ | 1 Senior Developer + 1 QA Engineer | - All tests must pass<br>- Manual test results attached<br>- Security scan clean |
| `main` | 2+ | Product Lead + Tech Lead | - Full regression test pass<br>- Security review completed<br>- Rollback plan documented |
| `hotfix/*` | 2+ | Tech Lead + 1 Senior Developer | - Hotfix justification provided<br>- Impact assessment included |

### Approval Process
1. **Create a Pull Request** with complete description
2. **Request Reviews** from required approvers
3. **Address Feedback** from code reviews
4. **Verify Checks** - All CI/CD pipelines must pass
5. **Squash and Merge** (for feature branches)
6. **Delete Source Branch** after successful merge

### Branch Naming

Format: `type/issue-number-kebab-case-title`

**Branch Types**:
- `feature/` - New functionality (e.g., `feature/123-add-marketplace-webhook`)
- `bugfix/` - Fixes (e.g., `bugfix/456-fix-sync-issue`)
- `hotfix/` - Urgent production patches (bypasses normal flow)
- `chore/` - Tooling, dependencies, maintenance
- `docs/` - Documentation updates
- `refactor/` - Code improvements without changing functionality

### Creating a New Branch

```bash
git checkout -b type/123-descriptive-branch-name
```

## Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
type(scope): short description

Longer description if needed

Fixes #123
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code changes that don't fix bugs or add features
- `perf`: Performance improvements
- `test`: Adding or modifying tests
- `chore`: Changes to build process or auxiliary tools

## Pull Requests

1. **Before creating a PR**:
   - Rebase on the latest `main` branch
   - Run all tests
   - Ensure code meets style guidelines
   - Update documentation if needed

2. **PR Title Format**:
   ```
   type(scope): Short description (fixes #123)
   ```

3. **PR Description**:
   - Reference related issues
   - Describe changes
   - Include screenshots if applicable
   - Update documentation if needed

## Code Review

1. **As an Author**:
   - Address all review comments
   - Keep commits focused and atomic
   - Update documentation as needed

2. **As a Reviewer**:
   - Review within 24 hours if possible
   - Be constructive and specific
   - Check for security implications
   - Verify tests are included for new features

## Merging

- Squash and merge for feature branches
- Rebase and merge for hotfixes
- Delete branches after merging

## Next Steps

- [Code Style & Standards →](3-code-style.md)
- [Testing Guidelines →](4-testing.md)
