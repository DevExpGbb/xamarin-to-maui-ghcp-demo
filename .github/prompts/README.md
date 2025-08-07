# Master Prompt Index for GitHub Repository Management

## Overview
This directory contains a comprehensive collection of prompts designed to help with GitHub repository management, following conventional commits standards and best practices for .NET MAUI development.

## Available Prompts

### 🐛 Issue Management
- **[Bug Report Creation](./create-issue-from-bug.prompt.md)**
  - Structured template for creating bug report issues
  - Follows conventional commits format
  - Includes environment details and reproduction steps

- **[Feature Request Creation](./create-issue-from-feature-request.prompt.md)**
  - Template for feature request issues
  - Business value and technical considerations
  - Acceptance criteria and implementation estimates

- **[Issue Triage](./triage-issues.prompt.md)**
  - Guidelines for triaging and labeling issues
  - Priority assignment and component classification
  - Automation scripts for issue management

### 🔀 Pull Request Management
- **[Pull Request Creation](./create-pull-request.prompt.md)**
  - Comprehensive PR template following conventional commits
  - Code review checklist and testing guidelines
  - Breaking change documentation

### 📋 Release Management
- **[Release Notes Generation](./generate-release-notes.prompt.md)**
  - Professional release notes from conventional commits
  - Semantic versioning determination
  - Comprehensive change documentation

- **[Changelog Generation](./generate-changelog.prompt.md)**
  - Keep a Changelog format implementation
  - Automated changelog from git history
  - Conventional commits categorization

### 🤖 Automation
- **[GitHub Actions Workflows](./create-github-actions.prompt.md)**
  - CI/CD pipeline templates
  - Automated labeling and triage
  - Security and quality workflows

### 🔄 Migration Guides
- **[Xamarin to MAUI API Migration](./xamarin-to-maui-api-migration.prompt.md)**
  - API mapping and migration guidance
  - Breaking changes documentation

- **[MAUI Handlers Migration](./xamarin-to-maui-handlers.prompt.md)**
  - Custom renderer to handler migration
  - Platform-specific implementation patterns

- **[MAUI Packages Migration](./xamarin-to-maui-packages.prompt.md)**
  - NuGet package migration guidance
  - Dependency updates and alternatives

- **[MAUI Platform Code](./xamarin-to-maui-platform-code.prompt.md)**
  - Platform-specific code migration
  - Conditional compilation updates

- **[MAUI Project Structure](./xamarin-to-maui-project-structure.prompt.md)**
  - Project file and structure migration
  - Build configuration updates

- **[MAUI XAML Migration](./xamarin-to-maui-xaml.prompt.md)**
  - XAML namespace and control updates
  - Layout and styling migration

- **[Migration Checklist](./xamarin-to-maui-checklist.prompt.md)**
  - Comprehensive migration checklist
  - Step-by-step migration process

## Quick Start Guide

### Using with GitHub CLI

#### 1. Create a Bug Report
```bash
# Use the bug report template
gh issue create --template bug_report.md \
  --title "bug: navigation crash on modal dismiss (affects Navigation)" \
  --label "bug,priority-high,area-navigation"
```

#### 2. Create a Feature Request
```bash
# Use the feature request template
gh issue create --template feature_request.md \
  --title "feat: add dark mode support (for Theming)" \
  --label "enhancement,area-theming"
```

#### 3. Generate Release Notes
```bash
# Get commits since last release
LAST_TAG=$(git tag --sort=-version:refname | head -1)
git log $LAST_TAG..HEAD --oneline --pretty=format:"%h %s"

# Create release with generated notes
gh release create v1.2.0 \
  --title "Release v1.2.0" \
  --notes-file release-notes.md
```

#### 4. Automate Workflows
```bash
# Create CI workflow
gh workflow create ci.yml --name "CI" --on "push,pull_request"

# Run release workflow
gh workflow run release.yml --ref main
```

### Conventional Commits Integration

All prompts follow conventional commits format:
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types:**
- `feat`: New features
- `fix`: Bug fixes
- `docs`: Documentation changes
- `style`: Formatting changes
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Test additions/fixes
- `chore`: Maintenance tasks

## Integration with Development Workflow

### 1. Issue Creation
- Use structured templates for consistency
- Apply appropriate labels automatically
- Link to related issues and PRs
- Follow conventional commits in titles

### 2. Pull Request Process
- Ensure commit messages follow conventional format
- Use comprehensive PR templates
- Include testing and documentation updates
- Document breaking changes clearly

### 3. Release Management
- Aggregate conventional commits for release notes
- Determine semantic version automatically
- Generate comprehensive changelogs
- Maintain release history

### 4. Automation
- Auto-label issues and PRs
- Validate conventional commits
- Generate release notes automatically
- Manage stale issues

## Best Practices

### Commit Message Guidelines
```bash
# Good examples
feat(navigation): add modal presentation styles
fix(databinding): resolve memory leak in ListView
docs(samples): update migration guide
perf(controls): optimize ListView rendering

# Breaking changes
feat!: remove deprecated APIs
feat(api)!: change NavigationService interface

BREAKING CHANGE: NavigationService.Push now requires additional parameter
```

### Issue and PR Labels
```bash
# Priority labels
priority-critical, priority-high, priority-medium, priority-low

# Type labels
bug, enhancement, documentation, duplicate, question

# Component labels
area-navigation, area-databinding, area-controls, area-platform-android

# Status labels
status-awaiting-response, status-blocked, status-in-progress
```

### Release Versioning
- **MAJOR** (X.0.0): Breaking changes, API removals
- **MINOR** (X.Y.0): New features, backward compatible
- **PATCH** (X.Y.Z): Bug fixes, small improvements

## Customization

### Adapting for Your Project
1. **Update component labels** to match your project structure
2. **Modify issue templates** for your specific requirements
3. **Customize workflows** for your CI/CD needs
4. **Adjust automation** based on team preferences

### Team Guidelines
- Establish clear conventional commits standards
- Define priority and severity levels
- Set response time expectations
- Create contributor onboarding process

## Resources

### External References
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Semantic Versioning](https://semver.org/)
- [GitHub CLI](https://cli.github.com/)

### Internal Documentation
- [Contributing Guidelines](../CONTRIBUTING.md)
- [Code of Conduct](../CODE_OF_CONDUCT.md)
- [Security Policy](../SECURITY.md)

## Legacy Migration Prompts

### 🔄 Xamarin.Forms to .NET MAUI Migration
These prompts help with migrating existing Xamarin.Forms applications to .NET MAUI:
- Platforms folder organization
- MainActivity/AppDelegate updates
- Service implementation migration
- Resource and asset management
- Dependency injection setup

### 6. [NuGet Package Migration](./xamarin-to-maui-packages.md)
Comprehensive guide for updating NuGet packages from Xamarin.Forms ecosystem to MAUI-compatible versions.

**Key Topics:**
- Core package replacements
- Third-party package compatibility
- Alternative package recommendations
- MauiProgram registration
- Testing strategy

### 7. [Complete Migration Checklist](./xamarin-to-maui-checklist.md)
Comprehensive checklist to ensure thorough and successful migration with proper testing and validation.

**Key Topics:**
- Pre-migration assessment
- Step-by-step migration process
- Testing and validation procedures
- Performance optimization
- Deployment preparation

## How to Use These Prompts

### For Complete Migration
1. Start with the **Project Structure Migration** prompt
2. Follow with **API Migration** for code updates
3. Use **Platform-Specific Code** for platform implementations
4. Apply **XAML Migration** for UI updates
5. Convert custom controls using **Custom Renderers to Handlers**
6. Update dependencies with **NuGet Package Migration**
7. Validate everything using the **Complete Migration Checklist**

### For Specific Issues
- Use individual prompts when you need to focus on a particular aspect
- Reference the checklist for validation steps
- Cross-reference related prompts for comprehensive understanding

### Best Practices
- Always backup your project before starting migration
- Test frequently during the migration process
- Migrate one aspect at a time for easier debugging
- Use the checklist to ensure nothing is missed
- Document any custom solutions for future reference

## Additional Resources

### Microsoft Documentation
- [.NET MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/)
- [Upgrade from Xamarin.Forms](https://docs.microsoft.com/en-us/dotnet/maui/migration/)

### Community Resources
- [.NET MAUI Community Toolkit](https://github.com/CommunityToolkit/Maui)
- [MAUI Samples Repository](https://github.com/dotnet/maui-samples)

### Tools
- [.NET Upgrade Assistant](https://docs.microsoft.com/en-us/dotnet/core/porting/upgrade-assistant-overview)
- [XAML Hot Reload](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/xaml/hot-reload)

## Contributing
If you find issues with these prompts or have suggestions for improvements, please create an issue or submit a pull request.

## Support
For specific migration questions or issues, refer to:
- Official .NET MAUI documentation
- Stack Overflow with the `maui` tag
- .NET MAUI GitHub repository discussions
