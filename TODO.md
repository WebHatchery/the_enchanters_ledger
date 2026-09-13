# TODO — The Enchanter's Ledger

## Standards alignment

- [ ] Expose testable logic through `src/lib.rs` and make `main.rs` consume it;
  migrate all tests and test-only helpers from `src/` into `tests/` before
  expanding coverage. Consolidate related cases toward five per major feature,
  preserving regression coverage and explaining necessary exceptions (§11).
- [ ] Split oversized functions by responsibility, starting with
  `Game::apply_action`, `GameSession::evaluate`, and `draw_drawing_slate`.
  Extract action handlers from the 763-line `src/game.rs`; keep functions within
  100 lines and every Rust file within 800 total physical lines (§2.2, §4.1).
- [ ] Extract pure evaluation, delivery accounting, and research calculations
  from `src/state/evaluate.rs` and `src/state/work.rs`; apply results through
  explicit session actions and preserve accounting regressions (§5.1).
- [ ] Use `macroquad_toolkit::include_json!` for embedded assets in `src/data.rs`,
  `src/ladder.rs`, and `src/rune_drawing/templates.rs`; initialize them at startup
  with source-labeled errors instead of lazy parsing that can panic (§5.3, §6).
- [ ] Validate unique IDs, rune/category references, nonempty commission lists,
  template geometry, ladder group indices, and balance ranges before indexing
  job lists or silently skipping unknown runes. Cover invalid inputs (§5.3, §6).
- [ ] Move hardcoded balance and recognition settings into typed JSON under
  `assets/`, including category scales, containment coefficients, recognition
  thresholds, and delivery/research rewards (§5.3).
- [ ] Move UI labels, tutorial prompts, notifications, and generated player text
  from `src/ui/`, `src/state/text.rs`, `src/state/tutorial.rs`, and
  `src/reading/sentences.rs` into loaded JSON (§5.3).
- [ ] Add visible touch controls for partial erasing on both slates, cancelling
  guide selection, and editing the keeper's name. Use toolkit input support and
  verify browser play without a physical keyboard or right mouse button (§7.5).
- [ ] Rewrite tutorial steps to name the visible `Interpret` control and required
  drawing gesture; update `game_page.json` and README controls to pair shortcuts
  with their visible tap controls (§7.5).
- [ ] Reject unrecognized saves in `src/state/save.rs`: the all-optional
  `LegacySave` accepts unrelated objects as a fresh workshop. Validate recognized
  legacy/current payloads and preserve the session on load failure (§6).
- [ ] Remove the unused `assets.zip` load in `Game::new` while the texture manifest
  is empty, or handle its result explicitly if runtime assets are introduced (§6).
- [ ] Add missing module-purpose `//!` comments, including state and UI child
  modules; correct `tests/code_standards.rs` to describe the gate as counting all
  physical lines, including tests (§2.2, §9.2).

## Recognition and performance

- [ ] Fix sparse-resampling confusion between `safer` and `sphere` with a
  density-stable corner measure; retune affected template profiles and remove
  the tracked confusion only after the confusion/property gates pass.
- [ ] Fix diagram grouping for the detached strokes of `sound` and `larger`;
  replace `fragmenting_runes_still_fragment` with positive regressions and remove
  their reference/manual test exclusions.
- [ ] Replace window-based overlap/contamination recovery with bounded candidate
  segmentation in `src/rune_diagram/recognition.rs`, preserving recognition and
  performance regression coverage.
- [ ] Add release performance validation for large diagrams in CI, measuring the
  100 ms native and 250 ms browser/WASM targets rather than only the current
  five-second debug sanity bound.

## Content and balance

- [ ] Author reading-based ladder drills using the existing `groups` support in
  `assets/data/ladder.json`; verify the resulting modifier/effect relationships,
  not just rune counts, when each generated diagram is interpreted.
- [ ] Tune root and nested containment budgets against representative commissions
  and ladder diagrams; document intended capacity boundaries and preserve them
  in focused regression cases.
