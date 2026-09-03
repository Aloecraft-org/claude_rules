# claude_rules

Shared Claude Code rules for writing code with two readers in mind: the
agent that maintains it and the human who reads a few declared surfaces.

The problem this solves: agent-written code is airtight but flat. The
five lines that matter carry the same visual weight as the 395 that
don't, examples bury their point under defensive boilerplate, and small
tools accrete flags and helpers nobody asked for. General instructions
like "be readable" make it worse; they get applied everywhere by
judgment and hollow out code that needed to stay complete. These rules
replace judgment with declaration: readability is opt-in, by path, at a
stated grade.

## Layout

```
claude_rules/
  .claude/
    this_project.md          # declaration for this repo itself
    rules/
      human_surfaces.md      # the invariant rule set
  README.md
```

## The two files

**`human_surfaces.md`** is byte-identical in every repo. It defines
three grades and their rules:

- `maintainer` (default): complete and correct; no brevity rules apply.
- `example`: exists to be read and retyped; may omit error handling if
  it says so with a marker; must fit on one screen and still run.
- `tool`: read, run, and hand-edited by the human; complete, but only
  as complete as its spec requires. Nothing the spec doesn't name.

It also carries the free-for-everyone shape rules: dense files open with
a surface block (entry points, configurables, fan-outs), nothing that
belongs there is declared elsewhere in the file, and depth sections are
marked skippable.

**`this_project.md`** is the only file that changes between repos. It
assigns grades to paths (often just `*: tool` for a small tool repo),
points at the spec, and holds project-specific notes. The one in this
repo doubles as the template.

## Using it in a repo

1. Get `human_surfaces.md` into `.claude/rules/` (copy, symlink, or
   submodule; Claude Code resolves symlinks in the rules directory).
2. Write `.claude/this_project.md` from the template.
3. Add one line to the repo's `CLAUDE.md` so it loads at launch:

   ```
   @.claude/this_project.md
   ```

Files under `.claude/rules/` load automatically; `this_project.md` does
not, hence the import. Verify with `/context` in a session: both files
should appear under Memory files.

## Enforcement

The rules are context, not enforcement. Two things are cheap to enforce
mechanically if drift shows up:

- The omission marker (`example: omits`) appearing outside
  example-grade paths: grep in CI, fail the build.
- Rules that must hold on every action belong in Claude Code hooks, not
  here.