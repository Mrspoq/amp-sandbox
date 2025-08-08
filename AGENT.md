# AGENT.md

Project: void-filter (primary). This file captures conventions for working with Amp using GitHub CLI as the default interface.

## Operating rules
- Prefer GitHub CLI (`gh`) over raw `git` for GitHub operations.
- Do not “try multiple variants until one works.” Plan and run a single validated command. Use `--help` and `gh auth status` to confirm assumptions before executing.
- If a local Git action fails (e.g., `git commit` environment edge cases), use `gh api` to create/update files instead of retrying different flags.
- Protocol: HTTPS (per `gh auth status`).
- Scope: Only operate on the `void-filter` project unless explicitly asked otherwise. Avoid cloning unrelated repos.

## Frequently used checks
- Auth status: `gh auth status -h github.com`
- Current user: `gh api user --jq '{login: .login, name: .name}'`
- Primary email: `gh api user/emails --jq 'map(select(.primary == true))[0].email'`
- Repo existence: `gh repo view <owner>/<repo> --json name -q .name`

## Repository lifecycle (void-filter)
- Create: `gh repo create <owner>/void-filter --public --description "Void Filter project" --add-readme`
- Clone (only when necessary): `gh repo clone <owner>/void-filter`
- View: `gh repo view <owner>/void-filter --web`

## Deterministic content updates (preferred)
- Get file SHA: `gh api repos/<owner>/void-filter/contents/<path> --jq .sha`
- Create/update: `gh api -X PUT repos/<owner>/void-filter/contents/<path> -f message='msg' -f content='BASE64' -f branch=main` (include `-f sha='<SHA>'` when updating)

## Local workflow (when using a clone)
- Branch: `git checkout -b <branch>`
- Stage/commit: `git add -A && git commit -m "<message>"`
- Push + PR: `git push -u origin <branch> && gh pr create -t "<title>" -b "<body>" -B main -H <branch>`

## Conventions
- Default branch: `main`.
- Commit messages: conventional commits (e.g., `chore: update config`).
- No speculative retries; run single, correct commands.

## Notes
- `user.name = Mrspoq`, `user.email = abbaceo@gmail.com` (configured).
- If `git commit` returns unexpected errors, switch to `gh api` for the change.

