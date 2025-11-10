# Git Leaderboard - Quick Examples

## Installation
npm install -g git-leaderboard

## Basic Commands

# Show default leaderboard (sorted by net lines)
git-leaderboard

# Show help
git-leaderboard --help

# Show version
git-leaderboard --version

## Sorting Examples

# Sort by commits
git-leaderboard --sort commits --show-commits

# Sort by lines added
git-leaderboard --sort added

# Sort by lines removed
git-leaderboard --sort removed

# Sort in reverse order (ascending)
git-leaderboard --sort commits --reverse --show-commits

## Filtering Examples

# Show top 5 contributors
git-leaderboard --limit 5

# Show top 10 by commits
git-leaderboard --sort commits --show-commits --limit 10

# Exclude bot accounts
git-leaderboard --exclude "dependabot,renovate,bot"

# Include only specific authors
git-leaderboard --include "Alice,Bob"

## Date Range Examples

# Last week
git-leaderboard --since "1 week ago"

# Last month
git-leaderboard --since "1 month ago"

# Last year
git-leaderboard --since "1 year ago"

# Specific year
git-leaderboard --since "2024-01-01" --until "2024-12-31"

# This quarter
git-leaderboard --since "3 months ago"

# Specific sprint (example: 2 weeks)
git-leaderboard --since "2024-10-01" --until "2024-10-14"

## Output Format Examples

# JSON output
git-leaderboard --format json

# JSON output with pretty formatting to file
git-leaderboard --format json > contributors.json

# CSV output
git-leaderboard --format csv

# CSV output to file
git-leaderboard --format csv > contributors.csv

# Table without colors
git-leaderboard --no-color

## Display Options

# Show commit counts
git-leaderboard --show-commits

# Show email addresses
git-leaderboard --show-email

# Show commits and emails
git-leaderboard --show-commits --show-email

## Combined Examples

# Top 10 contributors by commits in the last 6 months
git-leaderboard --sort commits --show-commits --limit 10 --since "6 months ago"

# Contributors excluding bots, sorted by lines added
git-leaderboard --sort added --exclude "dependabot,renovate"

# CSV export of top 20 contributors
git-leaderboard --limit 20 --format csv > top_contributors.csv

# JSON export of last month's contributions
git-leaderboard --since "1 month ago" --format json > monthly_stats.json

# Specific team members for review period
git-leaderboard --include "Alice,Bob,Charlie" --since "2024-10-01" --show-commits

# No color output for CI/CD
git-leaderboard --no-color --format table

## Pro Tips

# Pipe JSON to jq for advanced filtering
git-leaderboard --format json | jq '.[] | select(.commits > 10)'

# Export quarterly reports
git-leaderboard --since "3 months ago" --format csv > Q4_2024.csv

# Team performance comparison
git-leaderboard --show-commits --sort commits --since "1 month ago"

# Find contributors with most deletions
git-leaderboard --sort removed --show-commits

# Quick summary of recent work
git-leaderboard --since "1 week ago" --show-commits
