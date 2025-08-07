# Release Notes Generation Prompt

## Context
You are helping generate release notes and changelog from conventional commits since the last release. This prompt will help create professional, comprehensive release notes that follow semantic versioning and conventional commits standards.

## Instructions

### Prerequisites
Before generating release notes, gather:
1. **Last Release Tag**: Get the last release tag using `git tag --sort=-version:refname | head -1`
2. **Commit Range**: Use `git log [last-tag]..HEAD --oneline` to get commits since last release
3. **Conventional Commits**: Filter commits that follow conventional commits format

### Release Type Determination
Based on conventional commits, determine the release type:

- **MAJOR** (X.0.0): Contains `BREAKING CHANGE:` in footer or `!` after type/scope
- **MINOR** (X.Y.0): Contains `feat:` commits
- **PATCH** (X.Y.Z): Contains only `fix:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, `chore:`

### Release Notes Template

```markdown
# Release Notes - v[VERSION]

## Release Summary
[Brief overview of the release - key highlights and themes]

## 🚀 New Features
[List all feat: commits with descriptions]

### Navigation Enhancements
- **Modal Presentation Styles**: Added support for custom modal presentation options on iOS and Android ([#123](link-to-pr))
- **Deep Linking**: Enhanced deep linking capabilities with parameter validation ([#124](link-to-pr))

### Control Improvements
- **CollectionView**: Added swipe gesture support for item actions ([#125](link-to-pr))
- **Entry Controls**: Implemented custom border styling options ([#126](link-to-pr))

## 🐛 Bug Fixes
[List all fix: commits with descriptions]

### Critical Fixes
- **Memory Management**: Resolved memory leak in ListView with custom cells ([#127](link-to-pr))
- **Data Binding**: Fixed binding errors in nested DataTemplate scenarios ([#128](link-to-pr))

### Platform-Specific Fixes
#### Android
- Fixed keyboard overlapping content in modal pages ([#129](link-to-pr))
- Resolved crash when rotating device during navigation ([#130](link-to-pr))

#### iOS
- Fixed status bar appearance issues in dark mode ([#131](link-to-pr))
- Resolved memory warnings in image-heavy scenarios ([#132](link-to-pr))

## 📚 Documentation Updates
[List all docs: commits]
- Updated Xamarin.Forms to .NET MAUI migration guide with latest best practices
- Added new sample demonstrating custom handler implementation
- Improved API documentation with additional code examples

## ⚡ Performance Improvements
[List all perf: commits]
- Optimized ListView rendering performance for large datasets ([#133](link-to-pr))
- Reduced app startup time by 15% through dependency injection improvements ([#134](link-to-pr))

## 🔧 Maintenance & Technical Improvements
[List refactor:, style:, test:, chore: commits]
- Refactored custom renderer architecture for better maintainability
- Updated CI/CD pipeline to support .NET 8
- Added comprehensive unit tests for data binding scenarios
- Upgraded all NuGet packages to latest stable versions

## 💥 Breaking Changes
[List any breaking changes with migration guidance]

### API Changes
- **NavigationService**: The `PushModalAsync` method signature has changed. 
  ```csharp
  // Old
  await Navigation.PushModalAsync(page);
  
  // New
  await Navigation.PushModalAsync(page, presentationStyle);
  ```

### Migration Guide
1. Update method calls to include new required parameters
2. Review custom renderers for compatibility with new APIs
3. Test navigation flows thoroughly after upgrade

## 📦 Dependencies
### Added
- Microsoft.Extensions.Hosting v8.0.0
- CommunityToolkit.Maui v7.0.0

### Updated
- Microsoft.Maui.Controls: 8.0.6 → 8.0.10
- CommunityToolkit.Mvvm: 8.2.0 → 8.2.2

### Removed
- Legacy Xamarin.Forms compatibility shims

## 🎯 Migration from Previous Version

### For v[PREVIOUS_VERSION] Users
1. **Update NuGet Packages**: Update all Microsoft.Maui.* packages to v[CURRENT_VERSION]
2. **Review Breaking Changes**: Check the breaking changes section above
3. **Update Custom Code**: Update any custom renderers or handlers as needed
4. **Test Thoroughly**: Run your test suite and manual testing

### Automatic Migration
Most changes are backward compatible. The migration should be seamless for:
- Standard XAML layouts
- Basic data binding scenarios
- Common navigation patterns

## 📊 Statistics
- **Total Commits**: [X] commits since v[PREVIOUS_VERSION]
- **Contributors**: [X] contributors ([list major contributors])
- **Files Changed**: [X] files modified
- **Lines of Code**: +[X] additions, -[Y] deletions

## 🙏 Acknowledgments
Special thanks to all contributors who made this release possible:
- [@contributor1](link) - Feature development and bug fixes
- [@contributor2](link) - Documentation improvements
- [@contributor3](link) - Testing and quality assurance

## 📝 Full Changelog
**Full Changelog**: [v[PREVIOUS_VERSION]...v[CURRENT_VERSION]](link-to-compare)

---

## Installation

### Package Manager
```xml
<PackageReference Include="Microsoft.Maui.Controls" Version="[VERSION]" />
```

### .NET CLI
```bash
dotnet add package Microsoft.Maui.Controls --version [VERSION]
```

## Support
- **Documentation**: [Link to docs]
- **Issues**: [Link to issues]
- **Discussions**: [Link to discussions]
- **Discord**: [Link to community]
```

### GitHub CLI Commands for Release

#### Create Release with Notes
```bash
# Create release from tag
gh release create v[VERSION] \
  --title "Release v[VERSION]" \
  --notes-file release-notes.md \
  --target main

# Create pre-release
gh release create v[VERSION]-beta \
  --title "Release v[VERSION] Beta" \
  --notes-file release-notes.md \
  --prerelease \
  --target main
```

#### Generate Automated Changelog
```bash
# Generate changelog since last release
gh api repos/:owner/:repo/releases/generate-notes \
  -f tag_name="v[VERSION]" \
  -f target_commitish="main" \
  -f previous_tag_name="v[PREVIOUS_VERSION]"
```

### Automation Script Template
```bash
#!/bin/bash
# Generate release notes from conventional commits

LAST_TAG=$(git tag --sort=-version:refname | head -1)
CURRENT_VERSION="v1.2.0"  # Update this

echo "Generating release notes from $LAST_TAG to HEAD"

# Get conventional commits
git log $LAST_TAG..HEAD --oneline --grep="^feat\|^fix\|^docs\|^style\|^refactor\|^perf\|^test\|^chore" > commits.txt

# Determine release type
if git log $LAST_TAG..HEAD --grep="BREAKING CHANGE\|!" --oneline | wc -l > 0; then
  echo "MAJOR release detected"
elif git log $LAST_TAG..HEAD --grep="^feat" --oneline | wc -l > 0; then
  echo "MINOR release detected"
else
  echo "PATCH release detected"
fi

# Create release
gh release create $CURRENT_VERSION \
  --title "Release $CURRENT_VERSION" \
  --notes-file release-notes.md \
  --target main
```

### Quality Checklist
- [ ] All commits since last release are reviewed
- [ ] Breaking changes are clearly documented
- [ ] Migration guide is comprehensive
- [ ] Version number follows semantic versioning
- [ ] Dependencies are accurately listed
- [ ] Contributors are acknowledged
- [ ] Links and references are valid
