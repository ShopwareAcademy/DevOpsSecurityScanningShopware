# DevOpsSecurityScanningShopware

This project is part of the **DevOps** learning path of the Shopware Academy.

It shows the prepared reference project state for the practical lab **Extending a QA Pipeline With Security Scanning**.

It demonstrates how to:

- Start from a real Shopware project repository.
- Keep local environment files and generated runtime files out of Git.
- Provide a committed `composer.lock` file for Composer security audits.
- Prepare the repository for GitHub Actions security workflows.

Tested for **Shopware 6.7**.

## Reference Project

This repository is an educational reference state for the Academy practical lab. It is meant for comparing your local setup with a known project state before you add the GitHub Actions workflow files.

You do not need to run this project locally to use it as a reference. The most important files and folders to compare before starting the workflow steps are:

- `composer.json`
- `composer.lock`
- `.gitignore`
- `bin/`
- `config/`
- `custom/`
- `public/`
- `src/`

The GitHub Actions workflow files are intentionally not part of this initial setup state yet. In the learning unit, you create them step by step at the project root under `.github/workflows/`.

This repository is not a production template. The project structure and credentials are intentionally simple for local learning.

## Environment Files

The generated `.env` file is not committed because it contains local values such as `APP_SECRET`, `INSTANCE_ID`, and `DATABASE_URL`.

The repository keeps `.env` ignored. The security workflows in the learning unit use repository files, lock files, and configured image names. They do not need your local `.env`.

## Security Workflow Steps

The learning unit adds the workflow files in this order:

- `.github/workflows/security-smoke-test.yml`
- `.github/workflows/container-scan.yml`
- `.github/workflows/dependency-audits.yml`
- `.github/workflows/scheduled-security-checks.yml`
- `.github/workflows/container-scan-gate.yml`

Each workflow has one responsibility. This keeps the lab easy to inspect in the GitHub **Actions** tab.

The final `container-scan-gate.yml` workflow can fail when Trivy finds high or critical vulnerabilities. In this lab, that failure is expected because the workflow demonstrates what a blocking security gate looks like.

## Optional: Run the Project Locally

This reference project is mainly intended for comparison. You do not need to run it locally to follow the GitHub Actions lab.

If you want to run it locally, create your own local `.env` first and use the generated Shopware Docker development commands from this project, for example:

```bash
make up
make setup
```

The exact local runtime depends on your Docker setup and the generated Shopware development configuration.

## License

MIT License.

You may use this project in commercial and professional projects.
It is provided as an educational example and comes without a warranty and without support.

## Contributing

This project is part of the Shopware Academy curriculum.
