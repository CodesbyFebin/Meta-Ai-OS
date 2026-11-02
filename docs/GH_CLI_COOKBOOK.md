# gh CLI cookbook: 50 commands for repo growth and maintenance

Written against **gh 2.103.0**. Set the repo once so you can paste commands:

```bash
export R=CodesbyFebin/Meta-Ai-OS
```

Commands marked ✅ were run read-only against this repo while writing this guide.
⏳ means read-only but it only returns data after CodeQL has run once.
Commands that change things (✏️) were either run once to set up this repo (noted) or are
documented from `gh help` without being run. Review every ✏️ command before running it.

## Repo profile and discoverability
1. ✅ `gh repo view $R` : README and About as visitors see it.
2. ✅ `gh repo view $R --json description,homepageUrl,repositoryTopics,stargazerCount,forkCount` : About fields as JSON.
3. ✏️ `gh repo edit $R --description "Self-hosted AI business OS…"` : set the description (≤350 chars). Used for this repo.
4. ✏️ `gh repo edit $R --add-topic self-hosted --add-topic ai-agents` : add topics (max 20). Used for this repo.
5. ✏️ `gh repo edit $R --remove-topic old-topic` : remove a topic.
6. ✏️ `gh repo edit $R --homepage https://codesbyfebin.github.io/Meta-Ai-OS/` : set the website link (only once the page is live).
7. ✏️ `gh repo edit $R --enable-discussions --enable-issues` : turn on community features. Used for this repo.
8. ✏️ `gh repo edit $R --enable-wiki=false` : turn off the wiki if docs live in the repo.
9. ✅ `gh api repos/$R/topics --jq .names` : list topics via the REST API.
10. ✅ `gh api repos/$R/community/profile --jq '{health_percentage, files: (.files|keys)}'` : community-health checklist (README, CoC, CONTRIBUTING…).

## Traffic and audience (owner/push access needed)
11. ✅ `gh api repos/$R/traffic/views --jq '{count, uniques}'` : views over the last 14 days.
12. ✅ `gh api repos/$R/traffic/clones --jq '{count, uniques}'` : clones over the last 14 days.
13. ✅ `gh api repos/$R/traffic/popular/referrers` : which sites send visitors.
14. ✅ `gh api repos/$R/traffic/popular/paths` : most-viewed pages in the repo.
15. ✅ `gh api repos/$R/stargazers -H "Accept: application/vnd.github.star+json" --paginate --jq '.[].starred_at'` : star timestamps (to see real velocity).
16. ✅ `gh api repos/$R/subscribers --jq length` : number of watchers on the first page.

## Issues
17. ✅ `gh issue list -R $R --label "good first issue"` : starter tasks.
18. ✏️ `gh issue create -R $R --title "…" --body-file issue.md --label "good first issue"` : open an issue from a file. Used for this repo.
19. ✏️ `gh issue edit 12 -R $R --add-label "help wanted"` : add a label.
20. ✏️ `gh issue comment 12 -R $R --body "Thanks! Fixed in #34."` : reply.
21. ✏️ `gh issue close 12 -R $R --reason "not planned" --comment "…"` : close with a reason.
22. ✏️ `gh issue pin 12 -R $R` : pin a roadmap or welcome issue.
23. ✅ `gh issue list -R $R --search "no:assignee sort:created-asc" --state open` : untriaged backlog.
24. ✅ `gh search issues --repo $R --label bug --state open` : search across issues.

## Labels
25. ✅ `gh label list -R $R` : list labels.
26. ✏️ `gh label create "good first issue" -R $R --color 7057ff --description "Good for newcomers" --force` : create or update a label.
27. ✏️ `gh label clone owner/other-repo -R $R` : copy a label set from another repo.

## Pull requests
28. ✏️ `gh pr create -R $R --base main --head my-branch --title "…" --body-file pr.md` : open a PR. Used for this repo.
29. ✅ `gh pr list -R $R --state open` : open PRs.
30. ✅ `gh pr checks <n> -R $R` : CI status for a PR.
31. ✅ `gh pr view <n> -R $R --comments` : read a PR with comments.
32. ✅ `gh pr diff <n> -R $R --name-only` : changed files.
33. ✏️ `gh pr checkout <n> -R $R` : check a PR out locally to test it.
34. ✏️ `gh pr review <n> -R $R --approve --body "LGTM"` : review (you can't approve your own PR).
35. ✏️ `gh pr merge <n> -R $R --squash --delete-branch` : merge when ready.

## Releases
36. ✅ `gh release list -R $R` : list releases.
37. ✏️ `gh release create v0.1.0 -R $R --title "v0.1.0" --notes-file notes.md --prerelease` : publish a release with your own notes.
38. ✏️ `gh release create v0.2.0 -R $R --generate-notes` : notes generated from merged PRs using `.github/release.yml`.
39. ✏️ `gh release upload v0.1.0 -R $R ./demo.gif` : attach files.
40. ✅ `gh release view --json tagName,publishedAt,url -R $R` : latest release details.

## CI and security
41. ✅ `gh run list -R $R -L 10` : recent workflow runs.
42. ✅ `gh run view <run-id> -R $R --log-failed` : only the failing log lines.
43. ✏️ `gh run rerun <run-id> -R $R --failed` : rerun failed jobs.
44. ✏️ `gh workflow run ci.yml -R $R --ref main` : trigger a workflow manually (needs `workflow_dispatch`, which CI has).
45. ✅ `gh workflow list -R $R` : workflows and their state.
46. ⏳ `gh api repos/$R/code-scanning/alerts --jq '.[] | {rule: .rule.id, state}'` : CodeQL alerts (after the first scan).
47. ✏️ `gh secret set MY_SECRET -R $R` : set an Actions secret from a prompt (never put the value in the command line or chat).
48. ✏️ `gh api -X PUT repos/$R/private-vulnerability-reporting` : enable private vulnerability reporting (linked from SECURITY.md).

## Discovery and research
49. ✅ `gh search repos "self-hosted ai agents" --sort stars --limit 10` : see how similar projects describe themselves.
50. ✅ `gh browse -R $R --settings -n` : print the Settings URL (where you upload the social preview image; the API can't do it).
