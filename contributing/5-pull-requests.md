# Pull Request Process

## Before Creating a PR

1. **Ensure Code Quality**
   - Run linters and formatters
   - Verify all tests pass
   - Check for code smells
   - Remove debug code and console logs

2. **Update Documentation**
   - Update README if needed
   - Add/update API documentation
   - Include migration instructions if schema changed

3. **Self-Review**
   - Review your own changes
   - Ensure the PR is focused on a single feature/bug
   - Remove any commented-out code

## Creating a Pull Request

### PR Title Format

```
type(scope): Short description (fixes #123)
```

**Examples**:
- `feat(auth): add password reset flow (fixes #123)`
- `fix(api): handle null user in auth middleware`
- `docs(readme): update installation instructions`

### PR Description Template

```markdown
## Description
<!-- Describe your changes in detail -->

## Related Issues
<!-- List related issues (e.g., Fixes #123, Related to #456) -->

## Type of Change
<!-- Check all that apply -->
- [ ] Bug fix (non-breaking change)
- [ ] New feature (non-breaking change)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring
- [ ] Test updates
- [ ] CI/CD pipeline changes

## Testing
<!-- Describe how you tested your changes -->
- [ ] Unit tests
- [ ] Integration tests
- [ ] Manual testing

## Screenshots/Videos
<!-- If applicable, add screenshots or screen recordings -->

## Checklist
- [ ] My code follows the style guidelines
- [ ] I have performed a self-review of my code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective
- [ ] New and existing unit tests pass locally with my changes
- [ ] Any dependent changes have been merged and published

## Deployment Notes
<!-- Special instructions for deployment, migrations, etc. -->
```

## Code Review Process

1. **Initial Review** (Within 24 hours)
   - Automated checks (CI, tests, linting)
   - Initial code review by team members
   - Request changes if needed

2. **Addressing Feedback**
   - Make requested changes
   - Push new commits (don't amend/force push)
   - Resolve conversations when addressed

3. **Approval**
   - At least one approval required
   - All discussions must be resolved
   - All checks must pass

4. **Merging**
   - Squash and merge for feature branches
   - Rebase and merge for hotfixes
   - Delete source branch after merge

## Best Practices

### For Authors
- Keep PRs small and focused
- Include tests for new features
- Update documentation
- Be responsive to review comments
- Break large changes into multiple PRs

### For Reviewers
- Be constructive and kind
- Focus on code, not the author
- Suggest improvements, not just problems
- Review within 24 hours if possible
- Check for security implications

### Commit Messages in PRs

- Use present tense ("Add feature" not "Added feature")
- Reference issues and PRs
- Keep the first line under 72 characters
- Include details in the body if needed

## Common Issues to Check

- [ ] Memory leaks
- [ ] Security vulnerabilities
- [ ] Performance impacts
- [ ] Browser/device compatibility
- [ ] Accessibility concerns
- [ ] Internationalization needs

## Next Steps

- [Release Process →](6-release-process.md)
- [Getting Started →](../CONTRIBUTING.md)
