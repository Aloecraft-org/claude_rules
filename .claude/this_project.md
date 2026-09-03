# This project

<!-- Per repo. This is the only file that changes between repos.
     human-surfaces.md defines the grades; this file assigns them. -->

## What this is

claude_rules: the canonical home of the shared rule set. Other repos get
`rules/human-surfaces.md` from here (copy, symlink, or submodule) and
write their own `this_project.md` against it. This repo contains no
program code, only the rules and the documents explaining them.

## Surfaces

| path | grade |
|------|-------|
| `*`  | tool  |

Every file here is read and hand-edited by the human. Prose rules apply
in the spirit of the code rules: no section that isn't load-bearing, no
elaboration beyond what a rule needs to be followed.

## Project notes

- `rules/human-surfaces.md` must stay repo-invariant. Anything
  project-specific belongs in a consuming repo's `this_project.md`,
  never here. If an edit to the rules file only makes sense for one
  repo, it is in the wrong file.
- Keep the rules file under 200 lines; it loads into every session of
  every consuming repo.
- Changes to grade definitions change behavior everywhere at once.
  Propose them in conversation before writing them.