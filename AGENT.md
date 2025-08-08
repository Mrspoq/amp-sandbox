# AGENT.md

This file captures conventions for working on this project with Amp, using GitHub CLI as the default interface.

## Defaults
- Use GitHub CLI (`gh`) for repo operations instead of raw `git` when possible.
- Git operations protocol: HTTPS (per `gh auth status`).
- Default branch: `main`.

## Frequently used commands
- Show auth: `gh auth status -h github.com`
- Set default git protocol to HTTPS: `gh config set git_protocol https`
- Create repo (already done): `gh repo create Mrspoq/amp-sandbox --public --add-readme`
- Clone: `gh repo clone Mrspoq/amp-sandbox`
- View in browser: `gh repo view --web`
- Create issue: `gh issue create -t "Title" -b "Body"`
- Create PR: `gh pr create -t "Title" -b "Body" -B main -H <branch>`

## Local workflow
- Create a branch: `git checkout -b <branch>`
- Commit: `git add -A && git commit -m "<message>"`
- Push and open PR: `git push -u origin <branch> && gh pr create -t "<title>" -b "<body>" -B main -H <branch>`

## Repo setup checklist (use `gh`)
- Branch protections (manual or via API):
  - Require PR reviews on `main`.
  - Require status checks to pass.
- CODEOWNERS: add `.github/CODEOWNERS` as needed.
- Templates: add `.github/ISSUE_TEMPLATE/` and `.github/pull_request_template.md`.
- CI: add `.github/workflows/ci.yaml` if needed.

## Notes
- Author configured: `user.name = Mrspoq`, `user.email = abbaceo@gmail.com`.
- Adjust in Git with `git config --global user.name "<name>"` and `git config --global user.email "<email>"`.
