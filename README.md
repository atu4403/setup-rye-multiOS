# setup-rye-multiOS

GitHub Action to set up a Rye environment across multiple operating systems (Linux, macOS, and Windows).

## Features

- Sets up Rye on Linux, macOS, and Windows.
- Allows specifying the Python version to use with Rye.

## Usage

To use this action, create a `.github/workflows` directory in your GitHub repository if it doesn't exist. Then, create a new YAML file (e.g., `setup-rye-workflow.yml`) inside that directory and add the following content:

### Example Workflow

Here is an example workflow that sets up Rye and runs tests using pytest on Ubuntu and macOS for multiple Python versions.

```yaml
name: Run pytest

on:
  push:
    branches:
      - '*'
  pull_request:
    branches:
      - '*'

jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
        python-version: ['3.8', '3.11']
    steps:
    - name: Checkout code
      uses: actions/checkout@v3
    - name: Set up rye
      uses: atu4403/setup-rye-multiOS@v1
    - name: Sync dependencies using rye
      run: |
        rye pin ${{ matrix.python-version }}
        rye sync
    - name: Run tests with pytest
      run: rye run pytest
```

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

## License

[MIT License](LICENSE)
