# MDX support

- Task: Make the MDX posts in `gian.cool/src/data/blog/` available in Writer.
- Scope: Recognize MDX in workspace listings, search, recents, external file
  changes, single-file opens, links, file creation and macOS associations.
- Constraint: Keep the existing Markdown editor. Imports, JSX and expressions
  remain source text. Do not compile MDX or load project components.
- Reviewed: `open_target.rs`, `commands/fs.rs`, `commands/search.rs`,
  `commands/recents.rs`, `watcher.rs`, `paths.ts`, `wiki-links.ts`,
  the file picker, command palette, app manifests and blog samples.
- Decision: One extension list under `apps/desktop/shared/` feeds frontend
  helpers and the Rust path predicate. Tests check static bundle associations
  against that list.
- Verification: Extension and link regressions, nested workspace discovery,
  search, recents, subtree indexing and source-content round trips.
- Review: Rust/Tauri and QA plan reviews requested directory suffix handling,
  CLI help, wiki-link collision round trips and filename creation coverage.
- Implementation: Shared registry feeds all extension checks. Directory events
  keep subtree semantics. Explicit wiki extensions distinguish sibling files;
  ambiguous root targets start with `./` and collisions ignore case.
- Baseline: 790 frontend tests and 168 Rust tests pass.
- Browser QA: All 10 MDX posts in the user's blog directory load in the full
  editor playground and retain their source after editing and restoring text.
- Review: Rust/Tauri, frontend and QA reviews approve with no open findings.
- Validation: `vp check`, 808 frontend tests, 170 Rust tests, `cargo clippy`,
  `cargo fmt --check`, desktop build and website build pass. Existing warnings
  remain in unrelated code and tooling.
- Limits: Native watcher events and installed Finder associations need a
  packaged-app smoke test. Registry, discovery and manifest tests pass.
- Status: Complete.
