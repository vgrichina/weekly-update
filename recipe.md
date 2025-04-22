# Weekly Development Update Recipe

This document outlines the process for generating weekly development updates using GitHub's API through the `gh` command-line tool.

## Repository Structure

- `md/` - Detailed markdown updates with full information
- `tweets/` - Simplified tweet content for sharing on Twitter
- `svg/` - Cover images for social media posts

## Claude Instructions

When using Claude to generate an update, it should:

1. Determine the date range from the user's input (from the given start date to today)
2. Create files with the date-based naming convention: `YYYY-MM-DD_to_YYYY-MM-DD.md`
3. Execute GitHub API queries to collect repository activity since the given date
4. Generate the markdown, tweet, and SVG files for the update period
5. Commit all generated files to the repository

## GitHub Data Collection

Use these commands to gather information about repository activity:

```bash
# Get repositories created in the date range
gh api -X GET search/repositories -f q="user:vgrichina created:>YYYY-MM-DD" -q '.items[].name'

# Get commit messages since a specific date
gh api -X GET search/commits -f q="author:vgrichina committer-date:>YYYY-MM-DD" -q '.items[].commit.message'

# Get commits for a specific repository
gh api -X GET search/commits -f q="repo:vgrichina/REPO_NAME committer-date:>YYYY-MM-DD" -q '.items[].commit.message'

# Get PR/Issue titles created since a specific date
gh api -X GET search/issues -f q="author:vgrichina created:>YYYY-MM-DD" -q '.items[].title'

# Get repository information
gh api -X GET repos/vgrichina/REPO_NAME -q '.description,.created_at,.updated_at'
```

## File Formats

### Detailed Markdown Format (`md/`)

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

### Tweet Format (`tweets/`)

```
Enhanced Vibe Compiler with better CLI options, improved configuration system, added CI testing workflow, and created comprehensive documentation with tutorials.

Added AI Player to Vibe Pong with evaluation scripts to test different models. Refactored the project structure for better extensibility.

Links:
https://github.com/vgrichina/vibe-compiler
https://github.com/vgrichina/vibe-pong
```

### SVG Guidelines (`svg/`)

The SVG cover image should:
- Include "Dev Update" title and date range
- List key repositories/projects
- Use static design (no animations) for screenshot compatibility
- Use a purple/pink gradient background
- Include decorative elements that suggest code/development
- Avoid including usernames or handles in the image

## Commit Process

After generating all files, commit them to the repository:

```bash
git add md/ tweets/ svg/
git commit -m "Add weekly update for [date range]"
git push
```