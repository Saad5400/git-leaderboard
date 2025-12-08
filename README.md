# Git Leaderboard 🏆

A colorful git contribution leaderboard for your repository. Track and visualize contributions from all team members with detailed statistics.

## Features

- 📊 View detailed contribution statistics (lines added, removed, net changes)
- 📈 Visual bar chart showing relative contributions
- 🔢 Track commit counts per contributor
- 📅 Filter by date range
- 🎯 Sort by different metrics (commits, added, removed, net lines)
- 📋 Multiple output formats (table, JSON, CSV)
- 🎨 Colorful terminal output
- 🔍 Filter contributors (include/exclude)
- 📧 Display author email addresses
- 🤝 **Intelligent author name grouping** - Automatically detect and merge similar author names
- ⚡ Fast and lightweight

## Installation

### Run directly

```bash
npx --yes git-leaderboard
```

### Global Installation

```bash
npm install -g git-leaderboard
```

### Local Installation

```bash
npm install
npm link
```

## Usage

Navigate to any git repository and run:

```bash
git-leaderboard [options]
```

### Options

| Option | Description |
|--------|-------------|
| `-V, --version` | Output the version number |
| `-s, --sort <type>` | Sort by: `commits`, `added`, `removed`, `net` (default: `net`) |
| `-l, --limit <number>` | Limit the number of contributors shown |
| `-r, --reverse` | Reverse the sort order |
| `--since <date>` | Show contributions since date (e.g., '2024-01-01', '1 week ago') |
| `--until <date>` | Show contributions until date |
| `-f, --format <type>` | Output format: `table`, `json`, `csv` (default: `table`) |
| `--no-color` | Disable colored output |
| `-e, --exclude <authors...>` | Exclude specific authors |
| `-i, --include <authors...>` | Include only specific authors |
| `--show-email` | Show author email addresses |
| `--show-commits` | Show commit count in the table |
| `--no-chart` | Hide the bar chart (shown by default) |
| `--group-similar` | Automatically group similar author names |
| `--similarity-threshold <number>` | Minimum similarity score for grouping (0-1, default: 0.4) |
| `-h, --help` | Display help for command |

## Examples

### Basic Usage

Show all contributors with net line changes:
```bash
git-leaderboard
```

### Sort by Commits

```bash
git-leaderboard --sort commits --show-commits
```

### Show Top 5 Contributors

```bash
git-leaderboard --limit 5
```

### Filter by Date Range

Show contributions from the last month:
```bash
git-leaderboard --since "1 month ago"
```

Show contributions for a specific year:
```bash
git-leaderboard --since "2024-01-01" --until "2024-12-31"
```

### Export to JSON

```bash
git-leaderboard --format json > stats.json
```

### Export to CSV

```bash
git-leaderboard --format csv > stats.csv
```

### Exclude Bot Accounts

```bash
git-leaderboard --exclude "dependabot,renovate"
```

### Show Only Specific Contributors

```bash
git-leaderboard --include "John,Sarah"
```

### Show with Email Addresses

```bash
git-leaderboard --show-email
```

### Sort by Lines Added (Descending)

```bash
git-leaderboard --sort added
```

### Sort by Commits (Ascending)

```bash
git-leaderboard --sort commits --reverse --show-commits
```

### Hide the Bar Chart

```bash
git-leaderboard --no-chart
```

### Group Similar Author Names

Interactively review and group similar author names (e.g., "john doe" and "John Doe"):
```bash
git-leaderboard --similarity-threshold 0.7
```

Automatically group similar names without prompting:
```bash
git-leaderboard --group-similar --similarity-threshold 0.4
```

### Complete Example

Show top 10 contributors by commits in the last 6 months with commit counts:
```bash
git-leaderboard --sort commits --show-commits --limit 10 --since "6 months ago"
```

## Output Examples

### Table Format (Default)

```
No.  Contributor                         Added    Removed        Net  Chart
1    John Doe                             5234        892       4342  ████████████████████
2    Jane Smith                           3421        654       2767  ████████████▌
3    Bob Johnson                          1876        432       1444  ██████▌

Summary:
Total                                    10531       1978       8553
```

The bar chart visualizes the sorted metric (net changes by default). Use `--no-chart` to hide it.

### JSON Format

```json
[
  {
    "name": "John Doe",
    "added": 5234,
    "removed": 892,
    "net": 4342,
    "commits": 45
  },
  {
    "name": "Jane Smith",
    "added": 3421,
    "removed": 654,
    "net": 2767,
    "commits": 38
  }
]
```

### CSV Format

```csv
No,Contributor,Commits,Added,Removed,Net
1,"John Doe",45,5234,892,4342
2,"Jane Smith",38,3421,654,2767
```

## Use Cases

- 📈 **Team Performance**: Track team contributions over time
- 🎯 **Sprint Reviews**: Analyze contributions during specific sprints
- 📊 **Reports**: Generate contribution reports in various formats
- 🏅 **Recognition**: Identify top contributors for recognition
- 📅 **Historical Analysis**: Compare contributions across different time periods
- 🔍 **Code Reviews**: Understand contribution patterns

## Author Name Grouping

Git-leaderboard can intelligently detect and merge similar author names using Levenshtein distance. This is useful when contributors have multiple name variations in git history.

### How it works

The tool compares all author names and calculates a similarity score (0-1, where 1 is identical). Names exceeding the threshold are flagged as similar.

**Examples of names that can be grouped:**
- "ahmed farghaly" and "ahmedfarghaly"
- "Abdulmajeed Jamaan" and "Abdulmajeed-Jamaan"
- "Saad5400" and "Saad Batwa" (with lower threshold)

### Interactive Mode

Without `--group-similar`, you'll be prompted for each similar pair:
```
Similar authors detected (similarity: 85.7%):
  1) ahmed farghaly
  2) ahmedfarghaly
Group these authors together? (Y/n):
```
Press Enter (default: yes) or type 'n' to skip.

### Automatic Mode

Use `--group-similar` to automatically merge all similar names:
```bash
git-leaderboard --group-similar --similarity-threshold 0.5
```

### Adjusting Sensitivity

- **Higher threshold (0.7-0.9)**: Only very similar names (typos, capitalization)
- **Medium threshold (0.4-0.6)**: Catches variations with spaces, punctuation
- **Lower threshold (0.2-0.3)**: More aggressive, may group unrelated names

## Tips

- Use `--since` and `--until` to analyze specific time periods
- Combine `--sort` with `--show-commits` for detailed insights
- The bar chart scales based on your sort metric (`--sort added` shows bars for lines added)
- Export to CSV for use in spreadsheets and further analysis
- Use `--exclude` to filter out bot accounts (dependabot, renovate, etc.)
- Pipe JSON output to tools like `jq` for advanced filtering
- Start with interactive mode (no `--group-similar`) to review similar names before auto-grouping

## License

MIT

## Author

Saad5400

## Repository

https://github.com/Saad5400/git-leaderboard
