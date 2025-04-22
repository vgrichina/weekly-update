# Weekly Development Update Recipe

This document outlines the process for generating weekly development updates using GitHub's API through the `gh` command-line tool.

## Repository Structure

- `md/` - Detailed markdown updates with full information
- `tweets/` - Simplified tweet content for sharing on Twitter
- `svg/` - Cover images for social media posts

## Steps to Generate Weekly Updates

1. **Determine the date range** for the update (e.g., March 24, 2025 to April 21, 2025)

2. **Create files with date-based naming convention**:
   - Format: `YYYY-MM-DD_to_YYYY-MM-DD.md` (for all file types)
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

7. **Create the detailed markdown update** in the `md/` directory:
   - Title with date range
   - Section for each repository with key updates and GitHub link
   - Save as `md/YYYY-MM-DD_to_YYYY-MM-DD.md`

8. **Create the tweet content** in the `tweets/` directory:
   - Simplified version of the update
   - Each paragraph should be tweetable
   - No numbering or hashtags
   - Include links at the end
   - Save as `tweets/YYYY-MM-DD_to_YYYY-MM-DD.md`

9. **Create the SVG cover image** in the `svg/` directory:
   - Include "Dev Update" title and date range
   - List key repositories/projects
   - Use static design (no animations) for screenshot compatibility
   - Save as `svg/YYYY-MM-DD_to_YYYY-MM-DD.svg`

## Detailed Markdown Format Example

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

## Tweet Format Example

```
Enhanced Vibe Compiler with better CLI options, improved configuration system, added CI testing workflow, and created comprehensive documentation with tutorials.

Added AI Player to Vibe Pong with evaluation scripts to test different models. Refactored the project structure for better extensibility.

Links:
https://github.com/vgrichina/vibe-compiler
https://github.com/vgrichina/vibe-pong
```

Run this process regularly (weekly or bi-weekly) to maintain a consistent record of development activities.