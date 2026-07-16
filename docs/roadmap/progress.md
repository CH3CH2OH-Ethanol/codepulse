# CodePulse Learning Progress

## Current Position

- Current milestone: M0 — Environment, Terminal, and Git
- Current learning unit: Not started
- Status: Ready to begin
- Last updated: 2026-07-17

## Next Learning Unit

Inspect and understand the current development environment:

- terminal and Zsh;
- PATH and command resolution;
- Java and the installed JDKs;
- Node.js and NVM;
- npm;
- Git;
- why Maven Wrapper will be used instead of requiring global Maven.

The first unit should remain read-only until the learner understands which
executables are currently being selected.

## Confirmed Environment

- Operating system: macOS on Apple Silicon.
- Shell: Zsh.
- Java: Java 21 is available and currently selected.
- Additional JDKs: Java 17 and Java 11 are also installed.
- NVM: installed and configured in `.zshrc`.
- NVM-managed Node.js: Node.js 24.14.0 is installed and configured as the NVM
  default.
- Homebrew Node.js: Node.js 25.9.0 is also installed.
- Important observation: commands that do not load NVM may resolve to the
  Homebrew Node.js 25 installation instead of Node.js 24.
- npm: available with Node.js.
- Maven: no global `mvn` command is installed.
- Git: installed.
- VS Code application: version 1.124.2 was observed.
- VS Code `code` shell command: not currently available in the inspected shell.

These observations are a starting point, not a request to install or remove
anything.

## Current Product Decisions

- The primary goal is learning Spring, TypeScript, and engineering practice.
- The learner writes the main implementation.
- The Agent teaches, defines tasks, reviews, and summarizes.
- The first product version targets no more than 30 students on one local
  network.
- The teacher reads synchronized code and makes the judgment about whether help
  is needed.
- The first version shows the current active file and two activity timestamps.
- Five minutes is the initial inactivity highlight threshold.
- Students explicitly join and select a workspace.
- The teacher configures an extension allowlist.
- The first version may export final file snapshots but not edit history.
- Run-result detection and remote classroom access are deferred.

## Mandatory Agent Boundary

Without explicit user authorization, the Agent must not:

- modify project files;
- create scaffolding;
- install dependencies;
- write the implementation;
- apply automated fixes;
- advance to a later learning unit.

The Agent may read, explain, define a task, ask guiding questions, and review
the learner's work.

## Completed Learning Units

None yet.

## Learning Unit Record Template

Copy this section when a unit is accepted:

```text
### YYYY-MM-DD — Unit title

- Milestone:
- Goal:
- Work completed:
- Concepts learned:
- Important decisions:
- Tests or checks:
- Git commit:
- Remaining questions:
- Next unit:
```

## Immediate Next Step

Begin M0 Unit 1 by tracing how the shell chooses `java`, `node`, `npm`, and
`git`. The learner should run and interpret the commands with guidance rather
than having the environment changed automatically.
