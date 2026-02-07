# Contributing to Reusable GitHub Actions Workflows

Thank you for your interest in contributing to this repository! This document provides guidelines for contributing.

## How to Contribute

### Adding New Workflows

1. Create a new workflow file in `.github/workflows/`
2. Use `workflow_call` trigger for reusable workflows
3. Document all inputs and secrets clearly
4. Add usage examples in the README.md
5. Create example workflows in the `examples/` directory

### Workflow Structure

All reusable workflows should follow this structure:

```yaml
name: Workflow Name

on:
  workflow_call:
    inputs:
      input-name:
        description: 'Input description'
        required: false/true
        type: string/boolean/number
        default: 'default-value'
    secrets:
      secret-name:
        description: 'Secret description'
        required: false/true

jobs:
  job-name:
    runs-on: ubuntu-latest
    steps:
      - name: Step name
        # Step actions
```

### Best Practices

1. **Flexibility**: Provide sensible defaults but allow customization
2. **Documentation**: Document all inputs, outputs, and secrets
3. **Minimal Dependencies**: Only include necessary dependencies
4. **Security**: Never hardcode secrets, always use secrets input
5. **Testing**: Test workflows before submitting
6. **Versioning**: Use semantic versioning for releases

### Adding Examples

When adding a new workflow:

1. Create an example in `examples/` directory
2. Update `examples/README.md` with the new example
3. Update main README.md with usage instructions

### Documentation Guidelines

- Keep documentation clear and concise
- Provide complete usage examples
- Document all parameters with descriptions
- Include common use cases
- Explain any special requirements

## Supported Languages and Frameworks

Current support includes:
- Node.js
- Java
- Python
- Go
- Docker

To add support for a new language:
1. Update the CI workflow with new setup steps
2. Update documentation
3. Add examples

## Testing Changes

Before submitting:
1. Validate YAML syntax: `yamllint .github/workflows/*.yml`
2. Test the workflow in a test repository
3. Verify documentation is accurate
4. Check examples work correctly

## Questions?

If you have questions, please open an issue in the repository.
