# GitHub Activity & Stats — Diagnosis & Fix

## What's broken and why

| Badge | URL used | Status | Root cause |
|---|---|---|---|
| GitHub Stats | `github-readme-stats.vercel.app/api?...` | ⚠️ Intermittent | Shared public Vercel instance frequently hits rate limits / gets paused (503 `DEPLOYMENT_PAUSED`). Not a problem in your repo. |
| Top Languages | `github-readme-stats.vercel.app/api/top-langs/?...` | ⚠️ Intermittent | Same shared instance, same issue. |
| GitHub Streak | `github-readme-streak-stats.herokuapp.com/?...` | ❌ Dead | Heroku discontinued free dynos — this domain no longer resolves to a live app. The project moved to `streak-stats.demolab.com`. |

## Drop-in replacement

Replace your current "GitHub Activity & Stats" section with this:

```markdown
### 📊 GitHub Activity & Stats

[![Dipankar's GitHub Stats](https://github-readme-stats.vercel.app/api?username=dipankar-datasci&show_icons=true&theme=tokyonight&count_private=true)](https://github.com/dipankar-datasci)

[![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=dipankar-datasci&layout=compact&theme=tokyonight)](https://github.com/dipankar-datasci)

[![GitHub Streak](https://streak-stats.demolab.com/?user=dipankar-datasci&theme=tokyonight)](https://github.com/dipankar-datasci)
```

Only change from your original: `github-readme-streak-stats.herokuapp.com` → `streak-stats.demolab.com`.

## If the Stats/Top Languages cards still don't render reliably

The shared `github-readme-stats.vercel.app` instance is well known for going down under load. For a permanent fix, self-host your own copy (free):

1. Fork **anuraghazra/github-readme-stats** on GitHub.
2. Go to vercel.com → New Project → import your fork.
3. Deploy (no config needed for the basic card).
4. Optionally add a `PAT_1` environment variable in Vercel with a GitHub personal access token (no scopes needed) — this raises your rate limit and shows private repo stats if `count_private=true`.
5. Replace `github-readme-stats.vercel.app` in your badge URLs with your new deployment URL (e.g. `your-project-name.vercel.app`).

For the streak card, the same repo maintainer (DenverCoder1/github-readme-streak-stats) supports a similar one-click Vercel self-host via their `vercel` branch, using the same PAT approach.

## Also worth checking

- Make sure `dipankar-datasci` is your exact GitHub username in every URL (case-sensitive).
- If you just pushed the fix, GitHub/Vercel image caches can take a few minutes to refresh — hard-refresh (Ctrl+Shift+R) before assuming it's still broken.
- Contribution stats only count if your commits are made with the email linked to your GitHub account.
