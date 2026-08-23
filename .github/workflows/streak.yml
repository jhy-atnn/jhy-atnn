name: Update Streak Stats

on:
  schedule:
    - cron: '0 0 * * *' # Automatically updates daily at midnight UTC
  workflow_dispatch: # Gives you a button to update it manually just in case

jobs:
  update-streak:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4

      - name: Generate streak stats
        uses: be-next/github-streak-stats-action@v1
        with:
          username: ${{ github.repository_owner }}
          token: ${{ secrets.GITHUB_TOKEN }}
          output-path: streak-stats.svg
          theme: dark
          hide-border: false
          background: 161B22        # GitHub elevated surface (card bg)
          stroke: 30363D             # GitHub default border
          ring: F0883E               # GitHub "attention" orange (flame ring)
          fire: F0883E               # matches ring for a cohesive flame
          currStreakNum: E6EDF3      # GitHub primary text
          sideNums: E6EDF3           # GitHub primary text
          currStreakLabel: F0883E    # orange, matches original design
          sideLabels: 8B949E         # GitHub muted text
          dates: 6E7681              # GitHub dimmer muted text

      - name: Commit changes
        run: |
          git config user.name "github-actions"
          git config user.email "github-actions@users.noreply.github.com"
          git add streak-stats.svg
          git commit -m "Update streak stats" || exit 0
          git push
