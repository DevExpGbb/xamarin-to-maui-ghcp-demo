# Feature Request Issue Creation Prompt

## Context
You are helping create a GitHub issue for a feature request. Follow these guidelines to create a well-structured feature request that aligns with conventional commits principles and provides clear value proposition.

## Instructions

### Title Format
Use this format for the issue title:
```
feat: [brief description in imperative mood] (for [component/area])
```

Examples:
- `feat: add dark mode support for all controls (for Theming)`
- `feat: implement swipe gestures in CollectionView (for CollectionView)`
- `feat: add accessibility improvements to custom renderers (for Accessibility)`

### Issue Body Template
Use this structure for the issue body:

```markdown
## Feature Summary
Brief description of the proposed feature and its value.

## Problem Statement
Describe the problem this feature solves or the gap it fills.

## Proposed Solution
Detailed description of the proposed implementation.

## Use Cases
- **Primary Use Case**: [Main scenario this addresses]
- **Secondary Use Cases**: [Additional scenarios]
- **User Story**: As a [user type], I want [goal] so that [benefit].

## Technical Considerations
- **Affected Components**: [List of components/areas that would be modified]
- **Platform Impact**: [Cross-platform, platform-specific considerations]
- **Breaking Changes**: [Yes/No - with explanation]
- **Dependencies**: [Any new dependencies or requirements]

## Design Mockups/Examples
```csharp
// Proposed API usage example
public class ExampleUsage
{
    public void DemonstrateFeature()
    {
        // Show how the feature would be used
    }
}
```

## Acceptance Criteria
- [ ] [Specific, measurable criterion 1]
- [ ] [Specific, measurable criterion 2]
- [ ] [Additional criteria...]
- [ ] Documentation updated
- [ ] Unit tests added
- [ ] Platform-specific implementations completed

## Alternatives Considered
Describe alternative approaches and why they were not chosen.

## Implementation Estimate
- **Complexity**: [Low/Medium/High]
- **Estimated Effort**: [Small/Medium/Large]
- **Required Skills**: [List technical skills needed]

## Labels to Apply
- `enhancement`
- `feature-request`
- `priority-[high/medium/low]`
- `area-[component/subsystem]`
- `help wanted` (if seeking community contributions)

## Related Issues/PRs
Link to related issues, discussions, or existing PRs.
```

### Quality Checklist
Before creating the issue, ensure:
- [ ] Title clearly describes the feature
- [ ] Business value is articulated
- [ ] Technical approach is feasible
- [ ] Use cases are realistic and valuable
- [ ] Acceptance criteria are specific
- [ ] Implementation complexity is assessed
- [ ] Alternatives have been considered

### CLI Command Template
```bash
gh issue create \
  --title "feat: [description] (for [component])" \
  --body-file feature-request-body.md \
  --label "enhancement,feature-request,priority-medium" \
  --milestone "future"
```
