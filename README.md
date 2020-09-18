# GitHub Action for Codacy Analysis CLI

This is a GitHub Action for invoking the [Codacy Analysis CLI](https://github.com/codacy/codacy-analysis-cli) and returning identified issues in the code.

## GitHub Action

The following is an example of a workflow using the CLI as an action,
to analyse each commit and pull request.

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

- Analyse the current commit or pull request running all supported tools, with the default configuration,
  for the languages you are using.
- Print analysis results into the console (you can check them in GitHub's action workflow panel).
- Fail the workflow if at least one issue is found in your code.

Check the next section to see how you can further configure this action.

### Caveats

This action supports all [CLI configuration options](https://github.com/codacy/codacy-analysis-cli#commands-and-configuration) with the following exceptions:

- `--commit-uuid` -- **Not supported**. The action will only analyse the commit that triggered it.
- `--api-token` -- **Not supported**. Use [`--project-token`](https://github.com/codacy/codacy-analysis-cli#project-token) instead.
- `--username` -- **Not supported**. Use [`--project-token`](https://github.com/codacy/codacy-analysis-cli#project-token) instead.
- `--project` -- **Not supported**. Use [`--project-token`](https://github.com/codacy/codacy-analysis-cli#project-token) instead.

The command `validate-configuration` is also **not supported**.

When using `--project-token` make sure to use [GitHub security features](https://docs.github.com/en/actions/reference/encrypted-secrets)
to prevent you from committing a secret token to your code. For example, if you store your Codacy project
token in GitHub, this is how you would use it in the action workflow.

```yaml
# ...
uses: codacy/codacy-analysis-cli-action@master
with:
    project-token: ${{ secrets.<PROJECT_TOKEN_NAME> }}
# ...
```

## Contributing

We love contributions, feedback, and bug reports.
For issues with the invocation of this action,
file [issues](https://github.com/codacy/codacy-analysis-cli-action/issues) in this repository.


## More Information

For documentation on Codacy itself, including policy language and capabilities see the [Codacy Documentation](https://docs.codacy.com)
