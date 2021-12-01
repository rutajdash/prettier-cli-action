# Prettier CLI Check

A GitHub action to run [Prettier](https://prettier.io/) CLI Checks. This project was **heavily** inspired by other actions available and a shoutout to [@creyD](https://github.com/creyD). The goal of this project was to create a simple action which would be easy to use.

[![Code Style][code-style-shield]][code-style-url]
[![Latest Release][release-shield]][release-url]
[![MIT License][license-shield]][license-url]
[![Issues][issues-shield]][issues-url]
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]

## Usage

### Parameters

| Parameter        |        Default        | Description                                                                                                                                                     |
| ---------------- | :-------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| file_pattern     |      `'**/*.js'`      | The file pattern prettier will check. Follow [glob syntax](https://github.com/mrmlnc/fast-glob#pattern-syntax).                                                 |
| config_path      |         `''`          | The path to the `prettierrc` file. Read more [here](https://prettier.io/docs/en/configuration.html).                                                            |
| ignore_path      | `'./.prettierignore'` | The path to the `prettierignore` file. This file should list file patterns to skip using the [glob syntax](https://github.com/mrmlnc/fast-glob#pattern-syntax). |
| prettier_version |      `'latest'`       | The version of prettier to use. Find versions [here](https://www.npmjs.com/package/prettier?activeTab=versions).                                                |
| fail_on_error    |        `true`         | Whether the action should fail if prettier finds errors in formatting.                                                                                          |

### Output

You can access the list of files prettier found errors using the actions context like `steps.<step-id>.outputs.prettier_output`. The returned value is a list of files as a string, one per line.

### Examples

```yaml
name: Continuous Integration

# This action works with pull requests and pushes on the main branch
on:
  pull_request:
  push:
    branches: [main]

jobs:
  prettier:
    name: Prettier Check
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Run Prettier
        id: prettier-run
        uses: rutajdash/prettier-cli-action@v1.0.0
        with:
          config_path: ./.prettierrc.yml

      # This step only runs if prettier finds errors causing the previous step to fail
      # This steps lists the files where errors were found
      - name: Prettier Output
        if: ${{ failure() }}
        shell: bash
        run: |
          echo "The following files are not formatted:"
          echo "${{steps.prettier-run.outputs.prettier_output}}"
```

More documentation for writing a workflow can be found [here](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions).

## Issues

Please report all bugs and feature requests using the [GitHub issues function](https://github.com/rutajdash/prettier-cli-action/issues/new/choose). Thanks!

## Contributing

Pull Requests are always welcome! Feel free to pick any [issue][issues-url] or raise a new [feature request][feature-request-url]!
Do read the [contributing guidelines][contributing-guidelines-url] and [code of conduct][code-of-conduct-url].

[code-style-shield]: https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=plastic
[code-style-url]: https://github.com/prettier/prettier
[release-shield]: https://img.shields.io/github/v/release/rutajdash/prettier-cli-action?style=plastic
[release-url]: https://github.com/rutajdash/prettier-cli-actions/releases
[contributors-shield]: https://img.shields.io/github/contributors/rutajdash/prettier-cli-action?style=plastic
[contributors-url]: https://github.com/rutajdash/prettier-cli-action/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/rutajdash/prettier-cli-action?style=plastic
[forks-url]: https://github.com/rutajdash/prettier-cli-action/network/members
[stars-shield]: https://img.shields.io/github/stars/rutajdash/prettier-cli-action?style=plastic
[stars-url]: https://github.com/rutajdash/prettier-cli-action/stargazers
[issues-shield]: https://img.shields.io/github/issues/rutajdash/prettier-cli-action?style=plastic
[issues-url]: https://github.com/rutajdash/prettier-cli-action/issues
[feature-request-url]: https://github.com/rutajdash/prettier-cli-action/issues/new?assignees=&labels=enhancement&template=feature_request.md&title=feat%3A
[license-shield]: https://img.shields.io/github/license/rutajdash/prettier-cli-action?style=plastic
[license-url]: https://github.com/rutajdash/prettier-cli-action/blob/main/LICENSE
[contributing-guidelines-url]: https://github.com/rutajdash/prettier-cli-action/blob/main/CONTRIBUTING.md
[code-of-conduct-url]: https://github.com/rutajdash/prettier-cli-action/blob/main/CODE_OF_CONDUCT.md
