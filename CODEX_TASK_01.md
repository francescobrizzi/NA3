# Codex assignment 01 — Create NA3 vertical slice

You are the implementation agent for a **new, clean repository** named `na3` (or `na3-reboot` if the name is occupied). Read `SPEC.md` as the source of truth. Do not copy code/assets from the prior NA3 project.

## Mission
Implement a small but runnable Godot 4.x Android-first, portrait, pixel-art prototype with a functioning offline game loop. Work in a feature branch `feat/vertical-slice-01`, commit changes, and open a pull request when GitHub access permits. Never overwrite the old repository. Do not publish to an app store.

## Implementation order
1. Scaffold Godot project, scenes, autoload services, content folder, README, LICENSE decision placeholder, `.gitignore`, CI workflow for headless validation.
2. Create onboarding with age self-declaration, purpose/limitations, and selection among Enneagram narrative paths 2, 6, 9.
3. Create home/grove scene with original placeholder pixel-art oak; implement first 3 visually distinct stages, while keeping data structures ready for 11 stages.
4. Create missions list with at least 3 reviewed-draft mission entries per path (9 total), using JSON. Show difficulty and an opt-out/skip.
5. Implement mission attempt/completion, optional reflection, deterministic non-punitive point awards, persistence and idempotency.
6. Add journey view and settings with local data deletion, path switching, and reduced motion. If export cannot be implemented in this slice, mark it visibly as pending and document it.
7. Add tests and run them; report exact commands, pass/fail output, and limitations.
8. If Android SDK/export templates are configured, build a debug APK and give its artifact location; otherwise document reproducible setup steps and leave APK status as NOT BUILT.

## Constraints
- Italian copy, no clinical efficacy claims, no diagnostic Enneagram language.
- No telemetry, network, ads, cloud storage, or unnecessary Android permissions.
- No penalizing missed days, no negative growth, no coercive streaks.
- User data stays local. Never print journal entries in logs.
- Avoid external copyrighted artwork. Use original pixel-art placeholders and document provenance.
- Keep implementation modular and simple; no premature infrastructure.

## Deliverables
- Runnable Godot source with clear folder structure.
- Tests and reproducible run/build instructions.
- `IMPLEMENTATION_REPORT.md`: implemented features, screenshots if available, test results, known gaps, exact build status, next recommended tasks.
- Pull request against a **new** repository if permissions permit; otherwise a commit-ready project tree with precise instructions for creating the repository.

## Definition of acceptance for this assignment
A fresh user can choose one of 3 paths, see the grove, view 3 relevant missions, record an attempt, write an optional reflection, observe growth, close/reopen and retain state. All essential paths run offline. No unsupported claims of completed Android builds.

## Agent autonomy
Proceed independently on implementation details consistent with `SPEC.md`. Ask for human input only for blocking credentials/permissions, clinical content approval, or irreversible/public release actions. Do not repeatedly ask the user to copy code manually.
