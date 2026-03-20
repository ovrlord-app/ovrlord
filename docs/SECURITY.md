# Security Policy

## Supported Versions

| Version | Supported          |
|---------|--------------------|
| 1.x.x   | :white_check_mark: |
| < 1.x.x | :x:                |

## Reporting a Vulnerability

Send vulnerability details to [admin@ovrlord.dev](mailto:admin@ovrlord.dev) and please refrain from posting an
issue with the details until they can be reviewed by a maintainer of this repository.
If a vulnerability is confirmed a CVE will be opened with GitHub and the fix released as quickly as possible based on
severity of the issue.

## Vulnerability Scanning

Ovrlord runs automated vulnerability scanning in GitHub Actions workflows for all pull requests and commits to the `main` branch.
The current toolset includes `govulncheck` though is subject to change at any time.