# Versioning Guidelines

This repository follows [Semantic Versioning 2.0.0](https://semver.org/) for all releases.

## Version Format

Versions follow the format: **MAJOR.MINOR.PATCH** (e.g., `v1.2.3`)

### Version Components

Given a version number `MAJOR.MINOR.PATCH`:

-   **MAJOR** version increments indicate incompatible API changes (breaking changes)
-   **MINOR** version increments add functionality in a backward compatible manner
-   **PATCH** version increments make backward compatible bug fixes

### Pre-release Versions

Pre-release versions may be denoted by appending a hyphen and a series of dot-separated identifiers:

-   `v1.0.0-alpha.1` - Alpha release
-   `v1.0.0-beta.1` - Beta release
-   `v1.0.0-rc.1` - Release candidate

## What Constitutes a Breaking Change?

For reusable workflows, breaking changes include:

### Input Changes

-   Removing an existing input
-   Changing an input from optional to required
-   Changing the type or format of an input value
-   Renaming an input parameter

### Secret Changes

-   Removing a required secret
-   Adding a new required secret
-   Renaming a secret parameter

### Output Changes

-   Removing an output that workflows depend on
-   Changing the format of an output value

### Behavior Changes

-   Significantly altering workflow execution logic
-   Changing default values that affect existing implementations
-   Modifying job names that other workflows reference

## What is NOT a Breaking Change?

The following changes are backward compatible:

### Minor Version (Feature Additions)

-   Adding new optional inputs
-   Adding new optional secrets
-   Adding new outputs
-   Adding new jobs (that don't affect existing ones)
-   Improving performance without changing behavior
-   Adding new workflow features that are opt-in

### Patch Version (Bug Fixes)

-   Fixing bugs that restore intended behavior
-   Updating dependencies for security patches
-   Improving error messages
-   Documentation improvements
-   Internal refactoring without behavior changes

## Version Tags

This repository maintains the following tags:

-   **Full versions**: `v1.2.3` - Specific release version
-   **Minor versions**: `v1.2` - Points to latest patch in v1.2.x
-   **Major versions**: `v1` - Points to latest minor/patch in v1.x.x

### Recommended Usage

For **stability** (production):

```yaml
uses: acahet/shared-workflows/.github/workflows/playwright.yml@v1.2.3
```

For **latest features** in a major version:

```yaml
uses: acahet/shared-workflows/.github/workflows/playwright.yml@v1
```

For **cutting edge** (not recommended for production):

```yaml
uses: acahet/shared-workflows/.github/workflows/playwright.yml@main
```

## Release Process

Releases are fully automated using semantic-release:

1. **Commit Analysis**: Commits are analyzed for conventional commit types
2. **Version Calculation**: Version bump is determined automatically:
    - `feat:` commits → Minor version bump
    - `fix:` commits → Patch version bump
    - `BREAKING CHANGE:` in footer → Major version bump
3. **Release Creation**: GitHub release is created with auto-generated notes
4. **Tag Creation**: Version tags are created and pushed
5. **Changelog Update**: CHANGELOG.md is automatically updated

## Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

-   `feat`: New feature (→ MINOR version)
-   `fix`: Bug fix (→ PATCH version)
-   `perf`: Performance improvement (→ PATCH version)
-   `docs`: Documentation only
-   `style`: Code style changes (formatting, etc.)
-   `refactor`: Code refactoring
-   `test`: Adding or updating tests
-   `chore`: Maintenance tasks
-   `ci`: CI/CD changes
-   `build`: Build system changes

### Breaking Changes

To indicate a breaking change, add `BREAKING CHANGE:` in the commit footer:

```
feat(playwright): remove node-version input

BREAKING CHANGE: The node-version input has been removed.
Use the default Node.js LTS version instead.
```

Or use `!` after the type/scope:

```
feat!: remove deprecated workflow
```

## Examples

### Patch Release (v1.0.0 → v1.0.1)

```
fix(playwright): handle missing test files gracefully

Previously, the workflow would fail silently when test files
were missing. Now it logs a clear error message.
```

### Minor Release (v1.0.1 → v1.1.0)

```
feat(playwright): add support for custom reporters

Add new optional input 'reporters' to allow users to specify
custom Playwright reporters.
```

### Major Release (v1.1.0 → v2.0.0)

```
feat(playwright)!: require Node.js 20 or higher

BREAKING CHANGE: Node.js 18 is no longer supported.
Workflows must now use Node.js 20 or higher.
```

## Migration Guide

When a breaking change is released:

1. Review the release notes and CHANGELOG.md
2. Identify which inputs/secrets/behaviors changed
3. Update your workflow files accordingly
4. Test in a non-production environment
5. Update your version reference

### Example Migration

**Before (v1.x):**

```yaml
uses: acahet/shared-workflows/.github/workflows/playwright.yml@v1
with:
    run-tests: true # Old input
```

**After (v2.x):**

```yaml
uses: acahet/shared-workflows/.github/workflows/playwright.yml@v2
with:
    run-api-tests: true # New separate inputs
    run-ui-tests: true
```

## Questions?

If you have questions about versioning:

-   Review this document and the CHANGELOG.md
-   Check closed PRs with breaking change labels
-   Open a discussion in the repository
