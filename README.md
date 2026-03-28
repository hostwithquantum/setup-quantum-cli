# setup-quantum-cli

[![CI](https://github.com/hostwithquantum/setup-quantum-cli/actions/workflows/ci.yml/badge.svg)](https://github.com/hostwithquantum/setup-quantum-cli/actions/workflows/ci.yml)
[![GitHub Action](https://img.shields.io/badge/GitHub-Action-blue?logo=github)](https://github.com/hostwithquantum/setup-quantum-cli)
[![License: MPL 2.0](https://img.shields.io/badge/License-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)

A GitHub Action to install and configure [`quantum-cli`](https://cli.planetary-quantum.com) for use in your CI/CD workflows. This action downloads the CLI, adds it to your PATH, and sets up authentication automatically.

## Prerequisites

- A [Planetary Quantum](https://www.planetary-quantum.com/) account with valid credentials

## Supported platforms

| OS | Architecture |
|----|--------------|
| Linux | amd64, arm64 |
| macOS | amd64, arm64 |
| Windows | amd64, arm64 |

## Inputs

You should provide an `api-key`, but it's optional.

| Input | Description |  |
|-------|-------------|----------|
| `api-key` | Your Quantum API key | optional |
| `version` | The version | optional, defaults to latest |

## Usage

For detailed documentation on the `quantum-cli`, please refer to our [docs](https://docs.planetary-quantum.com/).

### Quickstart

```yaml
steps:
  - uses: hostwithquantum/setup-quantum-cli@v2
    with:
      api-key: ${{ secrets.QUANTUM_API_KEY }}
  - run: quantum-cli auth status
```

### Full workflow example

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: hostwithquantum/setup-quantum-cli@v2
        with:
          api-key: ${{ secrets.QUANTUM_API_KEY }}
      - run: quantum-cli auth status
      - run: quantum-cli stack deploy
        env:
          QUANTUM_ENDPOINT: my-cluster
          QUANTUM_STACK: my-app
```

### Windows example

```yaml
jobs:
  deploy:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v6
      - uses: hostwithquantum/setup-quantum-cli@v2
        with:
          api-key: ${{ secrets.QUANTUM_API_KEY }}
      - run: quantum-cli.exe auth status
```

## Environment variables

The action sets the following environment variables for subsequent steps:

When using API key:
- `QUANTUM_API_KEY` — your API key

## Dependencies

- `bash`
- `curl`
- `sha256sum`

## License

MPL-2.0
