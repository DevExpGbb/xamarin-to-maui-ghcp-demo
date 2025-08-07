# Issue Triage and Management Prompt

## Context
You are helping with GitHub issue triage and management. This prompt provides guidelines for efficiently triaging, labeling, and managing issues in a GitHub repository using conventional commits principles.

## Instructions

### Issue Triage Process

#### 1. Initial Assessment
For each new issue, evaluate:
- **Validity**: Is this a legitimate issue or feature request?
- **Clarity**: Is the issue description clear and actionable?
- **Scope**: Does this fit within the project's scope?
- **Duplicates**: Is this a duplicate of an existing issue?

#### 2. Issue Classification

##### Bug Reports
- **Title Pattern**: Should follow `bug: [description] (affects [component])`
- **Required Information**:
  - Steps to reproduce
  - Expected vs actual behavior
  - Environment details
  - Code samples (if applicable)

##### Feature Requests
- **Title Pattern**: Should follow `feat: [description] (for [component])`
- **Required Information**:
  - Problem statement
  - Proposed solution
  - Use cases
  - Acceptance criteria

##### Documentation Issues
- **Title Pattern**: Should follow `docs: [description]`
- **Types**: Missing docs, incorrect docs, outdated docs

##### Questions/Support
- **Redirect**: Point to discussions or Stack Overflow
- **Close**: If not a bug or feature request

### Labeling System

#### Priority Labels
- `priority-critical`: Security issues, data loss, app crashes
- `priority-high`: Major functionality broken, significant user impact
- `priority-medium`: Important features affected, moderate user impact
- `priority-low`: Minor issues, cosmetic problems

#### Type Labels
- `bug`: Something isn't working
- `enhancement`: New feature or request
- `documentation`: Improvements or additions to documentation
- `duplicate`: This issue or pull request already exists
- `question`: Further information is requested
- `wontfix`: This will not be worked on
- `help wanted`: Extra attention is needed
- `good first issue`: Good for newcomers

#### Component Labels
- `area-navigation`: Navigation, routing, modal presentation
- `area-databinding`: Data binding, MVVM, observable collections
- `area-controls`: UI controls, layouts, custom controls
- `area-platform-android`: Android-specific issues
- `area-platform-ios`: iOS-specific issues
- `area-platform-windows`: Windows-specific issues
- `area-platform-macos`: macOS-specific issues
- `area-performance`: Performance, memory, startup time
- `area-accessibility`: Accessibility, screen readers, keyboard navigation
- `area-migration`: Xamarin.Forms to .NET MAUI migration
- `area-samples`: Sample code, examples, tutorials

#### Status Labels
- `status-awaiting-response`: Waiting for issue author response
- `status-blocked`: Blocked by external dependency
- `status-in-progress`: Currently being worked on
- `status-needs-investigation`: Requires further investigation
- `status-needs-reproduction`: Cannot reproduce the issue

### Triage Actions

#### For Valid Bug Reports
```markdown
Thank you for reporting this issue! 

**Triage Summary:**
- **Impact**: [High/Medium/Low]
- **Platform(s)**: [Android/iOS/Windows/macOS/All]
- **Component**: [Navigation/DataBinding/Controls/etc.]
- **Reproducible**: [Yes/No/Needs more info]

**Next Steps:**
- [ ] Assign appropriate labels
- [ ] Set priority based on impact
- [ ] Assign to team member (if applicable)
- [ ] Request additional information (if needed)

**Labels Applied:**
- `bug`
- `priority-[level]`
- `area-[component]`
- `platform-[specific]` (if applicable)
```

#### For Feature Requests
```markdown
Thank you for this feature request!

**Triage Summary:**
- **Value**: [High/Medium/Low] - impact on users
- **Complexity**: [High/Medium/Low] - implementation difficulty
- **Scope**: [In scope/Out of scope/Needs discussion]
- **Priority**: [High/Medium/Low/Future]

**Next Steps:**
- [ ] Evaluate against project roadmap
- [ ] Assess technical feasibility
- [ ] Determine if community contribution is welcome
- [ ] Set milestone (if approved)

**Labels Applied:**
- `enhancement`
- `priority-[level]`
- `area-[component]`
- `help wanted` (if seeking contributions)
```

#### For Incomplete Issues
```markdown
Thanks for opening this issue! To help us investigate and resolve this, could you please provide:

**For Bug Reports:**
- [ ] Steps to reproduce the issue
- [ ] Expected behavior
- [ ] Actual behavior
- [ ] Platform and version information
- [ ] Minimal code sample demonstrating the issue

**For Feature Requests:**
- [ ] Detailed description of the proposed feature
- [ ] Use cases and scenarios
- [ ] Proposed API or implementation approach
- [ ] Why existing alternatives don't meet your needs

I'm adding the `status-awaiting-response` label. Please provide the requested information and we'll continue the investigation.
```

#### For Duplicate Issues
```markdown
Thanks for reporting this! This appears to be a duplicate of #[existing-issue-number].

Please follow the existing issue for updates and feel free to add any additional context there if your scenario differs.

Closing as duplicate.
```

### GitHub CLI Commands for Triage

#### Apply Labels
```bash
# Add bug labels
gh issue edit [issue-number] --add-label "bug,priority-high,area-navigation"

# Add feature request labels
gh issue edit [issue-number] --add-label "enhancement,priority-medium,area-controls,help wanted"

# Mark as awaiting response
gh issue edit [issue-number] --add-label "status-awaiting-response"
```

#### Batch Operations
```bash
# Close stale issues
gh issue list --label "status-awaiting-response" --state open --json number,updatedAt | jq -r '.[] | select(.updatedAt < "2024-01-01") | .number' | xargs -I {} gh issue close {}

# Add good first issue label to simple bugs
gh issue list --label "bug,priority-low" --state open --json number | jq -r '.[].number' | xargs -I {} gh issue edit {} --add-label "good first issue"
```

#### Create Issue Templates
```bash
# Create bug report template
gh issue create --template bug_report.md --title "bug: " --label "bug"

# Create feature request template
gh issue create --template feature_request.md --title "feat: " --label "enhancement"
```

### Triage Automation

#### Workflow for Auto-Labeling
```yaml
name: Auto-label Issues
on:
  issues:
    types: [opened]

jobs:
  auto-label:
    runs-on: ubuntu-latest
    steps:
      - name: Label bug reports
        if: contains(github.event.issue.title, 'bug:')
        run: gh issue edit ${{ github.event.issue.number }} --add-label "bug"
        
      - name: Label feature requests
        if: contains(github.event.issue.title, 'feat:')
        run: gh issue edit ${{ github.event.issue.number }} --add-label "enhancement"
        
      - name: Label documentation
        if: contains(github.event.issue.title, 'docs:')
        run: gh issue edit ${{ github.event.issue.number }} --add-label "documentation"
```

### Issue Management Best Practices

#### Regular Triage Schedule
- **Daily**: Review new issues and urgent bugs
- **Weekly**: Triage backlog and update priorities
- **Monthly**: Review stale issues and clean up labels

#### Response Time Goals
- **Critical Issues**: 2 hours
- **High Priority**: 24 hours
- **Medium Priority**: 3 days
- **Low Priority**: 1 week

#### Community Engagement
- **Welcome new contributors**: Use encouraging language
- **Provide guidance**: Link to contributing guidelines
- **Recognize contributions**: Thank contributors publicly
- **Set expectations**: Be clear about timelines and priorities

### Quality Metrics

#### Track These Metrics
- Time to first response
- Time to resolution
- Number of open issues by priority
- Community contribution rate
- Issue resolution rate

#### GitHub CLI for Metrics
```bash
# Count issues by label
gh issue list --label "bug" --state open | wc -l
gh issue list --label "enhancement" --state open | wc -l

# List old issues
gh issue list --state open --json number,title,createdAt | jq -r '.[] | select(.createdAt < "2024-01-01") | "\(.number): \(.title)"'

# Find issues needing attention
gh issue list --label "status-awaiting-response" --state open --json number,title,updatedAt
```
