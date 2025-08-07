# Changelog Generation from Conventional Commits

## Context
You are helping generate a changelog from conventional commits between releases. This prompt will help create a well-structured changelog that follows Keep a Changelog format and conventional commits standards.

## Instructions

### Prerequisites
1. **Determine Commit Range**: 
   - Get commits since last release: `git log [last-tag]..HEAD --oneline`
   - Or between specific tags: `git log v1.0.0..v1.1.0 --oneline`

2. **Filter Conventional Commits**:
   ```bash
   git log --oneline --grep="^feat\|^fix\|^docs\|^style\|^refactor\|^perf\|^test\|^chore\|^build\|^ci" [range]
   ```

### Changelog Format Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [VERSION] - YYYY-MM-DD

### Added
- New features (feat: commits)

### Changed
- Changes in existing functionality (refactor: commits that affect user experience)

### Deprecated
- Soon-to-be removed features

### Removed
- Removed features (feat: commits with BREAKING CHANGE)

### Fixed
- Bug fixes (fix: commits)

### Security
- Security-related fixes
```

### Detailed Changelog Template

```markdown
# Changelog

## [1.2.0] - 2024-12-15

### Added
#### Navigation
- **Modal presentation styles**: Added support for custom modal presentation options on iOS and Android
  - Commit: `feat(navigation): add modal presentation options` ([abc123](commit-link))
  - PR: [#123](pr-link)
  - Implements new `PresentationStyle` enum with `FullScreen`, `PageSheet`, and `FormSheet` options

#### Controls
- **CollectionView swipe gestures**: Implemented swipe actions for collection view items
  - Commit: `feat(controls): add swipe gestures to CollectionView` ([def456](commit-link))
  - PR: [#124](pr-link)
  - Supports left and right swipe actions with customizable templates

#### Data Binding
- **Compiled bindings performance**: Enhanced binding performance with compiled binding support
  - Commit: `feat(databinding): improve performance with compiled bindings` ([ghi789](commit-link))
  - PR: [#125](pr-link)
  - Reduces binding overhead by 40% in complex UI scenarios

### Changed
#### Architecture
- **Dependency injection pattern**: Migrated to Microsoft.Extensions.DependencyInjection
  - Commit: `refactor(di): migrate to Microsoft.Extensions.DependencyInjection` ([jkl012](commit-link))
  - PR: [#126](pr-link)
  - **Breaking Change**: Service registration syntax has changed

#### Performance
- **ListView rendering optimization**: Improved ListView performance for large datasets
  - Commit: `perf(listview): optimize cell recycling and measurement` ([mno345](commit-link))
  - PR: [#127](pr-link)
  - Reduces memory usage by 25% and improves scroll performance

### Deprecated
- **Legacy renderer pattern**: Custom renderers are deprecated in favor of handlers
  - Commit: `docs(renderers): mark custom renderers as deprecated` ([pqr678](commit-link))
  - Migration guide: [Renderer to Handler Migration](link-to-guide)
  - Will be removed in v2.0.0

### Removed
- **Xamarin.Forms compatibility layer**: Removed legacy Xamarin.Forms compatibility shims
  - Commit: `chore: remove Xamarin.Forms compatibility layer` ([stu901](commit-link))
  - **Breaking Change**: Projects must fully migrate to .NET MAUI APIs
  - Migration guide: [Xamarin.Forms to .NET MAUI](link-to-guide)

### Fixed
#### Critical Issues
- **Memory leak in ListView**: Fixed memory leak with custom cells and data templates
  - Commit: `fix(listview): resolve memory leak in custom cells` ([vwx234](commit-link))
  - PR: [#128](pr-link)
  - Issue: [#100](issue-link)
  - Affects: All platforms

- **Navigation crash on modal dismiss**: Fixed crash when dismissing modal pages rapidly
  - Commit: `fix(navigation): prevent crash on rapid modal dismiss` ([yza567](commit-link))
  - PR: [#129](pr-link)
  - Issue: [#101](issue-link)
  - Affects: iOS only

#### Platform-Specific Fixes
##### Android
- **Keyboard overlap**: Fixed keyboard overlapping content in bottom sheet scenarios
  - Commit: `fix(android): resolve keyboard overlap in bottom sheets` ([bcd890](commit-link))
  - PR: [#130](pr-link)

- **Dark mode issues**: Corrected status bar and navigation bar colors in dark mode
  - Commit: `fix(android): improve dark mode color handling` ([efg123](commit-link))
  - PR: [#131](pr-link)

##### iOS
- **Memory warnings**: Reduced memory pressure in image-heavy scenarios
  - Commit: `fix(ios): optimize image memory management` ([hij456](commit-link))
  - PR: [#132](pr-link)

- **Safe area calculation**: Fixed safe area insets calculation for notched devices
  - Commit: `fix(ios): correct safe area calculation for notched devices` ([klm789](commit-link))
  - PR: [#133](pr-link)

### Security
- **Input validation**: Enhanced input validation to prevent injection attacks
  - Commit: `security: add input validation for web view content` ([nop012](commit-link))
  - PR: [#134](pr-link)
  - CVE: None assigned
  - Severity: Medium

## [1.1.0] - 2024-11-20

### Added
- **Dark mode support**: Comprehensive dark mode implementation across all controls
- **Accessibility improvements**: Enhanced screen reader support and keyboard navigation
- **Custom handlers**: New handler system for platform-specific customizations

### Fixed
- **Data binding errors**: Resolved binding errors in nested collection scenarios
- **Platform lifecycle**: Fixed app lifecycle management on all platforms

## [1.0.0] - 2024-10-15

### Added
- Initial release of .NET MAUI samples
- Migration from Xamarin.Forms samples
- Cross-platform compatibility for Android, iOS, Windows, and macOS
- Comprehensive sample collection covering all major scenarios

---

## Commit Categories

### Feature Commits (Added)
```
feat(scope): description
```
- New features and capabilities
- API additions
- New sample projects

### Bug Fix Commits (Fixed)
```
fix(scope): description
```
- Bug fixes and corrections
- Platform-specific issues
- Performance fixes

### Documentation Commits
```
docs(scope): description
```
- Documentation updates
- README improvements
- Code comments

### Style Commits
```
style(scope): description
```
- Code formatting
- Whitespace changes
- Style guide compliance

### Refactoring Commits (Changed)
```
refactor(scope): description
```
- Code refactoring
- Architecture improvements
- API changes (if user-facing)

### Performance Commits (Fixed/Changed)
```
perf(scope): description
```
- Performance improvements
- Optimization changes
- Memory usage improvements

### Test Commits
```
test(scope): description
```
- Test additions
- Test improvements
- Test fixes

### Chore Commits
```
chore(scope): description
```
- Maintenance tasks
- Dependency updates
- Build system changes

### Breaking Changes (Removed/Changed)
```
feat!: description
BREAKING CHANGE: explanation
```
- API breaking changes
- Removed features
- Changed behavior

## Links
- [Unreleased]: https://github.com/owner/repo/compare/v1.2.0...HEAD
- [1.2.0]: https://github.com/owner/repo/compare/v1.1.0...v1.2.0
- [1.1.0]: https://github.com/owner/repo/compare/v1.0.0...v1.1.0
- [1.0.0]: https://github.com/owner/repo/releases/tag/v1.0.0
```

### GitHub CLI Commands

#### Generate Changelog
```bash
# Get commits since last tag for changelog
git log $(git describe --tags --abbrev=0)..HEAD --oneline --pretty=format:"%h %s" | grep -E "^[a-f0-9]{7,} (feat|fix|docs|style|refactor|perf|test|chore)"

# Generate between specific versions
git log v1.0.0..v1.1.0 --oneline --pretty=format:"%h %s" | grep -E "^[a-f0-9]{7,} (feat|fix|docs|style|refactor|perf|test|chore)"
```

#### Automation Script
```bash
#!/bin/bash
# Auto-generate changelog from conventional commits

LAST_TAG=$(git describe --tags --abbrev=0)
NEW_VERSION="v1.2.0"
DATE=$(date +%Y-%m-%d)

echo "## [$NEW_VERSION] - $DATE" > changelog-entry.md
echo "" >> changelog-entry.md

# Get feature commits
echo "### Added" >> changelog-entry.md
git log $LAST_TAG..HEAD --oneline --grep="^feat" --pretty=format:"- %s ([%h](commit-link))" >> changelog-entry.md

# Get bug fixes
echo -e "\n### Fixed" >> changelog-entry.md
git log $LAST_TAG..HEAD --oneline --grep="^fix" --pretty=format:"- %s ([%h](commit-link))" >> changelog-entry.md

# Get performance improvements
echo -e "\n### Performance" >> changelog-entry.md
git log $LAST_TAG..HEAD --oneline --grep="^perf" --pretty=format:"- %s ([%h](commit-link))" >> changelog-entry.md

# Prepend to existing CHANGELOG.md
cat changelog-entry.md CHANGELOG.md > temp && mv temp CHANGELOG.md
```

### Quality Checklist
- [ ] All notable changes are included
- [ ] Changes are categorized correctly
- [ ] Breaking changes are clearly marked
- [ ] Commit links are functional
- [ ] PR references are included
- [ ] Security fixes are highlighted
- [ ] Format follows Keep a Changelog
- [ ] Semantic versioning is respected
