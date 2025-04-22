# Weekly Development Updates

This repository contains my weekly development updates for various projects.

## Usage

To generate a new update, use Claude with this simple command:

```
Generate dev update since [DATE] following recipe.md
```

For example:
```
Generate dev update since March 24, 2025 following recipe.md
```

Claude will:
1. Fetch GitHub data
2. Create markdown, tweet content, and SVG cover image 
3. Commit everything to the repository

## Repository Structure

- `md/` - Detailed markdown updates
- `tweets/` - Twitter content
- `svg/` - Cover images for social media
- `recipe.md` - Instructions for Claude