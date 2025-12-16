# Security Policy

## Supported Versions

We actively maintain and provide security updates for the following versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.x     | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

We take security seriously. If you discover a security vulnerability, please follow these steps:

### 1. Do Not Open a Public Issue

Please **do not** create a public GitHub issue for security vulnerabilities. This helps protect users while a fix is being developed.

### 2. Report Privately

Send an email to the repository maintainers with:

-   **Description** of the vulnerability
-   **Steps to reproduce** the issue
-   **Potential impact** assessment
-   **Suggested fix** (if you have one)

### 3. Response Timeline

-   **Initial response**: Within 48 hours
-   **Status update**: Within 7 days
-   **Fix timeline**: Depends on severity, typically 14-30 days

### 4. Coordinated Disclosure

We practice coordinated disclosure:

1. We'll acknowledge your report
2. We'll investigate and develop a fix
3. We'll release the security patch
4. We'll publish a security advisory
5. We may credit you in the advisory (with your permission)

## Security Best Practices for Workflow Users

### Secrets Management

1. **Never hardcode secrets** in workflow files
2. **Use GitHub Secrets** for sensitive data
3. **Limit secret scope** to specific workflows when possible
4. **Rotate secrets regularly**
5. **Use least-privilege access** for tokens

### Workflow Permissions

1. **Explicitly define permissions** in workflows:

```yaml
permissions:
    contents: read
    pull-requests: read
```

2. **Avoid `permissions: write-all`**
3. **Review third-party actions** before use
4. **Pin action versions** to specific commits or tags

### Dependency Security

1. **Keep workflows updated** to the latest version
2. **Monitor for security advisories**
3. **Review workflow changes** in release notes
4. **Test updates** in a non-production environment first

### Third-Party Actions

Our workflows use these trusted third-party actions:

-   `actions/checkout` - Official GitHub action
-   `actions/cache` - Official GitHub action
-   `actions/setup-node` - Official GitHub action
-   `amannn/action-semantic-pull-request` - Well-maintained, 1M+ downloads
-   `cycjimmy/semantic-release-action` - Popular semantic-release wrapper
-   `requarks/changelog-action` - Maintained changelog generator
-   `stefanzweifel/git-auto-commit-action` - Popular auto-commit tool

We regularly review and update these dependencies.

## Security Considerations

### Workflow Execution

-   Workflows run in isolated GitHub-hosted runners
-   Each job runs in a fresh virtual environment
-   No persistent state between workflow runs
-   Secrets are masked in logs automatically

### Input Validation

Our workflows validate inputs to prevent:

-   Command injection
-   Path traversal
-   Unauthorized access
-   Resource exhaustion

### Network Security

-   Workflows only connect to trusted endpoints
-   No external data exfiltration
-   All GitHub API calls use authenticated requests

## Known Limitations

1. **Secrets in fork PRs**: GitHub does not expose secrets to workflows triggered by forks. This is a security feature.
2. **Workflow logs**: While secrets are masked, be careful about logging sensitive data structures.
3. **Third-party actions**: We cannot guarantee the security of third-party actions beyond our review process.

## Security Updates

Security updates are released as:

-   **Critical**: Immediate patch release
-   **High**: Release within 7 days
-   **Medium**: Release within 30 days
-   **Low**: Included in next regular release

All security updates will be documented in:

-   CHANGELOG.md
-   GitHub Security Advisories
-   Release notes

## Compliance

This project follows:

-   GitHub's security best practices
-   OWASP secure coding guidelines
-   Principle of least privilege
-   Defense in depth strategy

## Questions

For security-related questions that are not vulnerabilities, you may open a public discussion in the repository.

---

**Thank you for helping keep this project secure!**
