# codacy-analysis-cli action

> 🤖 Automate Codacy static analysis

This action run the [codacy-analysis-cli](https://github.com/codacy/codacy-analysis-cli) for all commits and pull requests with your Codacy configuration.

## Usage

Create a new workflow `.yml` file in the `.github/workflows/` directory.

### .github/workflows/codacy-analysis-cli.yml

```yml
name: codacy-analysis-cli

on: ["push", "pull_request"]

jobs:
  codacy-analysis-cli:
    runs-on: ubuntu-latest
    name: codacy-analysis-cli
    steps:
      - uses: actions/checkout@master
      - name: Run codacy-analysis-cli
        uses: mrfyda/codacy-analysis-cli-action@action
        with:
          project-token: ${{ secrets.CODACY_PROJECT_TOKEN }}
```

## Workflow options

Change these options in the workflow `.yml` file to meet your GitHub project needs.

| Setting         | Description           | Values                                |
| --------------- | --------------------- | ------------------------------------- |
| `project-token` | The project API token | `${{ secrets.CODACY_PROJECT_TOKEN }}` |
