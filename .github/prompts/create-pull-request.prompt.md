# Pull Request Creation Prompt

## Context
You are helping create a GitHub Pull Request. Follow these guidelines to create a well-structured PR that follows conventional commits principles and provides clear information for reviewers.

## Instructions

### Title Format
Use conventional commits format for the PR title:
```
[type][optional scope]: [description]
```

**Types:**
- `feat`: new feature
- `fix`: bug fix
- `docs`: documentation changes
- `style`: formatting, missing semicolons, etc.
- `refactor`: code refactoring
- `perf`: performance improvements
- `test`: adding or fixing tests
- `chore`: maintenance tasks

**Examples:**
- `feat(navigation): add modal presentation options`
- `fix(databinding): resolve memory leak in ListView`
- `docs(samples): update Xamarin.Forms to .NET MAUI migration guide`
- `refactor(controls): simplify custom renderer implementation`

### PR Body Template
Use this structure for the PR body:

```markdown
## Description
Brief description of the changes and why they were made.

## Type of Change
- [ ] 🐛 Bug fix (non-breaking change which fixes an issue)
- [ ] ✨ New feature (non-breaking change which adds functionality)
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] 📚 Documentation update
- [ ] 🎨 Style/formatting changes
- [ ] ♻️ Refactoring (no functional changes)
- [ ] ⚡ Performance improvement
- [ ] ✅ Test additions or fixes
- [ ] 🔧 Chore/maintenance

## Related Issues
Closes #[issue-number]
Related to #[issue-number]

## Changes Made
### Modified Files
- `path/to/file1.cs` - [brief description of changes]
- `path/to/file2.xaml` - [brief description of changes]

### Key Changes
1. [Change 1 with technical details]
2. [Change 2 with technical details]
3. [Additional changes...]

## Testing
### Test Environment
- **Platforms Tested**: [Android/iOS/Windows/macOS]
- **Devices/Simulators**: [List specific devices/simulators]
- **Test Scenarios**: [Key scenarios tested]

### Test Results
- [ ] All existing tests pass
- [ ] New tests added for new functionality
- [ ] Manual testing completed
- [ ] No regressions identified

## Screenshots/Videos
[If applicable, add screenshots or videos demonstrating the changes]

## Breaking Changes
[If applicable, describe any breaking changes and migration path]

## Documentation Updates
- [ ] Code comments updated
- [ ] README updated (if needed)
- [ ] API documentation updated
- [ ] Sample code updated

## Checklist
- [ ] Code follows the project's coding standards
- [ ] Self-review of code completed
- [ ] Code is properly commented
- [ ] Tests pass locally
- [ ] Lint checks pass
- [ ] No new warnings introduced
- [ ] Commit messages follow conventional commits
```

### Commit Message Guidelines
Ensure all commits in the PR follow conventional commits:

```
type(scope): description

[optional body]

[optional footer]
```

**Examples:**
```
feat(navigation): add support for modal presentation styles

Implement new modal presentation options for iOS and Android
to provide better user experience and platform consistency.

Closes #123
```

```
fix(databinding): resolve memory leak in custom ListView cells

- Remove event handler subscriptions in cell disposal
- Add proper cleanup in renderer lifecycle methods
- Update documentation with memory management best practices

Fixes #456
```

### Quality Checklist
Before creating the PR, ensure:
- [ ] Title follows conventional commits format
- [ ] Description clearly explains the changes
- [ ] All checklist items are completed
- [ ] Code review is self-completed
- [ ] Tests are comprehensive
- [ ] Documentation is updated
- [ ] Breaking changes are documented

### CLI Command Template
```bash
gh pr create \
  --title "feat(component): description of changes" \
  --body-file pr-body.md \
  --label "enhancement" \
  --reviewer @maintainer1,@maintainer2 \
  --milestone "next-release"
```

### PR Labels to Consider
- **Type**: `bug`, `enhancement`, `documentation`, `refactor`
- **Priority**: `priority-high`, `priority-medium`, `priority-low`
- **Status**: `work-in-progress`, `ready-for-review`, `needs-changes`
- **Platform**: `android`, `ios`, `windows`, `macos`
- **Area**: `navigation`, `databinding`, `controls`, `performance`
