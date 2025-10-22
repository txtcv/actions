# txtcv actions

This repository provides a GitHub Action that installs the
[`txtcv`](https://github.com/txtcv/cli) command-line tool via the official Homebrew tap
and provides a few utilities on top of it.

## Usage

### Validation

The `validate` workflow lets you validate JSON Resume CV files. Here's an example:

```yaml
name: Validate CV

on:
  push:
    paths:
      - cv.json
  pull_request:
    paths:
      - cv.json

jobs:
  validate:
    runs-on: ubuntu-latest
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v4

      - name: Validate CV
        uses: txtcv/actions@main
        with:
          cv-path: cv.json
```

## Notes

- Homebrew must be available on the runner. GitHub-hosted macOS and Ubuntu runners
  include Homebrew by default; ensure it is available on self-hosted runners before
  using this action.
- The action installs or upgrades the latest formula from `txtcv/tap`; pinning to a
  specific release is not currently supported through Homebrew.
- The action currently targets Linux and macOS runners. Ensure a matching Homebrew
  bottle exists before enabling it on Windows.
