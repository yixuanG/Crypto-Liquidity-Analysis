# Contributing to Cryptocurrency Liquidity Analysis

Thank you for your interest in contributing to this project! This is an academic research project, but contributions are welcome.

## How to Contribute

### Reporting Issues
- Check if the issue already exists
- Provide a clear description of the problem
- Include error messages and relevant context
- Specify which notebook and which step caused the issue

### Suggesting Enhancements
- Clearly describe the enhancement
- Explain why it would be useful
- Provide examples if possible

### Code Contributions

#### For Bug Fixes
1. Fork the repository
2. Create a new branch (`git checkout -b fix/bug-description`)
3. Make your changes
4. Test thoroughly
5. Commit with clear messages
6. Push to your fork
7. Open a Pull Request

#### For New Features
1. Open an issue first to discuss the feature
2. Follow the same process as bug fixes
3. Include documentation for new features
4. Add examples if applicable

### Code Style Guidelines
- Follow PEP 8 for Python code
- Use descriptive variable names
- Add comments for complex logic
- Include docstrings for functions
- Keep functions focused and modular

### Jupyter Notebook Guidelines
- Clear cell outputs before committing
- Add markdown cells to explain each section
- Use descriptive variable names
- Include error handling where appropriate
- Document data requirements

### Documentation
- Update README.md if you change functionality
- Add or update docstrings
- Update CHANGELOG.md for significant changes
- Keep comments up to date

## Development Setup

```bash
# Clone your fork
git clone https://github.com/your-username/Crypto_Liquidity.git
cd Crypto_Liquidity

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies (if any)
pip install jupyter pytest black flake8
```

## Testing

- Test your changes with sample data
- Ensure all notebooks run without errors
- Check that outputs are as expected
- Verify documentation is accurate

## Commit Messages

Use clear, descriptive commit messages:
```
Good:
- "Fix panel generation bug for cross-month events"
- "Add visualization for depth metric"
- "Update README with installation instructions"

Bad:
- "fix"
- "update"
- "changes"
```

## Pull Request Process

1. Update documentation as needed
2. Clear notebook outputs (unless showing results)
3. Ensure code follows style guidelines
4. Describe your changes in the PR description
5. Reference any related issues
6. Wait for review and address feedback

## Questions?

If you have questions:
- Check existing issues
- Review the documentation
- Open a new issue for discussion

## Code of Conduct

- Be respectful and constructive
- Focus on the project goals
- Help others learn
- Give credit where due
- Respect data privacy and copyright

## Academic Integrity

This is an academic project:
- Do not share proprietary data
- Give proper citations
- Respect intellectual property
- Follow your institution's academic policies

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to cryptocurrency liquidity research!

