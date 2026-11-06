# NA3 — Product and technical specification (v0.1)

## 1. Vision and boundaries
NA3 is a single-player, offline-first Android serious game for adults aged 18+. It blends a growing pixel-art oak tree, small real-life behavioral experiments, and optional reflective journaling. The initial narrative paths are Enneagram types 2, 6, and 9. Enneagram is a **narrative self-exploration framework**, not a validated diagnostic assessment. Do not claim therapeutic efficacy or provide diagnosis, treatment, crisis support, or clinical scoring.

**Core design principle:** progress is not contingent on perfection. Skipped missions, pauses, and failed attempts never cause the tree to wither, remove previously earned growth, or shame the player. Attempts and reflection can count as meaningful engagement.

## 2. Audience, platform, and experience
- Audience: 18+; Italian UI/content first; localization-ready.
- Target: Android phone, portrait layout; touch controls; 60 fps target where hardware permits; responsive safe areas.
- Offline-first: no login, analytics, advertising, push notifications, cloud sync, or AI-generated personalized advice in MVP.
- Visuals: original cohesive pixel art, nearest-neighbor texture filtering, stable base resolution scaled to common phone aspect ratios; no copyrighted asset copying.
- Accessibility: readable text sizes, sufficient contrast, reduced-motion setting, clear touch targets, screen-reader limitations documented if any.

## 3. Game loop
1. Open the grove and view oak growth.
2. Choose a mission from three optional suggestions (easy, medium, challenging) based on selected path.
3. Attempt an action in real life; mark `attempted`, `completed`, or `skipped` without penalty.
4. Optionally log a short reflection (emotion, difficulty, learning, free text).
5. Earn non-punitive growth points for participation and reflection; unlock cosmetic tree stages and narrative milestones.

**Important:** no coercive streaks, daily punishment, or comparison leaderboard. Player can switch path and pause missions at any time.

## 4. MVP screens
1. Onboarding: age gate (self-declaration 18+), concise purpose/limitations/privacy notice, path selection (2/6/9), reduced-motion toggle.
2. Grove/Home: animated oak, growth stage, gentle progress summary, navigation.
3. Missions: 3 suggestions, details, start/record status, replacement option, safety/comfort skip.
4. Reflection: optional mood word, perceived challenge (1–5), prompt, optional note; save/delete.
5. Journey: growth timeline, completed/attempted missions, path milestones.
6. Settings: change path, export data as JSON, delete all local data with confirmation, reduced motion, privacy and non-clinical disclaimer.

## 5. Content model
Mission: `id`, `path` (2|6|9), `title`, `description`, `difficulty` (1|2|3), `prompt`, `tags`, `contraindication_note?`, `locale`, `version`, `active`.
MissionEvent: `event_id`, `mission_id`, `timestamp`, `status` (`attempted|completed|skipped`), `reflection_id?`, `growth_awarded`.
Reflection: `id`, `timestamp`, `emotion?`, `challenge?`, `insight?`, `note?`.
PlayerState: `schema_version`, `created_at`, `selected_path`, `growth_points`, `tree_stage`, `settings`, `events`, `reflections`.

Initial mission themes:
- Type 2: boundaries, receiving help, acknowledging own needs.
- Type 6: calibrated trust, tolerating uncertainty, self-directed decisions.
- Type 9: voicing preferences, initiating action, navigating mild disagreement.

Mission wording must be gentle and consent-aware; avoid exposing players to unsafe interpersonal situations, encouraging confrontation with abusive persons, or replacing professional care.

## 6. Progression (provisional tuning)
- 11 oak stages, from acorn to mature tree; all unlocks cosmetic/narrative, not clinical ratings.
- Suggested starting rule: +5 points for an attempted mission, +5 additional for a completed mission, +3 for an optional reflection; max once per mission event. Skips yield 0 but never lose points.
- Suggested stage thresholds: [0,10,25,45,70,100,140,185,235,290,350]. These are *game-balance placeholders* to revise through playtesting.
- No consecutive-day streaks or decay. Repeating a mission is allowed with an explicit cooldown to prevent accidental point farming.

## 7. Architecture
- Engine: Godot 4.x stable, GDScript, 2D project; no external runtime services.
- Modular scene tree: `scenes/onboarding`, `scenes/grove`, `scenes/missions`, `scenes/reflection`, `scenes/journey`, `scenes/settings`.
- Scripts: `scripts/domain`, `scripts/services`, `scripts/ui`.
- Content: versioned JSON under `content/it/missions.json` and `content/it/strings.json`.
- Art: `assets/pixel/` with source attribution file; original placeholders acceptable for first vertical slice.
- Services: `SaveService`, `MissionService`, `ProgressionService`, `NavigationService`; autoload only where justified.
- Persist in `user://` with atomic temp-write + rename, schema version, validation, and graceful recovery on corruption; keep a backup and test migration.
- JSON export via Android-compatible save/share strategy, or document the initial MVP limitation and implement export before release.
- No collection or transmission of personal journal data. Sensitive text must not be logged in release builds.

## 8. Safety, privacy, and evidence
- In-app wording: educational/self-reflection game, not a diagnostic or psychotherapy tool; no promises of improved self-esteem.
- Do not present Enneagram type selection as scientifically validated profiling.
- No mandatory journaling; privacy-first local storage; clear deletion.
- For distressing content, permit stopping and suggest contacting a qualified professional without intrusive crisis messaging on ordinary screens.
- Before public distribution: review privacy disclosures, platform policies, accessibility, and any applicable medical-device implications if claims or features change.

## 9. Testing and acceptance
- Unit tests (or headless Godot test scripts) for progression thresholds, reward idempotency, serialization, corrupted save handling, and path switching.
- Smoke test all screens and back navigation, persistence across restart, offline behavior, no permission prompts not strictly needed.
- Android debug APK build via reproducible export presets when SDK/export templates available; otherwise document exact unmet prerequisites, do not claim build success.
- Acceptance: a new user can select type 2/6/9, view oak, pick a mission, record an attempt, optionally reflect, see stage progress, restart without data loss, export/delete data.

## 10. Explicitly out of scope for first playable version
Cloud accounts, social features, paid features, chatbots, clinical assessments, push notifications, iOS release, full 9-type content, advanced procedural art.

## 11. Definition of done for MVP
Runs offline on a real Android device; no blocking errors in core flow; save/reload and deletion verified; 9 reviewed missions minimum (3 per path), 11 visually distinct tree stages (placeholder art may be replaced before public launch), documentation and privacy text included, automated test suite passing, debug APK generated and manually tested.

## 12. Open product decisions
Precise art direction/palette, mission review by clinical owner, balancing of stage progression, localization beyond Italian, whether to permit journal export as plain JSON (privacy trade-off), Android minimum version, and eventual public distribution channel.
