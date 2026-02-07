# Reusable GitHub Actions Workflows

A collection of reusable GitHub Actions workflows for common development tasks. These workflows can be called from other repositories to standardize CI/CD processes.

## Available Workflows

### 1. CI Workflow (`ci.yml`)

Runs continuous integration tasks including build, lint, and test for multiple languages.

**Supported Languages:**
- Node.js
- Java
- Python
- Go

**Usage Example:**

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  ci:
    uses: jenly1314/actions/.github/workflows/ci.yml@main
    with:
      node-version: '18'
      build-command: 'npm ci && npm run build'
      test-command: 'npm test'
      lint-command: 'npm run lint'
```

**Inputs:**
- `node-version`: Node.js version (default: '18')
- `java-version`: Java version
- `python-version`: Python version
- `go-version`: Go version
- `working-directory`: Working directory (default: '.')
- `build-command`: Build command
- `test-command`: Test command
- `lint-command`: Lint command
- `cache-dependency-path`: Path to dependency file for caching

### 2. Release Workflow (`release.yml`)

Automates the release process including building, packaging, and creating GitHub releases.

**Usage Example:**

```yaml
name: Release

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    uses: jenly1314/actions/.github/workflows/release.yml@main
    with:
      node-version: '18'
      build-command: 'npm ci && npm run build'
      release-command: 'npm publish'
      artifact-path: 'dist/**'
      create-github-release: true
    secrets:
      npm-token: ${{ secrets.NPM_TOKEN }}
```

**Inputs:**
- `node-version`: Node.js version (default: '18')
- `java-version`: Java version
- `python-version`: Python version
- `go-version`: Go version
- `working-directory`: Working directory (default: '.')
- `build-command`: Build command
- `release-command`: Release command
- `artifact-path`: Path to artifacts to upload
- `create-github-release`: Create GitHub release (default: true)

**Secrets:**
- `npm-token`: NPM authentication token
- `pypi-token`: PyPI authentication token

### 3. Security Scan Workflow (`security.yml`)

Performs security scanning using CodeQL and dependency review.

**Usage Example:**

```yaml
name: Security

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 0 * * 0'

jobs:
  security:
    uses: jenly1314/actions/.github/workflows/security.yml@main
    with:
      enable-codeql: true
      enable-dependency-review: true
      codeql-languages: '["javascript", "python"]'
```

**Inputs:**
- `node-version`: Node.js version (default: '18')
- `java-version`: Java version
- `python-version`: Python version
- `working-directory`: Working directory (default: '.')
- `enable-codeql`: Enable CodeQL analysis (default: true)
- `enable-dependency-review`: Enable dependency review (default: true)
- `codeql-languages`: Languages for CodeQL (JSON array format, e.g., '["javascript", "python"]')

### 4. Code Quality Workflow (`code-quality.yml`)

Analyzes code quality and generates coverage reports.

**Usage Example:**

```yaml
name: Code Quality

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  quality:
    uses: jenly1314/actions/.github/workflows/code-quality.yml@main
    with:
      node-version: '18'
      coverage-command: 'npm run test:coverage'
      coverage-path: 'coverage/lcov.info'
      enable-sonarcloud: true
      sonar-project-key: 'my-project'
      sonar-organization: 'my-org'
    secrets:
      sonar-token: ${{ secrets.SONAR_TOKEN }}
```

**Inputs:**
- `node-version`: Node.js version (default: '18')
- `python-version`: Python version
- `working-directory`: Working directory (default: '.')
- `enable-sonarcloud`: Enable SonarCloud (default: false)
- `sonar-project-key`: SonarCloud project key
- `sonar-organization`: SonarCloud organization
- `coverage-command`: Command to generate coverage
- `coverage-path`: Path to coverage report (default: 'coverage/lcov.info')

**Secrets:**
- `sonar-token`: SonarCloud authentication token

### 5. Docker Build Workflow (`docker.yml`)

Builds and pushes Docker images with multi-platform support.

**Usage Example:**

```yaml
name: Docker

on:
  push:
    branches: [ main ]
    tags:
      - 'v*'

jobs:
  docker:
    uses: jenly1314/actions/.github/workflows/docker.yml@main
    with:
      docker-image: 'ghcr.io/${{ github.repository }}'
      dockerfile-path: 'Dockerfile'
      platforms: 'linux/amd64,linux/arm64'
      push: true
    secrets:
      registry-username: ${{ github.actor }}
      registry-password: ${{ secrets.GITHUB_TOKEN }}
```

**Inputs:**
- `docker-image`: Docker image name (required)
- `dockerfile-path`: Path to Dockerfile (default: 'Dockerfile')
- `context`: Build context (default: '.')
- `platforms`: Target platforms (default: 'linux/amd64,linux/arm64')
- `push`: Push to registry (default: false)
- `tags`: Additional tags (comma-separated)
- `build-args`: Build arguments (key=value, newline-separated)

**Secrets:**
- `registry-username`: Docker registry username
- `registry-password`: Docker registry password

## Getting Started

To use these workflows in your repository:

1. Reference the workflow in your `.github/workflows` directory
2. Use the `uses` keyword with the format: `{owner}/{repo}/.github/workflows/{workflow}.yml@{ref}`
3. Pass required inputs and secrets

## Examples

### Node.js Project

```yaml
name: CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  ci:
    uses: jenly1314/actions/.github/workflows/ci.yml@main
    with:
      node-version: '20'
      build-command: 'npm ci && npm run build'
      test-command: 'npm test'
      lint-command: 'npm run lint'
      
  security:
    uses: jenly1314/actions/.github/workflows/security.yml@main
    with:
      codeql-languages: '["javascript"]'
```

### Python Project

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  ci:
    uses: jenly1314/actions/.github/workflows/ci.yml@main
    with:
      python-version: '3.11'
      build-command: 'pip install -r requirements.txt'
      test-command: 'pytest'
      lint-command: 'flake8 .'
```

### Java Project

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  ci:
    uses: jenly1314/actions/.github/workflows/ci.yml@main
    with:
      java-version: '17'
      build-command: './gradlew build'
      test-command: './gradlew test'
```

## License

These workflows are provided as-is for use in any project.
