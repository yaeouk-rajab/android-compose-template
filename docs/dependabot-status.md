# Dependabot status

_Last updated: 2026-10-27. Starter template extracted from `lexicon-android`; update when the state changes._

## Configuration

- Ecosystems covered: gradle (`/`), github-actions (`/`).
- Grouping: Kotlin plugins grouped as `kotlin` (they must move together).
- Schedule: weekly.
- Ignore rules: none.

## State at last update

- Open Dependabot PRs: 0 (each merged or closed only after reading its checks).
- Default-branch CI: green at last check.
- Repository settings (read live 2026-10-10): public, `is_template` true, description set, default branch `main` (the only branch kept), secret scanning, push protection and Dependabot security updates enabled, dependency graph on (SBOM endpoint 200). Non-provider secret patterns and validity checks stay off: GitHub does not offer them on this user-owned public repo.
- Set by the repo owner through the API on 2026-10-10 (the session's proxy blocks repository-settings writes) and read back by the session the same day: private vulnerability reporting enabled (PUT 204), `delete_branch_on_merge` on (PATCH 200), repository topics set (PUT 200). Fork-PR workflow approval is `all_external_contributors` (read with the owner's token). Stale branches left over from squash-merged PRs were deleted after a fresh diff against `main` showed their content already on `main`.
- Alerts read 2026-10-10 with the repo owner's token: No Dependabot, code-scanning or secret-scanning alerts.
- Rescan 2026-10-11 repeated every dimension (open PRs, branches, CI on `main`, required contexts against the last merged PR's check runs, protection, `security_and_analysis`, private vulnerability reporting, dependency graph, `is_template`, description, topics, licence placeholders) and added one: whether the GitHub description actually describes this repo. Live result: no open PRs, `main` the only branch, CI on `main` green, every required context produced green by the last merged PR, protection unchanged, secret scanning, push protection and Dependabot security updates enabled, private vulnerability reporting on, SBOM 200, `is_template` true, description accurate, topics set, `LICENSE` filled in (2026, arb-rajab). The repo owner's token read 0 open Dependabot, code-scanning and secret-scanning alerts and fork-PR approval `all_external_contributors`. No new gaps.
- Rescan 2026-10-27 (a new loop after a gap in which Dependabot opened a fresh batch of PRs). Merged (squash) after reading each PR's check runs: #8, #9, #12, #13, #14. Merged from this session: #15 (force guava 33.7.2 (GHSA-xxph-c9ww-hj94) and regenerate the Gradle lockfile on a runner). New gap fixed: guava 33.2.1, 33.4.0 and 33.6.0 in `app/gradle.lockfile` (GHSA-xxph-c9ww-hj94) are forced to 33.7.2-jre in every configuration; the lockfile was regenerated on a runner with a temporary workflow that was removed before the merge (#15). Live result when this entry was written: main CI green, branch protection and required contexts unchanged and each context produced by the last merged PR's check runs, private vulnerability reporting on, dependency graph on (SBOM 200). Dependabot, code-scanning and secret-scanning alerts and the repository security settings are read with the owner's token, not by the session; their state is recorded after the owner's next read.
- Alerts and repository settings read 2026-10-27 with the owner's token (a new token for the account that owns the repos; the session's proxy cannot read them): open Dependabot, code-scanning and secret-scanning alerts 0 before the changes below; fork-PR workflow approval `all_external_contributors`; private vulnerability reporting on. Secret scanning, push protection and Dependabot security updates were set by the owner (PATCH 200, automated-security-fixes 204) and read back as `enabled`; the secret-scanning read lists no open alert.

## Time-limited exemptions

- None.

## Notes

- Merge policy (deliberate choice by the repo owner, the same blanket policy as the application repos): every PR, major-version dependency bumps included, is squash-merged as soon as all of its required checks are green, confirmed per PR. This repo is a code showcase with no business or sensitive dependency, so green checks are the only gate. Red, pending or conflicted PRs are fixed or closed instead.
- `main` protection (2026-10-10, read back): pull request required (0 approvals), enforced for admins, force pushes and deletions blocked, "require branches to be up to date" off (`strict` false) on purpose. Nobody pushes to `main` directly; status-log updates go through a PR too.
- Required contexts: `lint-and-test`, `instrumented-tests (30)`, `Secret scan (gitleaks)`. Nothing else is required on purpose: osv-scanner, npm audit, dependency review and CodeQL depend on a moving advisory database or run only on some events.
- Closed unmerged on 2026-10-10, each with an explanatory comment: #2 and #3 (superseded by #4, which bumped both with a lockfile regenerated on a runner). If Dependabot recreates one, apply the merge policy; the closure is not re-raised. Dependabot does not re-propose a major after its PR is closed, so a later upgrade is a manual change.
- Dependency locking is on: a Gradle bump also needs `app/gradle.lockfile` regenerated (`./gradlew :app:dependencies --write-locks`). The sandbox cannot run Gradle, so regenerate it on a runner (a temporary workflow on the PR branch, removed before merge), never by hand.
- #5 (Gradle wrapper 9.8.0 -> 9.8.1) merged 2026-10-10 with every required check green.
- `app/build.gradle.kts` forces `com.google.guava:guava` to 33.7.2-jre in every configuration (GHSA-xxph-c9ww-hj94). Regenerate `app/gradle.lockfile` on a runner after changing it; drop the rule once the build tooling ships a patched guava.

## Deferred (not re-raised each pass)

- Alert reads (Dependabot, code scanning, secret scanning) and Actions settings (fork-PR approval) are blocked for Claude sessions by the proxy; they are read and written with the repo owner's token on their own machine.
- The owner keeps the token's Administration, Contents and Secret scanning permissions and does not rotate it (deliberate, 2026-10-09, reconfirmed 2026-10-10 for the template repos).
- Dependabot commands (`@dependabot rebase`, `@dependabot recreate`) written by a Claude session are neutralised when the comment is posted (the mention is mangled, so Dependabot never sees it). Rebases and recreates of conflicted or stale PRs go through the owner's token; the session can only refresh a branch with the update-branch call or replace the PR with its own.
