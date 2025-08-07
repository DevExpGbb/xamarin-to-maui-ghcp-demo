# Bug Report Issue Creation Prompt

## Context
You are helping create a GitHub issue for a bug report. Follow these guidelines to create a well-structured issue that follows conventional commits principles and provides clear, actionable information.

## Instructions

### Title Format
Use this format for the issue title:
```
bug: [brief description in imperative mood] (affects [component/area])
```

Examples:
- `bug: fix navigation crash when returning from modal page (affects Navigation)`
- `bug: resolve memory leak in ListView with custom cells (affects ListView)`
- `bug: correct binding errors in DataTemplate scenarios (affects DataBinding)`

### Issue Body Template
Use this structure for the issue body:

```markdown
## Summary
Brief description of the bug and its impact.

## Environment
- **Platform(s)**: [Android/iOS/Windows/macOS]
- **Framework**: [Xamarin.Forms version / .NET MAUI version]
- **Device/Simulator**: [Specific device or simulator info]
- **OS Version**: [Target OS version]

## Steps to Reproduce
1. [First step]
2. [Second step]
3. [Additional steps...]

## Expected Behavior
Describe what should happen.

## Actual Behavior
Describe what actually happens.

## Code Sample
```csharp
// Minimal reproducible code sample
```

## Additional Context
- Screenshots/videos if applicable
- Error messages or stack traces
- Related issues or PRs
- Workarounds attempted

## Labels to Apply
- `bug`
- `priority-[high/medium/low]`
- `platform-[android/ios/windows/macos]` (if platform-specific)
- `area-[navigation/databinding/controls/etc]`

## Assignment
Consider assigning to maintainers familiar with the affected component.
```

### Quality Checklist
Before creating the issue, ensure:
- [ ] Title is concise and follows the format
- [ ] Bug is reproducible with clear steps
- [ ] Environment information is complete
- [ ] Code sample is minimal and focused
- [ ] Appropriate labels are suggested
- [ ] Impact and priority are clear

### CLI Command Template
```bash
gh issue create \
  --title "bug: [description] (affects [component])" \
  --body-file issue-body.md \
  --label "bug,priority-medium" \
  --assignee @maintainer
```
