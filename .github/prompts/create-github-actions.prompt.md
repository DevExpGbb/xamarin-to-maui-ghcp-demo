# GitHub Actions Workflow Generation Prompt

## Context
You are helping create GitHub Actions workflows for automated CI/CD, issue management, and release processes. These workflows should integrate with conventional commits and follow best practices for .NET MAUI projects.

## Instructions

### Core Workflow Types

#### 1. Continuous Integration (CI)
Basic CI workflow for building and testing:

```yaml
name: CI
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'
          
      - name: Restore dependencies
        run: dotnet restore
        
      - name: Build
        run: dotnet build --no-restore
        
      - name: Test
        run: dotnet test --no-build --verbosity normal
```

#### 2. Automated Labeling
Auto-label issues and PRs based on conventional commits:

```yaml
name: Auto Label
on:
  issues:
    types: [opened]
  pull_request:
    types: [opened]

jobs:
  label:
    runs-on: ubuntu-latest
    steps:
      - name: Label bugs
        if: contains(github.event.issue.title, 'bug:') || contains(github.event.pull_request.title, 'fix:')
        run: |
          gh issue edit ${{ github.event.issue.number || github.event.pull_request.number }} \
            --add-label "bug"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          
      - name: Label features
        if: contains(github.event.issue.title, 'feat:') || contains(github.event.pull_request.title, 'feat:')
        run: |
          gh issue edit ${{ github.event.issue.number || github.event.pull_request.number }} \
            --add-label "enhancement"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

#### 3. Release Automation
Automated release creation based on conventional commits:

```yaml
name: Release
on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
          
      - name: Generate Release Notes
        id: release_notes
        run: |
          # Get previous tag
          PREV_TAG=$(git tag --sort=-version:refname | head -2 | tail -1)
          
          # Generate notes
          gh api repos/${{ github.repository }}/releases/generate-notes \
            -f tag_name="${{ github.ref_name }}" \
            -f target_commitish="main" \
            -f previous_tag_name="$PREV_TAG" \
            --jq '.body' > release_notes.md
            
      - name: Create Release
        run: |
          gh release create ${{ github.ref_name }} \
            --title "Release ${{ github.ref_name }}" \
            --notes-file release_notes.md
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Advanced Workflow Patterns

#### Multi-Platform Build Matrix
```yaml
name: Multi-Platform Build
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    strategy:
      matrix:
        os: [windows-latest, macos-latest, ubuntu-latest]
        include:
          - os: windows-latest
            platform: Windows
          - os: macos-latest
            platform: macOS
          - os: ubuntu-latest
            platform: Android
            
    runs-on: ${{ matrix.os }}
    
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup .NET MAUI
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'
          
      - name: Install MAUI Workload
        run: dotnet workload install maui
        
      - name: Build for ${{ matrix.platform }}
        run: |
          if [ "${{ matrix.platform }}" == "Android" ]; then
            dotnet build -f net8.0-android
          elif [ "${{ matrix.platform }}" == "Windows" ]; then
            dotnet build -f net8.0-windows10.0.19041.0
          elif [ "${{ matrix.platform }}" == "macOS" ]; then
            dotnet build -f net8.0-maccatalyst
          fi
```

#### Conventional Commits Validation
```yaml
name: Validate Commits
on:
  pull_request:
    branches: [ main ]

jobs:
  validate-commits:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
          
      - name: Validate Conventional Commits
        run: |
          # Get commits in PR
          git log --oneline origin/main..HEAD | while read commit; do
            if ! echo "$commit" | grep -qE "^[a-f0-9]{7} (feat|fix|docs|style|refactor|perf|test|chore|build|ci)(\(.+\))?: .+"; then
              echo "❌ Invalid commit message: $commit"
              echo "Commit messages must follow conventional commits format:"
              echo "type(scope): description"
              exit 1
            else
              echo "✅ Valid commit: $commit"
            fi
          done
```

#### Issue and PR Templates Sync
```yaml
name: Sync Templates
on:
  push:
    paths:
      - '.github/ISSUE_TEMPLATE/**'
      - '.github/PULL_REQUEST_TEMPLATE.md'
    branches: [ main ]

jobs:
  sync-templates:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Validate Issue Templates
        run: |
          for template in .github/ISSUE_TEMPLATE/*.md; do
            echo "Validating $template"
            # Check for required fields
            grep -q "name:" "$template" || { echo "Missing name field"; exit 1; }
            grep -q "about:" "$template" || { echo "Missing about field"; exit 1; }
            grep -q "title:" "$template" || { echo "Missing title field"; exit 1; }
            echo "✅ $template is valid"
          done
```

#### Automated Changelog Generation
```yaml
name: Update Changelog
on:
  release:
    types: [published]

jobs:
  update-changelog:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          token: ${{ secrets.PAT_TOKEN }}
          
      - name: Generate Changelog Entry
        run: |
          # Get release info
          RELEASE_TAG="${{ github.event.release.tag_name }}"
          RELEASE_DATE=$(date +%Y-%m-%d)
          
          # Get previous release
          PREV_TAG=$(gh release list --limit 2 --json tagName --jq '.[1].tagName')
          
          # Generate changelog entry
          echo "## [$RELEASE_TAG] - $RELEASE_DATE" > changelog_entry.md
          echo "" >> changelog_entry.md
          
          # Get conventional commits
          echo "### Added" >> changelog_entry.md
          git log $PREV_TAG..$RELEASE_TAG --oneline --grep="^feat" \
            --pretty=format:"- %s" >> changelog_entry.md
          
          echo "" >> changelog_entry.md
          echo "### Fixed" >> changelog_entry.md
          git log $PREV_TAG..$RELEASE_TAG --oneline --grep="^fix" \
            --pretty=format:"- %s" >> changelog_entry.md
          
          # Update CHANGELOG.md
          if [ -f CHANGELOG.md ]; then
            # Insert after the first line (title)
            sed -i '1r changelog_entry.md' CHANGELOG.md
          else
            mv changelog_entry.md CHANGELOG.md
          fi
          
      - name: Commit Changes
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add CHANGELOG.md
          git commit -m "docs: update changelog for ${{ github.event.release.tag_name }}"
          git push
        env:
          GITHUB_TOKEN: ${{ secrets.PAT_TOKEN }}
```

#### Stale Issue Management
```yaml
name: Manage Stale Issues
on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly on Sunday
  workflow_dispatch:

jobs:
  stale:
    runs-on: ubuntu-latest
    steps:
      - name: Mark Stale Issues
        run: |
          # Find issues awaiting response for > 14 days
          gh issue list \
            --label "status-awaiting-response" \
            --state open \
            --json number,updatedAt \
            --jq '.[] | select(.updatedAt < (now - 14*24*3600 | strftime("%Y-%m-%dT%H:%M:%SZ"))) | .number' | \
          while read issue; do
            gh issue comment "$issue" --body "This issue has been marked as stale due to inactivity. Please provide the requested information or it will be closed automatically."
            gh issue edit "$issue" --add-label "stale"
          done
          
      - name: Close Very Stale Issues
        run: |
          # Close issues stale for > 7 days
          gh issue list \
            --label "stale" \
            --state open \
            --json number,updatedAt \
            --jq '.[] | select(.updatedAt < (now - 7*24*3600 | strftime("%Y-%m-%dT%H:%M:%SZ"))) | .number' | \
          while read issue; do
            gh issue close "$issue" --reason "not planned" --comment "Closing due to inactivity. Please feel free to reopen if you can provide the requested information."
          done
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Security and Quality Workflows

#### Dependency Security Scan
```yaml
name: Security Scan
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 6 * * 1'  # Weekly on Monday

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Run Dependency Check
        uses: dependency-check/Dependency-Check_Action@main
        with:
          project: 'xamarin-forms-samples'
          path: '.'
          format: 'JSON'
          
      - name: Upload Results
        uses: actions/upload-artifact@v3
        with:
          name: security-report
          path: reports/
```

#### Code Quality Check
```yaml
name: Code Quality
on:
  pull_request:
    branches: [ main ]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'
          
      - name: Restore dependencies
        run: dotnet restore
        
      - name: Build
        run: dotnet build --no-restore --configuration Release
        
      - name: Run Code Analysis
        run: dotnet build --verbosity normal --configuration Release /p:RunAnalyzersDuringBuild=true
        
      - name: Check Formatting
        run: dotnet format --verify-no-changes --verbosity diagnostic
```

### Workflow Templates for GitHub CLI

#### Create CI Workflow
```bash
gh workflow create ci.yml \
  --name "Continuous Integration" \
  --on "push,pull_request" \
  --jobs "build,test"
```

#### Enable Workflow
```bash
gh workflow enable ci.yml
```

#### Run Workflow Manually
```bash
gh workflow run release.yml \
  --ref main \
  -f version="1.2.0"
```

#### Monitor Workflow
```bash
gh run list --workflow ci.yml
gh run view [run-id]
```

### Best Practices

#### Workflow Organization
- Keep workflows focused on single responsibilities
- Use reusable workflows for common patterns
- Organize workflows by purpose (CI, CD, automation)
- Use clear, descriptive names

#### Security Considerations
- Use minimal permissions (`permissions: read-all`)
- Store secrets securely
- Validate inputs in workflow_dispatch
- Use trusted actions from verified publishers

#### Performance Optimization
- Cache dependencies when possible
- Use matrix builds efficiently
- Fail fast on errors
- Parallelize independent jobs

#### Monitoring and Maintenance
- Set up notifications for failed workflows
- Review workflow metrics regularly
- Update actions to latest versions
- Clean up unused workflows

This comprehensive set of GitHub Actions workflows will automate most common repository management tasks while following conventional commits and best practices for .NET MAUI development.
