# Swift Package Resolve Check Pre-commit Hook

This repository provides a pre-commit hook to ensure your Swift project's `Package.resolved` file stays consistent and up-to-date.

## What does it do?

The `swift-resolve-check` hook runs `swift package resolve` and checks if your `Package.resolved` file changes as a result. It can either:
- **Fail** (default): Block the commit if `Package.resolved` changes after resolving dependencies.
- **Update**: Automatically update `Package.resolved` and allow the commit to proceed.

It supports custom package paths and custom Swift executables.

## Installation

1. **Install [pre-commit](https://pre-commit.com/):**
   ```sh
   pip install pre-commit
   ```

2. **Add this hook to your `.pre-commit-config.yaml`:**
   ```yaml
   - repo: https://github.com/noahkamara/swift-resolve-check
     rev: v0.1.0
     hooks:
       - id: swift-resolve-check
         # Optionally pass args, e.g. --update or --package-path ExamplePackage
         # args: [--update]
   ```

3. **Install the hooks:**
   ```sh
   pre-commit install
   ```

## Usage

By default, the hook will block commits if `Package.resolved` changes after running `swift package resolve`. You can configure the behavior:

- **Fail on change (default):**
  ```sh
  git commit
  # If Package.resolved changes, the commit is blocked.
  ```
- **Auto-update on change:**
  In your `.pre-commit-config.yaml`:
  ```yaml
  - repo: local
    hooks:
      - id: swift-resolve-check
        args: [--update]
  ```

- **Custom package path or Swift executable:**
  ```yaml
  - repo: local
    hooks:
      - id: swift-resolve-check
        args: [--package-path, DocsyLib, --swift, /path/to/swift]
  ```

## Run

- Run the hook:
  ```sh
  pre-commit run swift-resolve-check
  ```

## More info

See [pre-commit.com](https://pre-commit.com/) for more details on configuring and using pre-commit hooks. 
