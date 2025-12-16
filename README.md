# Shared Workflows

Centralized reusable GitHub Actions workflows for CI/CD automation across multiple repositories.

## Table of Contents

-   [Quick Start](#quick-start)
-   [Repository Structure](#repository-structure)
-   [Reusable Workflows](#reusable-workflows)
    -   [Playwright Tests](#1-playwright-tests-playwrightyml)
    -   [PR Title Check](#2-pr-title-check-pr-title-checkyml)
-   [Internal Workflows](#internal-workflows)
-   [Versioning](#versioning)
-   [Contributing](#contributing)
-   [Security](#security)
-   [License](#license)

## Quick Start

To use these workflows in your repository:

1. Reference the workflow using the format: `acahet/shared-workflows/.github/workflows/<workflow-name>.yml@v1`
2. Pass required inputs and secrets
3. Ensure your repository has the necessary secrets configured

## Repository Structure

```
shared-workflows/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       ├── playwright.yml        # Reusable: Playwright tests
│       ├── pr-title-check.yml    # Reusable: PR title validation
│       ├── release.yml           # Internal: Semantic releases
│       └── update-changelog.yml  # Internal: Changelog automation
├── .releaserc.json
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── SECURITY.md
└── VERSIONING.md
```

## Reusable Workflows

These workflows can be called from other repositories.

### 1. Playwright Tests (`playwright.yml`)

Executes Playwright UI and/or API tests with configurable Node.js versions and test types.

**Usage:**

```yaml
name: Run Tests
on:
    push:
        branches: [main]
    pull_request:
        branches: [main]

jobs:
    test:
        uses: acahet/shared-workflows/.github/workflows/playwright.yml@v1
        with:
            run-api-tests: true
            run-ui-tests: true
            node-version: '20'
        secrets:
            EMAIL_API: ${{ secrets.EMAIL_API }}
            PASSWORD_API: ${{ secrets.PASSWORD_API }}
            API_URL: ${{ secrets.API_URL }}
```

**Inputs:**

-   `run-api-tests` (boolean, required): Enable API tests
-   `run-ui-tests` (boolean, required): Enable UI tests
-   `node-version` (string, optional): Node.js version (default: `lts/*`)

**Required Secrets:**

-   `EMAIL_API`: API authentication email
-   `PASSWORD_API`: API authentication password
-   `API_URL`: Base URL for API endpoints

**Features:**

-   Dependency caching for faster runs
-   Parallel test execution support
-   Automatic Playwright browser installation
-   Test result artifacts and HTML reports

### 2. PR Title Check (`pr-title-check.yml`)

Enforces conventional commit format for pull request titles to maintain consistent commit history and enable automated semantic versioning.

**Usage:**

```yaml
name: Check PR Title
on:
    pull_request:
        types: [opened, edited, synchronize, reopened]

permissions:
    contents: read
    pull-requests: read

jobs:
    lint-pr-title:
        uses: acahet/shared-workflows/.github/workflows/pr-title-check.yml@v1
        secrets: inherit
```

**Supported Commit Types:**

| Type       | Description              | Version Bump |
| ---------- | ------------------------ | ------------ |
| `feat`     | New feature              | Minor        |
| `fix`      | Bug fix                  | Patch        |
| `chore`    | Maintenance tasks        | None         |
| `build`    | Build system changes     | None         |
| `ci`       | CI configuration changes | None         |
| `docs`     | Documentation updates    | None         |
| `style`    | Code style changes       | None         |
| `refactor` | Code refactoring         | None         |
| `perf`     | Performance improvements | Patch        |
| `test`     | Test updates             | None         |

**Examples:**

-   ✅ `feat: add user authentication`
-   ✅ `fix: resolve memory leak in cache`
-   ✅ `docs: update API documentation`
-   ❌ `Update readme` (missing type)
-   ❌ `feature: new login` (wrong type)

## Internal Workflows

These workflows run automatically within the shared-workflows repository and are not designed to be called externally.

### Release (`release.yml`)

Automatically creates semantic version releases based on conventional commits when workflow changes are pushed to `main`.

**Trigger:** Push to `main` branch with changes to `.github/workflows/*.yml`

### Update Changelog (`update-changelog.yml`)

Automatically generates and commits changelog updates when version tags are created.

**Trigger:** Push of version tags matching `v*.*.*` or `v*.*.*-*`

## Versioning

This repository follows [Semantic Versioning](https://semver.org/):

-   **Major (v1.0.0)**: Breaking changes to workflow inputs/outputs
-   **Minor (v1.1.0)**: New features, backward compatible
-   **Patch (v1.0.1)**: Bug fixes, backward compatible
## Contributing

We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for:

-   How to report bugs and request features
-   Development guidelines and best practices
-   Pull request process and requirements
-   Testing guidelines

## Security

Security is a priority. Please review [SECURITY.md](SECURITY.md) for:

-   How to report security vulnerabilities
-   Security best practices for workflow usage
-   Supported versions and update policy

##

See [VERSIONING.md](VERSIONING.md) for detailed versioning guidelines.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for complete release history and breaking changes.

## License

See [LICENSE](LICENSE) file for details.
