# Contributing to Shared Workflows

Thank you for your interest in contributing to this project! This document provides guidelines for contributing to the shared workflows repository.

## Code of Conduct

By participating in this project, you agree to maintain a respectful and collaborative environment.

## How to Contribute

### Reporting Issues

-   Check existing issues before creating a new one
-   Use clear, descriptive titles
-   Include relevant details: workflow name, error messages, expected vs actual behavior
-   Provide reproduction steps when applicable

### Proposing Changes

1. **Fork the repository** and create a new branch
2. **Make your changes** following the guidelines below
3. **Test thoroughly** in a separate test repository
4. **Submit a pull request** with a clear description

### Pull Request Guidelines

-   Follow conventional commit format for PR titles (enforced by CI)
-   Update documentation if adding/changing workflows
-   Include examples of workflow usage
-   Test changes in a real repository before submitting
-   Keep changes focused and atomic

## Workflow Development Guidelines

### Creating a New Reusable Workflow

1. **Add `workflow_call` trigger** to make it reusable:

```yaml
on:
    workflow_call:
        inputs:
            # Define inputs here
        secrets:
            # Define secrets here
```

2. **Document all inputs and secrets** with clear descriptions
3. **Provide usage examples** in README.md
4. **Test in a consumer repository** before merging

### Modifying Existing Workflows

1. **Maintain backward compatibility** when possible
2. **Document breaking changes** in the PR description
3. **Update version appropriately**:
    - Breaking changes → Major version (v2.0.0)
    - New features → Minor version (v1.1.0)
    - Bug fixes → Patch version (v1.0.1)

### Best Practices

-   **Use descriptive job and step names**
-   **Add comments** for complex logic
-   **Implement proper error handling**
-   **Cache dependencies** to improve performance
-   **Use matrix strategies** for parallel execution when applicable
-   **Avoid hardcoded values** - use inputs or secrets
-   **Set appropriate timeouts** to prevent hanging workflows

## Testing Changes

Before submitting a PR:

1. Create a test repository
2. Reference your branch: `uses: your-fork/shared-workflows/.github/workflows/workflow.yml@your-branch`
3. Verify all inputs and secrets work correctly
4. Test edge cases and error conditions
5. Check workflow logs for warnings or issues

## Documentation Updates

When adding or modifying workflows, update:

-   `README.md` - Add/update workflow documentation with usage examples
-   `CHANGELOG.md` - Will be auto-generated on release
-   Inline comments in workflow files for complex logic

## Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:**

-   `feat`: New feature (minor version bump)
-   `fix`: Bug fix (patch version bump)
-   `docs`: Documentation only
-   `chore`: Maintenance tasks
-   `ci`: CI/CD changes
-   `refactor`: Code restructuring
-   `perf`: Performance improvements
-   `test`: Test updates

**Examples:**

-   `feat(playwright): add support for custom browsers`
-   `fix(pr-title): handle special characters correctly`
-   `docs: update playwright workflow examples`

## Release Process

Releases are automated via semantic-release:

1. Merge PR to `main` (triggers release workflow)
2. Semantic-release analyzes commits since last release
3. Version is bumped automatically based on commit types
4. Release notes are generated from commits
5. Git tag is created and pushed

## Questions or Help

If you have questions or need help:

-   Open a discussion in the repository
-   Review existing documentation in README.md and VERSIONING.md
-   Check closed PRs for similar changes

Thank you for contributing! 🎉
