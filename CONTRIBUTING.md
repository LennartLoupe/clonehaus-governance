# Contributing to Clonehaus Governance Plugin

Thank you for your interest in contributing! We welcome contributions from the community.

## How to Contribute

### Reporting Bugs

Use GitHub Issues with the bug report template. Include:
- Steps to reproduce
- Expected vs actual behavior
- Cowork version
- Plugin version
- Framework (if relevant)

### Suggesting Features

Use GitHub Discussions or Issues with the feature request template. Describe:
- The problem you're trying to solve
- Your proposed solution
- Any alternatives you've considered

### Adding Framework Support

Want to add support for a new framework? Great!

1. **Fork the repository**
2. **Create template file** in `templates/`
   - Follow existing template structure
   - Include governance guard implementation
   - Add comprehensive comments
   - Include usage example
3. **Add documentation** in `docs/frameworks/`
4. **Create example** in `examples/`
5. **Update README** to list the new framework
6. **Submit PR** with description of framework and testing

### Code Style

**Markdown files:**
- Use ATX headers (`#` not underlines)
- One sentence per line for easy diffs
- Include examples where helpful

**Python templates:**
- Follow PEP 8
- Include type hints
- Comprehensive docstrings
- Clear variable names

**JSON templates:**
- Pretty-printed (2-space indent)
- Include comments where format allows
- Validate against schema

### Testing Your Changes

Before submitting:
1. Install plugin locally in Cowork
2. Test all affected commands
3. Verify generated code works (for framework templates)
4. Check documentation renders correctly

### Pull Request Process

1. **Create feature branch**: `git checkout -b feature/your-feature-name`
2. **Make changes** with clear commits
3. **Update documentation** if needed
4. **Update CHANGELOG.md** under [Unreleased]
5. **Submit PR** with clear description
6. **Respond to feedback** from maintainers

### Community Guidelines

- Be respectful and constructive
- Focus on what's best for the project
- Assume good intentions
- Help others when you can

## Development Setup
```bash
# Clone your fork
git clone https://github.com/YOUR-USERNAME/clonehaus-governance.git
cd clonehaus-governance

# Create feature branch
git checkout -b feature/your-feature

# Make changes
# ...

# Test locally
claude plugin install .

# Test in Cowork
# Run commands and verify behavior

# Commit and push
git add .
git commit -m "Clear description of changes"
git push origin feature/your-feature
```

## Questions?

Open a discussion on GitHub or email info@clonehaus.ai

## License

By contributing, you agree that your contributions will be licensed under the MIT License.