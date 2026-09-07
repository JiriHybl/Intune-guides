# Contributing to Intune Guides

Thank you for your interest in contributing! This project welcomes contributions in the form of new guides, corrections, improvements, and translations.

## Contributor License Agreement

Most contributions require you to agree to a Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit [https://cla.opensource.microsoft.com](https://cla.opensource.microsoft.com).

When you submit a pull request, a CLA bot will automatically determine whether you need to provide a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repos using our CLA.

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](../../issues) to report errors, unclear steps, or outdated information.
- Include the guide name, section, and a clear description of the problem.

### Submitting a Pull Request

1. Fork this repository.
2. Create a new branch: `git checkout -b fix/your-description`.
3. Make your changes following the [style guide](#style-guide) below.
4. Commit your changes with a clear message.
5. Push to your fork and open a Pull Request against `main`.

### Style Guide

- Write in clear, plain English.
- Use numbered steps for sequential instructions.
- Use screenshots sparingly — only when a visual is essential.
- Store guides under `docs/<workload>/<scenario>/` (e.g., `docs/app-protection/mam-without-enrollment/`).
- Use lowercase, hyphen-separated filenames (e.g., `admin-guide.md`, `user-guide.md`, `deployment-plan.md`).
- Use [`templates/guide-template.md`](templates/guide-template.md) as the starting point for new guides.
- Include the standard guide metadata: audience, platform, Intune workload, last-reviewed date, and status.
- Label content clearly for its intended audience: **Admin** or **End User**.
- Keep platform-specific instructions (iOS, Android, Windows) clearly separated.

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). By participating, you are expected to uphold this code. Please report unacceptable behavior to [opencode@microsoft.com](mailto:opencode@microsoft.com).
