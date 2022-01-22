# workflows.php
Default workflos for php projects

## Available Workflows

### CI

Validates composer.json and runs the CI pipelines to verify the project is working correctly. The workflow supports building a matrix of php versions and stabilities. By default prefer-lowest and prefer-stable are tested with all given php versions which should cover most of the package ranges. 

#### Inputs
    php-versions:
      description: 'The php versions to test as JSON array. Will be converted and used to create a matrix.'
      default: '["8.1"]'
      required: true
      type: string
    prefer-stability:
      description: 'The staibility of the packages to use. Will be converted and used to create a matrix.'
      default: '["prefer-lowest", "prefer-stable"]'
      type: string
    test-command:
      description: 'The command to run for executing tests'
      default: 'composer ci-all'
      type: string

#### Example

```yaml

name: CI

on:
  push:
    branches:
      - main
      - release
    paths-ignore:
      - '**.md'
  pull_request:
    branches:
      - main
      - release
    paths-ignore:
      - '**.md'

jobs:
  ci:
    uses: codenamephp/workflows.php/.github/workflows/ci.yml@main
    with:
      php-versions: '["8.1", "8.0"]'
```
