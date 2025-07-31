# Contributing to Pump.fun Smart Contract

Thank you for your interest in contributing to the Pump.fun Smart Contract! This document provides guidelines and information for contributors.

## 🚀 Getting Started

### Prerequisites

- Rust 1.70+
- Solana CLI 1.91.8+
- Anchor Framework 0.29.0+
- Node.js 16+
- Git

### Development Setup

1. **Fork the repository**
   ```bash
   git clone https://github.com/Tronzit-Veca/Pumpfun-Smart-Contract.git
   cd pumpfun-smart-contract
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Build the project**
   ```bash
   anchor build
   ```

4. **Run tests**
   ```bash
   anchor test
   ```

## 📝 Code Style Guidelines

### Rust Code Style

- Follow Rust standard formatting with `rustfmt`
- Use meaningful variable and function names
- Add comprehensive comments for complex logic
- Implement proper error handling

### TypeScript/JavaScript Code Style

- Use Prettier for code formatting
- Follow ESLint rules
- Use TypeScript for type safety
- Write clear function documentation

## 🧪 Testing

### Running Tests

```bash
# Run all tests
anchor test

# Run specific test file
anchor test tests/specific_test.ts

# Run with verbose output
anchor test --verbose
```

### Writing Tests

- Write tests for all new functionality
- Include both positive and negative test cases
- Test edge cases and error conditions
- Use descriptive test names

## 🔧 Development Workflow

### 1. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 2. Make Your Changes

- Write clean, well-documented code
- Add tests for new functionality
- Update documentation as needed

### 3. Commit Your Changes

```bash
git add .
git commit -m "feat: add virtual LP management functionality

- Implement add_virtual_lp instruction
- Add comprehensive error handling
- Include unit tests for new features"
```

### 4. Push and Create Pull Request

```bash
git push origin feature/your-feature-name
```

## 📋 Pull Request Guidelines

### Before Submitting

- [ ] Code follows style guidelines
- [ ] All tests pass
- [ ] Documentation is updated
- [ ] No breaking changes (unless discussed)
- [ ] Commit messages are clear and descriptive

### Pull Request Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No console errors
```

## 🐛 Reporting Bugs

### Bug Report Template

```markdown
## Bug Description
Clear description of the bug

## Steps to Reproduce
1. Step 1
2. Step 2
3. Step 3

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: [e.g., Windows 10]
- Rust Version: [e.g., 1.70.0]
- Solana CLI Version: [e.g., 1.91.8]
- Anchor Version: [e.g., 0.29.0]

## Additional Information
Any other relevant information
```

## 💡 Feature Requests

### Feature Request Template

```markdown
## Feature Description
Clear description of the requested feature

## Use Case
Why this feature is needed

## Proposed Implementation
Brief description of how it could be implemented

## Alternatives Considered
Other approaches that were considered
```

## 📚 Documentation

### Contributing to Documentation

- Keep documentation up-to-date with code changes
- Use clear, concise language
- Include code examples where appropriate
- Add diagrams for complex concepts

### Documentation Standards

- Use proper markdown formatting
- Include table of contents for long documents
- Add links to related resources
- Keep examples simple and working

## 🔒 Security

### Security Guidelines

- Never commit sensitive information (keys, passwords)
- Report security vulnerabilities privately
- Follow secure coding practices
- Validate all inputs

### Reporting Security Issues

For security issues, please contact us privately:
- Email: security@pump.fun
- Telegram: [@Tr1030109](https://t.me/Tr1030109)

## 🏆 Recognition

Contributors will be recognized in:
- Project README
- Release notes
- Contributor hall of fame

## 📞 Getting Help

- **GitHub Issues**: [Create an issue](https://github.com/Tronzit-Veca/Pumpfun-Smart-Contract/issues)
- **Telegram**: [@Tr1030109](https://t.me/Tr1030109)
- **Discord**: 0xapp123

## 📄 License

By contributing to this project, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to the Pump.fun Smart Contract! 🚀 