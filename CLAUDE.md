# Faber Bracket Battle — how to record a match result

This repo is a static GitHub Pages site. The only files that matter are `index.html`
and `OG-image.png`. **All match results live in ONE place:** the JSON inside the
`<script id="results-data" type="application/json">…</script>` block near the bottom
of `index.html`.

## To record a result
When the user gives a score (e.g. "Mexico beat Ecuador 2-0" or "France 3 Sweden 0"):

1. Look up the **match number** in the table below.
2. Add or update that match's entry inside the `results-data` JSON block in `index.html`.
3. Commit and push.

**Entry format** — `a` = goals for the team listed FIRST in the table, `b` = goals for
the team listed SECOND. `winner` must be spelled **exactly** like the team name in the table.

```json
"79": { "winner": "Mexico", "a": 2, "b": 0 }
```

- **Penalty shootout:** record the score and add `"so": true`, e.g.
  `"74": { "winner": "Paraguay", "a": 1, "b": 2, "so": true }`
- Only `winner` affects the standings; `a`/`b` are just the displayed score.
- Keep the existing entries; just add the new one (valid JSON, comma-separated).

Then:
```
git add index.html
git commit -m "Result: M79 Mexico 2-0 Ecuador"
git push
```
GitHub Pages redeploys in ~1 minute and everyone sees the updated standings.

## Match-number reference (spell team names exactly like this)

**Round of 32**
| # | Match | | # | Match |
|----|-------|---|----|-------|
| 73 | Canada vs South Africa | | 81 | USA vs Bosnia & Herzegovina |
| 74 | Germany vs Paraguay | | 82 | Belgium vs Senegal |
| 75 | Netherlands vs Morocco | | 83 | Portugal vs Croatia |
| 76 | Brazil vs Japan | | 84 | Spain vs Austria |
| 77 | France vs Sweden | | 85 | Switzerland vs Algeria |
| 78 | Côte d'Ivoire vs Norway | | 86 | Argentina vs Cabo Verde |
| 79 | Mexico vs Ecuador | | 87 | Colombia vs Ghana |
| 80 | England vs Congo DR | | 88 | Australia vs Egypt |

**Round of 16** (teams come from earlier results): 89 = winners of 74 & 77 · 90 = 73 & 75 ·
91 = 76 & 78 · 92 = 79 & 80 · 93 = 83 & 84 · 94 = 81 & 82 · 95 = 86 & 88 · 96 = 85 & 87
**Quarterfinals:** 97 = 89 & 90 · 98 = 93 & 94 · 99 = 91 & 92 · 100 = 95 & 96
**Semifinals:** 101 = 97 & 98 · 102 = 99 & 100
**Third place:** 103 = losers of 101 & 102 · **Final:** 104 = winners of 101 & 102

For matches 89+ the two teams depend on prior results. `winner` is what counts; for
`a`/`b`, list the goals in the order the two teams appear on that match's page (if unsure,
the score is cosmetic — the winner is what drives the standings).

## Notes
- Team spellings that matter: `Côte d'Ivoire`, `Congo DR`, `Bosnia & Herzegovina`,
  `Cabo Verde`, `South Africa`, `USA`.
- Don't change anything else in `index.html` — only the `results-data` block.
- The page is read-only for viewers; results only change by editing this file.
