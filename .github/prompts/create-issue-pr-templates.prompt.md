# GitHub Issue and PR Templates Creation Prompt

## Context
You are helping create GitHub issue and pull request templates that integrate with conventional commits and provide structured formats for consistent issue tracking and code contributions.

## Instructions

### Issue Template Creation

#### Bug Report Template
Create `.github/ISSUE_TEMPLATE/bug_report.yml`:

```yaml
name: 🐛 Bug Report
description: Create a report to help us improve
title: "bug: [brief description] (affects [component])"
labels: ["bug", "needs-triage"]
assignees: []
body:
  - type: markdown
    attributes:
      value: |
        Thanks for taking the time to fill out this bug report! Please provide as much detail as possible.

  - type: input
    id: summary
    attributes:
      label: Summary
      description: Brief description of the bug and its impact
      placeholder: "Describe the issue in one sentence"
    validations:
      required: true

  - type: dropdown
    id: platforms
    attributes:
      label: Platform(s)
      description: Which platforms are affected?
      multiple: true
      options:
        - Android
        - iOS
        - Windows
        - macOS
        - All platforms
    validations:
      required: true

  - type: input
    id: framework-version
    attributes:
      label: Framework Version
      description: Version of Xamarin.Forms or .NET MAUI
      placeholder: "e.g., .NET MAUI 8.0.10"
    validations:
      required: true

  - type: input
    id: device-info
    attributes:
      label: Device/Simulator
      description: Specific device or simulator information
      placeholder: "e.g., iPhone 15 Pro, Android API 34 Emulator"
    validations:
      required: true

  - type: textarea
    id: steps-to-reproduce
    attributes:
      label: Steps to Reproduce
      description: Clear steps to reproduce the issue
      placeholder: |
        1. Go to '...'
        2. Click on '...'
        3. Scroll down to '...'
        4. See error
    validations:
      required: true

  - type: textarea
    id: expected-behavior
    attributes:
      label: Expected Behavior
      description: What should happen?
      placeholder: "Describe what you expected to happen"
    validations:
      required: true

  - type: textarea
    id: actual-behavior
    attributes:
      label: Actual Behavior
      description: What actually happened?
      placeholder: "Describe what actually happened"
    validations:
      required: true

  - type: textarea
    id: code-sample
    attributes:
      label: Code Sample
      description: Minimal reproducible code sample
      render: csharp
      placeholder: |
        // Provide a minimal code sample that demonstrates the issue
        public class ExamplePage : ContentPage
        {
            public ExamplePage()
            {
                // Your code here
            }
        }

  - type: textarea
    id: additional-context
    attributes:
      label: Additional Context
      description: Any other context about the problem
      placeholder: |
        - Screenshots or videos
        - Error messages or stack traces
        - Workarounds attempted
        - Related issues

  - type: dropdown
    id: priority
    attributes:
      label: Priority
      description: How critical is this issue?
      options:
        - Low - Cosmetic issue, workaround available
        - Medium - Functionality affected, workaround difficult
        - High - Major functionality broken, no workaround
        - Critical - App crashes, security issue, data loss
    validations:
      required: true

  - type: checkboxes
    id: component-areas
    attributes:
      label: Component Areas
      description: Which areas does this affect? (Select all that apply)
      options:
        - label: Navigation
        - label: Data Binding
        - label: Controls (Button, Entry, etc.)
        - label: Layouts (Grid, StackLayout, etc.)
        - label: Collections (ListView, CollectionView)
        - label: Graphics and Animation
        - label: Platform Integration
        - label: Performance
        - label: Accessibility
        - label: Theming/Styling
```

#### Feature Request Template
Create `.github/ISSUE_TEMPLATE/feature_request.yml`:

```yaml
name: ✨ Feature Request
description: Suggest an idea for this project
title: "feat: [feature description] (for [component])"
labels: ["enhancement", "needs-triage"]
assignees: []
body:
  - type: markdown
    attributes:
      value: |
        Thanks for suggesting a new feature! Please provide detailed information to help us understand and evaluate your request.

  - type: input
    id: feature-summary
    attributes:
      label: Feature Summary
      description: Brief description of the proposed feature
      placeholder: "Summarize the feature in one sentence"
    validations:
      required: true

  - type: textarea
    id: problem-statement
    attributes:
      label: Problem Statement
      description: What problem does this feature solve?
      placeholder: "Describe the problem or gap this feature addresses"
    validations:
      required: true

  - type: textarea
    id: proposed-solution
    attributes:
      label: Proposed Solution
      description: Detailed description of your proposed implementation
      placeholder: "Describe how you envision this feature working"
    validations:
      required: true

  - type: textarea
    id: use-cases
    attributes:
      label: Use Cases
      description: Specific scenarios where this feature would be useful
      placeholder: |
        **Primary Use Case**: Main scenario this addresses
        **Secondary Use Cases**: Additional scenarios
        **User Story**: As a [user type], I want [goal] so that [benefit]
    validations:
      required: true

  - type: textarea
    id: api-example
    attributes:
      label: Proposed API Usage
      description: Show how the feature would be used in code
      render: csharp
      placeholder: |
        // Example of how the feature would be used
        public class ExampleUsage
        {
            public void DemonstrateFeature()
            {
                // Show the proposed API
            }
        }

  - type: checkboxes
    id: acceptance-criteria
    attributes:
      label: Acceptance Criteria
      description: What must be true for this feature to be complete?
      options:
        - label: Feature works on all supported platforms
        - label: API is consistent with existing patterns
        - label: Documentation is updated
        - label: Unit tests are added
        - label: Sample code is provided
        - label: Performance impact is acceptable
        - label: Accessibility requirements are met

  - type: dropdown
    id: complexity
    attributes:
      label: Implementation Complexity
      description: How complex do you think this feature would be to implement?
      options:
        - Low - Simple addition or modification
        - Medium - Moderate implementation effort
        - High - Significant architecture changes required
        - Unknown - Need technical assessment
    validations:
      required: true

  - type: dropdown
    id: priority
    attributes:
      label: Priority
      description: How important is this feature?
      options:
        - Low - Nice to have
        - Medium - Would improve user experience
        - High - Important for adoption
        - Critical - Blocking major scenarios
    validations:
      required: true

  - type: textarea
    id: alternatives
    attributes:
      label: Alternatives Considered
      description: What other approaches have you considered?
      placeholder: "Describe alternative solutions and why they weren't chosen"

  - type: checkboxes
    id: breaking-changes
    attributes:
      label: Breaking Changes
      description: Would this feature introduce breaking changes?
      options:
        - label: This feature would introduce breaking changes
        - label: This feature is backward compatible

  - type: checkboxes
    id: contribution
    attributes:
      label: Community Contribution
      description: Are you willing to contribute to this feature?
      options:
        - label: I'd like to work on this feature
        - label: I can help with testing
        - label: I can help with documentation
        - label: I need someone else to implement this
```

#### Documentation Issue Template
Create `.github/ISSUE_TEMPLATE/documentation.yml`:

```yaml
name: 📚 Documentation Issue
description: Report an issue with documentation
title: "docs: [description of documentation issue]"
labels: ["documentation", "needs-triage"]
assignees: []
body:
  - type: dropdown
    id: doc-type
    attributes:
      label: Documentation Type
      description: What type of documentation issue is this?
      options:
        - Missing documentation
        - Incorrect information
        - Outdated content
        - Unclear instructions
        - Broken links
        - Code sample issues
    validations:
      required: true

  - type: input
    id: location
    attributes:
      label: Location
      description: Where is the documentation issue? (URL, file path, or section)
      placeholder: "https://docs.example.com/page or path/to/file.md"
    validations:
      required: true

  - type: textarea
    id: current-content
    attributes:
      label: Current Content
      description: What does the documentation currently say?
      placeholder: "Copy the current text or describe what's there"

  - type: textarea
    id: suggested-content
    attributes:
      label: Suggested Content
      description: What should the documentation say instead?
      placeholder: "Provide the corrected or missing content"
    validations:
      required: true

  - type: textarea
    id: additional-context
    attributes:
      label: Additional Context
      description: Any other context or examples that would help
      placeholder: "Screenshots, related documentation, external references"
```

### Pull Request Template

Create `.github/PULL_REQUEST_TEMPLATE.md`:

```markdown
## Description
Brief description of the changes and why they were made.

## Type of Change
Please select the type of change (check one):

- [ ] 🐛 Bug fix (non-breaking change which fixes an issue)
- [ ] ✨ New feature (non-breaking change which adds functionality)
- [ ] 💥 Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] 📚 Documentation update
- [ ] 🎨 Style/formatting changes (no functional changes)
- [ ] ♻️ Code refactoring (no functional changes)
- [ ] ⚡ Performance improvement
- [ ] ✅ Test additions or fixes
- [ ] 🔧 Chore/maintenance

## Related Issues
<!-- Link to related issues using keywords: Closes #123, Fixes #456, Related to #789 -->

## Changes Made
### Files Modified
- `path/to/file1.cs` - [brief description]
- `path/to/file2.xaml` - [brief description]

### Key Changes
1. [Specific change with technical details]
2. [Another change with context]
3. [Additional changes as needed]

## Testing
### Platforms Tested
- [ ] Android
- [ ] iOS  
- [ ] Windows
- [ ] macOS

### Test Scenarios
- [ ] [Specific test scenario 1]
- [ ] [Specific test scenario 2]
- [ ] [Additional scenarios]

### Test Results
- [ ] All existing tests pass
- [ ] New tests added for new functionality
- [ ] Manual testing completed
- [ ] No regressions identified

## Screenshots/Videos
<!-- Add screenshots or videos demonstrating the changes if applicable -->

## Breaking Changes
<!-- If this introduces breaking changes, describe them and provide migration guidance -->

## Checklist
- [ ] My code follows the project's coding standards
- [ ] I have performed a self-review of my code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
- [ ] Any dependent changes have been merged and published

## Additional Notes
<!-- Any additional information that reviewers should know -->
```

### GitHub CLI Commands for Templates

#### Create Issue Templates Directory
```bash
mkdir -p .github/ISSUE_TEMPLATE
```

#### Create Issue from Template
```bash
# Bug report
gh issue create --template bug_report.yml

# Feature request  
gh issue create --template feature_request.yml

# Documentation issue
gh issue create --template documentation.yml
```

#### List Available Templates
```bash
gh issue create --help
```

### Template Configuration

#### Configure Default Labels
Add to `.github/ISSUE_TEMPLATE/config.yml`:

```yaml
blank_issues_enabled: false
contact_links:
  - name: 💬 Discussions
    url: https://github.com/owner/repo/discussions
    about: Ask questions and discuss ideas with the community
  - name: 🆘 Support
    url: https://stackoverflow.com/questions/tagged/maui
    about: Get help with implementation questions on Stack Overflow
  - name: 📖 Documentation
    url: https://docs.microsoft.com/dotnet/maui/
    about: Read the official .NET MAUI documentation
```

### Automation Integration

#### Auto-assign Labels Based on Template
```yaml
name: Auto-assign Labels
on:
  issues:
    types: [opened]

jobs:
  auto-assign:
    runs-on: ubuntu-latest
    steps:
      - name: Assign bug labels
        if: contains(github.event.issue.title, 'bug:')
        run: |
          gh issue edit ${{ github.event.issue.number }} \
            --add-label "bug,needs-triage"
            
      - name: Assign feature labels  
        if: contains(github.event.issue.title, 'feat:')
        run: |
          gh issue edit ${{ github.event.issue.number }} \
            --add-label "enhancement,needs-triage"
            
      - name: Assign documentation labels
        if: contains(github.event.issue.title, 'docs:')
        run: |
          gh issue edit ${{ github.event.issue.number }} \
            --add-label "documentation,needs-triage"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Quality Assurance

#### Template Validation
- Ensure all required fields are marked as required
- Test templates by creating sample issues
- Verify that labels are applied correctly
- Check that workflows trigger properly

#### Regular Review
- Update templates based on feedback
- Add new fields as needed
- Remove unused options
- Keep examples current and relevant

These templates provide a structured approach to issue and PR management while integrating seamlessly with conventional commits and automated workflows.
