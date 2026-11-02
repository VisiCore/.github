# .github

*Community health files and shared workflows for the [@VisiCore](https://github.com/VisiCore) organization*

For more information, please see the article on [creating a default community health file for your organization](https://help.github.com/en/articles/creating-a-default-community-health-file-for-your-organization).

---

## Organization Reusable Workflows

### OpenTofu CI (`opentofu.yml`)

A self-contained, minimal reusable workflow for validating, formatting, testing, and linting OpenTofu configurations across VisiCore infrastructure repositories.

#### Usage

In your repository (e.g. `.github/workflows/tofu-ci.yml`):

```yaml
name: OpenTofu CI

on:
  pull_request:
    branches: [main]
  push:
    branches: [main]

permissions:
  contents: read

jobs:
  opentofu:
    uses: VisiCore/.github/.github/workflows/opentofu.yml@main
    with:
      run_test: true
      run_tflint: true
```

#### Inputs

| Input | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| `working_directory` | Directory to execute OpenTofu commands in | string | `.` |
| `run_fmt` | Run `tofu fmt -check -recursive` | boolean | `true` |
| `run_validate` | Run `tofu validate -no-color` | boolean | `true` |
| `run_test` | Run `tofu test -no-color` | boolean | `true` |
| `run_tflint` | Run `tflint` if `.tflint.hcl` is present | boolean | `true` |
| `tofu_version` | OpenTofu version to install | string | `1.10.0` |
| `tflint_version` | TFLint version to install | string | `v0.55.0` |
