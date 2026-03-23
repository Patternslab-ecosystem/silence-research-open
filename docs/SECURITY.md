# Security Policy

## Supported Versions

`silence-research-open` is a documentation repository. It does not ship executable code. Security vulnerabilities in the conventional sense (CVEs, injection flaws, etc.) do not apply to this repository's content.

However, the following security-relevant concerns are in scope:

| Concern | In Scope |
|---|---|
| Exposure of PII in committed documents | Yes |
| Incorrect compliance information creating legal risk | Yes |
| CI workflow vulnerabilities (GitHub Actions) | Yes |
| Dependency vulnerabilities (GitHub Actions versions) | Yes |

## Reporting a Vulnerability

If you discover a security concern in this repository — including PII in committed files, a CI workflow that could be exploited, or a compliance misrepresentation with legal consequences — please report it responsibly.

**Do not open a public GitHub Issue for security concerns.**

Report security issues by emailing: **globalzapasowe@gmail.com**

Please include:
- A description of the concern
- The specific file(s) affected
- The potential impact
- Any suggested remediation

We will acknowledge receipt within 2 business days and provide a resolution timeline within 5 business days.

## PII Incident Response

If a file containing personally identifiable information is discovered in the repository history:

1. **Do not attempt to use or share the PII**
2. Report immediately to globalzapasowe@gmail.com with subject line: `[PII INCIDENT] silence-research-open`
3. We will force-push to remove the PII from history and rotate any exposed credentials within 24 hours
4. An incident report will be published in this repository following resolution

## GitHub Actions Security

- All GitHub Actions are pinned to specific versions via dependabot
- Third-party actions are limited to well-maintained, widely-audited actions
- Secrets are never logged or exposed in workflow output
- The GITHUB_TOKEN is scoped to minimum required permissions per workflow

## Disclosure Policy

We support responsible disclosure. If you report a legitimate security concern, we commit to:

- Acknowledging your report within 2 business days
- Keeping you informed of our remediation progress
- Crediting your discovery in the resolution commit message (unless you prefer anonymity)
- Not pursuing legal action against good-faith security researchers
