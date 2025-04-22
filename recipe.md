# Weekly Development Update Recipe

This document outlines the process for generating weekly development updates using GitHub's API through the `gh` command-line tool.

## Steps to Generate Weekly Updates

1. **Determine the date range** for the update (e.g., March 24, 2025 to April 21, 2025)

2. **Create a file with a date-based naming convention**:
   - Format: `YYYY-MM-DD_to_YYYY-MM-DD.md`
   - Example: `2025-03-24_to_2025-04-21.md`

3. **Fetch repository information**:
   ```bash
   # Get repositories created in the date range
   gh api -X GET search/repositories -f q="user:vgrichina created:>YYYY-MM-DD" -q '.items[].name'
   ```

4. **Fetch commit information** for each repository:
   ```bash
   # Get commit messages since a specific date
   gh api -X GET search/commits -f q="author:vgrichina committer-date:>YYYY-MM-DD" -q '.items[].commit.message'
   
   # Get commits for a specific repository
   gh api -X GET search/commits -f q="repo:vgrichina/REPO_NAME committer-date:>YYYY-MM-DD" -q '.items[].commit.message'
   ```

5. **Check Pull Requests and Issues**:
   ```bash
   # Get PR/Issue titles created since a specific date
   gh api -X GET search/issues -f q="author:vgrichina created:>YYYY-MM-DD" -q '.items[].title'
   ```

6. **Get repository details** for additional context:
   ```bash
   # Get repository information
   gh api -X GET repos/vgrichina/REPO_NAME -q '.description,.created_at,.updated_at'
   ```

7. **Organize the update** with the following sections:
   - Title with date range
   - For each repository:
     - Key updates and changes
     - Features added
     - Important fixes
     - GitHub link

8. **Save the file** in the weekly-update directory

## Update Format Example

```markdown
# Dev Update: [Start Date] - [End Date]

## [Repository Name]
- [Key update 1]
- [Key update 2]
- GitHub: https://github.com/vgrichina/[repository]

## [Repository Name]
- [Key update 1]
- [Key update 2]
- GitHub: https://github.com/vgrichina/[repository]
```

Run this process regularly (weekly or bi-weekly) to maintain a consistent record of development activities.