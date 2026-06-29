# DevOpsSecurityScanningShopware

This project is part of the **DevOps** learning path of the Shopware Academy.

It shows the reference project state after the practical lab **Extending a QA Pipeline With Security Scanning**.

It demonstrates how to:

- Create separate GitHub Actions workflow files for security checks.
- Add a small smoke-test workflow before adding security tools.
- Scan a Shopware-related container image with Trivy.
- Run PHP and Node dependency audits with `composer audit` and `npm audit`.
- Run recurring security checks with a scheduled workflow.
- Compare informational baseline scans with a blocking gate workflow.

Tested for **Shopware 6.7**.

## Reference Project

This repository is an educational reference state for the Academy practical lab. It is meant for comparing your local result with a known working project state.

You do not need to run this project to use it as a reference. The most important files to compare are:

- `.github/workflows/security-smoke-test.yml`
- `.github/workflows/container-scan.yml`
- `.github/workflows/dependency-audits.yml`
- `.github/workflows/scheduled-security-checks.yml`
- `.github/workflows/container-scan-gate.yml`

These files show the expected GitHub Actions workflow structure at the end of the lab.

The repository is not a production template. The workflow files are intentionally split into small learning steps so that each security concern is easy to inspect in the GitHub **Actions** tab.

## Workflow Overview

The workflow files have different responsibilities:

- `security-smoke-test.yml` verifies that GitHub Actions can start a workflow and run a simple command.
- `container-scan.yml` runs an informational Trivy scan against the configured Shopware CI image.
- `dependency-audits.yml` runs `composer audit` and `npm audit` when matching lock files or package directories exist.
- `scheduled-security-checks.yml` repeats the same security checks on a schedule and can also be started manually.
- `container-scan-gate.yml` demonstrates how a Trivy scan becomes a blocking gate by using `exit-code: "1"`.

The `container-scan-gate.yml` workflow can fail when Trivy finds high or critical vulnerabilities. In this lab, that failure is expected because the workflow demonstrates what a blocking security gate looks like.

## Optional: Run the Workflows

If you want to run the workflows yourself, push this repository to GitHub and open the **Actions** tab.

Most workflows run on `push`, `pull_request`, and manual `workflow_dispatch` events. The scheduled workflow runs once per day at `02:00 UTC` and can also be started manually.

The dependency audit workflow is intentionally tolerant:

- If `composer.lock` does not exist, the Composer audit job exits without failing.
- If the configured `NPM_AUDIT_DIR` does not exist, the npm audit job exits without failing.
- If findings are reported, the baseline audit commands keep the first run non-blocking.

If your project uses a different Node dependency directory, adjust `NPM_AUDIT_DIR` in:

- `.github/workflows/dependency-audits.yml`
- `.github/workflows/scheduled-security-checks.yml`

## License

MIT License.

You may use this project in commercial and professional projects.
It is provided as an educational example and comes without a warranty and without support.

## Contributing

This project is part of the Shopware Academy curriculum.
