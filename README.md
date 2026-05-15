# Weekly GitHub Contribution Stats

Per-user weekly summary of commits, lines added/deleted, PRs opened, and project items created/moved.

## Important: must be run from an actual cloned repository

This script relies on `git log` against a real local clone of the target repository to count commits and lines. **It will not work if run from this folder or any folder that is not itself a clone of the repo you want to analyze.**

Before running:

1. `git clone` the repository you want to analyze (e.g. `drew-csci/opportunity_app_srping_2026`).
2. `cd` into that clone.
3. Run the script from there with `--repo .` (or pass an absolute path to the clone via `--repo`).

The `--repo_full owner/repo` argument is the GitHub identifier used for `gh` API calls (PRs, project items). The `--repo` argument is the filesystem path to the local clone used for `git log`. Both must point at the **same** project.

You also need:

- `git` on PATH
- `gh` CLI authenticated (`gh auth login`) for PR and Project v2 data
- `pip install -r requirements.txt` (and `pandas` + `openpyxl` if you use `--name_fix_file`)

## Usage examples

Run these from inside the corresponding cloned repo:

```
# opportunity_app_spring_2026
python grading_github_statistics_2025.py --repo . --all_refs \
  --repo_full drew-csci/opportunity_app_srping_2026 \
  --start_date 2026-01-15 --end_date 2026-05-15 \
  --org_project_owner drew-csci --org_project_number 6

# discovery_hub_spring_2026
python grading_github_statistics_2025.py --repo . --all_refs \
  --repo_full drew-csci/discovery_hub_spring_2026 \
  --start_date 2026-01-15 --end_date 2026-05-15 \
  --org_project_owner drew-csci --org_project_number 7

# minecraft_mod_spring_2026
python grading_github_statistics_2025.py --repo . --all_refs \
  --repo_full drew-csci/minecraft_mod_spring_2026 \
  --start_date 2026-01-15 --end_date 2026-05-15 \
  --org_project_owner drew-csci --org_project_number 5

# f25_opportunity
python grading_github_statistics_2025.py --repo . --all_refs \
  --repo_full drew-csci/f25_opportunity \
  --start_date 2025-08-25 --end_date 2025-12-12 \
  --org_project_owner drew-csci --org_project_number 3 \
  --user_project_owner alrudniy --user_project_number 7 \
  --name_fix_file fix_github_names.xlsx
```

## Output

Two timestamped CSVs are written to the current directory:

- `<out_csv>_detailed_<timestamp>.csv` — one row per user per week
- `<out_csv>_summary_<timestamp>.csv` — pivot with users as rows, weeks as columns
