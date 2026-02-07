# Example Workflows

This directory contains example workflows demonstrating how to use the reusable workflows from this repository.

## Examples

- **[nodejs-ci.yml](nodejs-ci.yml)**: Complete CI/CD pipeline for a Node.js project
- **[python-ci.yml](python-ci.yml)**: Complete CI/CD pipeline for a Python project
- **[docker-build.yml](docker-build.yml)**: Docker build and push workflow
- **[release.yml](release.yml)**: Release workflow with NPM publishing and Docker image

## How to Use

1. Copy the example that matches your project type
2. Place it in your repository's `.github/workflows/` directory
3. Customize the inputs to match your project's needs
4. Add any required secrets to your repository settings

## Common Customizations

### Changing Node.js Version
```yaml
with:
  node-version: '20'  # or '18', '16', etc.
```

### Adding Build Arguments
```yaml
with:
  build-command: 'npm ci && npm run build'
```

### Enabling Additional Features
```yaml
with:
  enable-sonarcloud: true
  sonar-project-key: 'your-project-key'
  sonar-organization: 'your-org'
```

### Multiple Language Support
```yaml
with:
  codeql-languages: '["javascript", "python"]'
```
