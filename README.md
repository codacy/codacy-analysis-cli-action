# Codacy GitHub Action

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/946b78614f154f81b1c9c0514fd9f35c)](https://www.codacy.com/gh/codacy/codacy-analysis-cli-action/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=codacy/codacy-analysis-cli-action&amp;utm_campaign=Badge_Grade)

GitHub Action for running Codacy static analysis on over 30 [supported languages](https://docs.codacy.com/getting-started/supported-languages-and-tools/) and returning identified issues in the code.

<br/>

<a href="https://www.codacy.com" target="_blank"><img src="images/codacy-logo.svg" alt="Codacy" width="400"/></a>

<br/>

[Codacy](https://www.codacy.com/) is an automated code review tool that monitors your technical debt, helps you improve your code quality, teaches best practices to your developers, and helps you save time in code reviews:

-   Identify new static analysis issues
-   Commit and pull request analysis with GitHub
-   Auto-comments on commits and pull requests
-   Integrations with Slack and Jira
-   Track issues in Code Style, Security, Error Proneness, Performance, Unused Code and other categories

Codacy also helps keep track of Code Coverage, Code Duplication, and Code Complexity.

Codacy supports PHP, Python, Ruby, Java, JavaScript, and Scala, among others, and is free for Open Source projects.

## GitHub Action

The following is an example GitHub Action workflow that uses the Codacy Analysis CLI
to analyze each commit and pull request.

```yaml
name: codacy-analysis-cli

on: ["push"]

jobs:
  codacy-analysis-cli:
    runs-on: ubuntu-latest
    name: Codacy Analysis CLI
    steps:
      - name: Checkout code
        uses: actions/checkout@master
      - name: Run codacy-analysis-cli
        uses: codacy/codacy-analysis-cli-action@master
```

Running the action with the default configurations will:

- Analyze the current commit or pull request by running all supported static code analysis tools, with their default configurations,
  for the languages you are using.
- Print analysis results on the console, visible on the GitHub Action's workflow panel.
- Fail the workflow if at least one issue is found in your code.

Read the next section to learn how you can further configure this action.

## Extra configurations

The Codacy GitHub Action is a wrapper for running the [Codacy Analysis CLI](https://github.com/codacy/codacy-analysis-cli) and supports the same parameters as the command `analyze`, with the following exceptions:

- `--commit-uuid` (the action always analyzes the commit that triggered it)
- `--api-token`, `--username`, and `--project` (use [`--project-token`](https://github.com/codacy/codacy-analysis-cli#project-token) instead)

When using `--project-token` make sure that you use [GitHub security features](https://docs.github.com/en/actions/reference/encrypted-secrets)
to avoid committing the secret token to your repository. For example, if you store your Codacy project
token in GitHub, this is how you would use it in the action workflow:

```yaml
# ...
uses: codacy/codacy-analysis-cli-action@master
with:
    project-token: ${{ secrets.<PROJECT_TOKEN_NAME> }}
# ...
```

## Contributing

We love contributions, feedback, and bug reports.
If you run into issues while running this action,
[open an issue](https://github.com/codacy/codacy-analysis-cli-action/issues) in this repository.
