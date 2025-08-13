```
README.md

# CI-demo

This project demonstrates how to achieve Continuous Integration (CI) using GitHub Actions and Python unit testing.

## Continuous Integration with GitHub Actions

The repository is configured with a GitHub Actions workflow that automatically runs unit tests whenever code is pushed or a pull request is created. This ensures that all code changes are tested before being merged, improving code quality and reliability.

### How CI is Achieved

1. **GitHub Actions Workflow**  
    A YAML workflow file (e.g., `.github/workflows/ci.yml`) is set up in the repository. This file defines the steps to install dependencies and run tests.

    - Example:  
      ```yaml
      name: CI
      on: [push, pull_request]
      jobs:
        build:
          runs-on: ubuntu-latest
          steps:
            - uses: actions/checkout@v3
            - name: Set up Python
              uses: actions/setup-python@v4
              with:
                python-version: '3.10'
      ```

2. **Automatic Triggers**  
    The workflow is triggered on `push` and `pull_request` events, so tests run automatically on every code change.

    - No manual commands needed; GitHub Actions handles this based on the workflow configuration.

3. **Install Dependencies**  
    The workflow installs your project dependencies, typically using `pip`.

    - Example command in the workflow:  
      ```yaml
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      ```

4. **Unit Testing**  
    The project uses Python's built-in `unittest` framework to write and run tests. The workflow executes these tests to verify the correctness of the code.

    - Example command in the workflow:  
      ```yaml
      - name: Run tests
        run: |
          python -m unittest discover
      ```

## Example Workflow File

```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Run tests
        run: |
          python -m unittest discover
```