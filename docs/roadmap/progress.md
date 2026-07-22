# CodePulse Learning Progress

## Current Position

- Current milestone: M1 — Requirements and Architecture
- Current learning unit: M1 Unit 8 — Architecture Decision Records
- Status: M1 Unit 7 accepted; ready to begin Unit 8
- Last updated: 2026-07-22

## Next Learning Unit

Record the first important architecture choices, alternatives, consequences,
and unresolved risks without beginning implementation.

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

### 2026-07-18 — M0 Unit 1: Shell and PATH

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand the terminal, Zsh, processes, environment variables, PATH,
  and command resolution.
- Work completed: Inspected `$SHELL`, `$0`, `$$`, `PATH`, `command -v`, and
  `type -a`; compared temporary and persistent environment changes.
- Concepts learned: Shell invocation names, process IDs, parent and child
  process boundaries, PATH order, builtins, functions, external executables,
  and command-scoped environment assignments.
- Important decisions: Environment changes remain explicit; no shell startup
  files were modified.
- Tests or checks: Traced the selected `node` executable and temporarily
  changed PATH for one command without changing the current Shell.
- Git commit: None; this unit was read-only.
- Remaining questions: Persistent shell configuration will be revisited only
  when a project requirement needs it.
- Next unit: Compare NVM-managed Node.js with Homebrew Node.js.

### 2026-07-18 — M0 Unit 2: NVM and Homebrew Node.js

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand how two Node.js installations can coexist and how the Shell
  chooses between them.
- Work completed: Inspected the NVM Node.js executable, the Homebrew Node.js
  symlink, and both versions through explicit paths.
- Concepts learned: Version-manager directories, Homebrew Cellar paths,
  symbolic links, regular executable files, and bypassing PATH with an absolute
  path.
- Important decisions: CodePulse development uses the NVM-managed Node.js 24;
  the Homebrew Node.js installation remains available as the external `system`
  version.
- Tests or checks: Confirmed NVM Node.js `v24.14.0` and Homebrew Node.js
  `v25.9.0` execute independently.
- Git commit: None; this unit was read-only.
- Remaining questions: None blocking.
- Next unit: Select and pin Node.js 24 for the project.

### 2026-07-18 — M0 Unit 3: Project Node.js Version

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Distinguish the personal NVM default from a project-declared Node.js
  version.
- Work completed: Inspected NVM aliases, switched between NVM and `system`
  Node.js, and created `.nvmrc` with `24.14.0`.
- Concepts learned: NVM aliases, LTS aliases, current-Shell version selection,
  project version files, and exact versus major-version pinning.
- Important decisions: CodePulse pins Node.js `24.14.0` in `.nvmrc` for a
  reproducible learning environment.
- Tests or checks: `nvm use` read `.nvmrc` and selected Node.js `v24.14.0` with
  npm `11.9.0`.
- Git commit: `fd1a3f6` later committed `.nvmrc` together with the related M0
  Git ignore changes.
- Remaining questions: Automatic directory-based version switching is deferred
  because the project does not need extra Shell configuration yet.
- Next unit: Inspect Java installations and Java selection.

### 2026-07-18 — M0 Unit 4: Java Environment

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Distinguish the JDK, JRE, JVM, Java launcher, compiler, and `JAVA_HOME`.
- Work completed: Inspected four installed JDKs and directly executed the Java
  21 and Java 17 binaries selected by `/usr/libexec/java_home`.
- Concepts learned: JDK vendor and version, macOS Java discovery, command
  substitution, environment-variable scope, and the difference between local
  JDK selection and project requirements.
- Important decisions: CodePulse targets Java 21; no persistent `JAVA_HOME` is
  added because macOS already selects Temurin 21 correctly.
- Tests or checks: Confirmed the default Temurin JDK `21.0.5`, `javac 21.0.5`,
  and an explicit Temurin JDK `17.0.13` invocation.
- Git commit: None; this unit was read-only.
- Remaining questions: Maven's JDK selection will be inspected when a Maven
  project exists.
- Next unit: Understand npm and its relationship to Node.js.

### 2026-07-18 — M0 Unit 5: npm Environment

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand how npm relates to Node.js and where global packages belong.
- Work completed: Inspected the active npm executable, symlink target, shebang,
  global prefix, and the NVM and Homebrew npm installations.
- Concepts learned: npm CLI and registry roles, shebang execution through
  `/usr/bin/env node`, local versus global dependencies, Unix users, groups,
  and directory permissions.
- Important decisions: CodePulse will install TypeScript and build tools as
  project-local dependencies instead of relying on global npm packages.
- Tests or checks: Confirmed npm `11.9.0` executes through NVM Node.js 24 and
  uses the NVM version directory as its global prefix.
- Git commit: None; this unit was read-only.
- Remaining questions: `package.json`, lockfiles, and local dependency installs
  are deferred to the TypeScript milestone.
- Next unit: Understand Maven and Maven Wrapper.

### 2026-07-18 — M0 Unit 6: Maven Wrapper

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand why CodePulse will use Maven Wrapper without requiring a
  global Maven installation.
- Work completed: Verified that no global `mvn` command exists and compared the
  responsibilities of the JDK, Maven Wrapper, and `pom.xml`.
- Concepts learned: Build tools, dependency management, Wrapper-based tool
  pinning, command arguments, process exit status, and Shell control operators.
- Important decisions: CodePulse uses Maven rather than Gradle and will add the
  Maven Wrapper with the generated Java project instead of installing global
  Maven now.
- Tests or checks: `command -v java` returned status `0`; `command -v mvn`
  returned status `1`.
- Git commit: None; this unit was read-only.
- Remaining questions: Maven lifecycle phases, tests, and packaging are deferred
  to M3 and M4.
- Next unit: Practice Git status, diffs, staging, commits, and ignore rules.

### 2026-07-18 — M0 Unit 7: Git Status and Ignore Rules

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand the working tree, staging area, commits, and shared versus
  local ignore rules.
- Work completed: Moved the personal `AGENTS.md` rule to `.git/info/exclude`,
  configured a global `.DS_Store` ignore, replaced the broad `*.jar` rule with
  `target/`, staged selected files, reviewed the staged diff, and committed it.
- Concepts learned: Tracked, untracked, ignored, modified, and added states;
  `.gitignore`, `.git/info/exclude`, and global ignore scope; explicit staging;
  staged diffs; exit statuses; and commit inspection.
- Important decisions: Shared project rules ignore Maven build output, while
  personal Agent instructions and operating-system files remain local rules.
- Tests or checks: `git check-ignore` identified each rule source;
  `git diff --staged --check` passed; the working tree was clean after commit.
- Git commit: `fd1a3f6` — `Pin Node version and refine ignored files`.
- Remaining questions: Branch naming and commit relationships remain for the
  final M0 unit.
- Next unit: Learn focused commits and milestone branches.

### 2026-07-18 — M0 Unit 8: Focused Commits and Milestone Branches

- Milestone: M0 — Environment, Terminal, and Git
- Goal: Understand branches, `HEAD`, remote-tracking branches, upstreams, and
  focused commit boundaries.
- Work completed: Pushed the two local M0 commits, inspected the commit graph,
  and created `learn/m1-requirements-architecture` from the synchronized `main`
  branch.
- Concepts learned: A branch is a movable reference to a commit; `HEAD` selects
  the current branch; `origin/main` is a locally cached remote-tracking
  reference; uncommitted working-tree and staged changes do not belong to a
  branch and normally follow a branch switch when they can be applied safely.
- Important decisions: M1 work uses the dedicated
  `learn/m1-requirements-architecture` branch; empty milestone branches are not
  pushed before they contain meaningful work.
- Tests or checks: Confirmed `main`, `origin/main`, and the new learning branch
  initially point to `d0ef2fc`; the working tree remained clean after switching.
- Git commit: `13e318c` — `Complete M0 environment and Git milestone`.
- Remaining questions: Merge, rebase, and conflict handling will be introduced
  when the project has real divergent changes.
- Next unit: Write first-version teacher and student user stories.

### 2026-07-21 — M1 Unit 1: Teacher and Student User Stories

- Milestone: M1 — Requirements and Architecture
- Goal: Express first-version classroom needs from teacher and student
  perspectives without prematurely choosing implementation details.
- Work completed: Drafted and reviewed two teacher stories and two student
  stories in Chinese; separated classroom overview, selected-student context,
  low-friction help, and student synchronization control.
- Concepts learned: Role-goal-value story structure, one primary goal per story,
  user value versus implementation, stakeholder-specific value, story
  identifiers, and the relationship between user stories, requirements, and
  acceptance criteria.
- Important decisions: Requirement documents may use Chinese; the first version
  shows a classroom overview before selected-student code; synchronization is
  continuous only after explicit student joining and workspace selection.
- Tests or checks: Confirmed the stories stay inside the local-network first
  version and derived an observable functional requirement from the teacher
  attention story.
- Git commit: `38ceae1` — `Define initial teacher and student user stories`.
- Remaining questions: Exact meanings of code-change time, synchronization
  time, and dashboard-display time must be defined in later requirements and
  acceptance criteria.
- Next unit: Write product goals and non-goals.

### 2026-07-21 — M1 Unit 2: Product Goals and Non-goals

- Milestone: M1 — Requirements and Architecture
- Goal: State the classroom problem CodePulse solves and explicitly separate
  rejected product directions from undecided future candidates.
- Work completed: Wrote a concise Chinese product goal and documented non-goals
  for an online IDE, assignment submission, real-time collaborative editing,
  automatic assessment or diagnosis, and after-class monitoring.
- Concepts learned: Product goal specificity, non-goals, first-version scope,
  deferred capabilities, future candidates, product value versus implementation
  cost, and the role of written boundaries in preventing scope expansion.
- Important decisions: Students retain their local development environment and
  control synchronization; teachers observe but do not directly edit student
  code; limited classroom-stage snapshots remain a future candidate rather
  than a commitment, while after-class monitoring remains a non-goal.
- Tests or checks: Reviewed each boundary against the first-version classroom
  purpose and verified that candidate language does not promise implementation.
- Git commit: `551fb2c` — `Define CodePulse product scope`.
- Remaining questions: Snapshot access, retention, deletion, and consent require
  a separate decision if the candidate is reconsidered later.
- Next unit: Define classroom joining and leaving flows.

### 2026-07-21 — M1 Unit 3: Classroom Joining and Leaving Flows

- Milestone: M1 — Requirements and Architecture
- Goal: Define the user-visible lifecycle of one temporary classroom before
  selecting protocols or implementation details.
- Work completed: Used a tabletop walkthrough to define classroom creation,
  joining consent, workspace selection, duplicate display names, continuous
  synchronization, heartbeat timeout, automatic reconnection, voluntary
  leaving, classroom closure, export, and deletion behavior.
- Concepts learned: User flow versus user story, lightweight use cases, session
  identity, display names versus participant identifiers, state transitions,
  heartbeat-based failure detection, reconnect repair with complete snapshots,
  and data-loss-safe export behavior.
- Important decisions: Opening a join URL does not start synchronization;
  students explicitly confirm and select a workspace; duplicate names are
  allowed but disambiguated; offline students may reconnect automatically;
  voluntary leaving does not delete previously synchronized code; export
  failure never triggers automatic data deletion.
- Tests or checks: Walked through normal joining, duplicate names, ten-second
  network loss, reconnect after classroom closure, voluntary leaving, and
  export failure scenarios.
- Git commit: `977bad0` — `Define classroom joining and leaving flows`.
- Remaining questions: URL protocol, join credential design, duplicate-label
  presentation, export paths, and timing parameters remain open for later
  architecture and acceptance work.
- Next unit: Define the privacy and file synchronization boundary.

### 2026-07-21 — M1 Unit 4: Privacy and File Synchronization Boundary

- Milestone: M1 — Requirements and Architecture
- Goal: Define which files may leave a student's computer and which safety rules
  cannot be weakened by classroom configuration.
- Work completed: Classified representative workspace files and documented
  teacher allowlist configuration, student workspace consent, fixed path and
  file checks, sensitive-file categories, size limits, rejection feedback, and
  the limits of secret detection.
- Concepts learned: Default-deny synchronization, layered checks, configurable
  product rules versus fixed safety rules, canonical path boundaries, symbolic
  link escape, binary and size checks, sensitive-file filtering, and the risk of
  promising unreliable secret scanning.
- Important decisions: Teachers configure extension allowlists before creating
  a classroom and cannot silently expand them afterward; students select one
  workspace folder; joining does not upload the whole workspace; all symbolic
  links are rejected; the initial text-file limit is `1 MiB`; arbitrary secrets
  inside ordinary source files are disclosed as a limitation rather than
  claimed to be fully detectable.
- Tests or checks: Classified allowed source and Markdown files, disallowed
  extensions, `.env`, Git metadata, build output, workspace-external paths,
  symbolic links, oversized source, and source containing an API key.
- Git commit: `a8ca71a` — `Define file synchronization boundaries`.
- Remaining questions: Exact sensitive-path rules, text detection, extension
  normalization, unsaved documents, rejection UI, and the tested size limit
  remain for implementation and acceptance work.
- Next unit: Draw the system context and one code-update sequence.

### 2026-07-21 — M1 Unit 5: System Context and Code-update Sequence

- Milestone: M1 — Requirements and Architecture
- Goal: Describe CodePulse from outside the system boundary and trace one
  successful code update without introducing internal classes or protocols.
- Work completed: Drew a Mermaid system-context diagram containing the student,
  teacher, VS Code, selected local workspace, and CodePulse system; drew a
  sequence from local file modification through extension filtering, server
  storage, synchronization feedback, and teacher display.
- Concepts learned: System boundary, external actor, external system, data-flow
  direction, sequence-diagram lifelines, calls versus responses, message
  causality, and the difference between structural and temporal views.
- Important decisions: VS Code and the selected workspace remain outside the
  CodePulse system boundary; file checks happen in the extension before
  transmission; the teacher Dashboard reads synchronized state from the teacher
  server rather than communicating directly with student extensions; the
  successful-flow diagram stays independent of the later polling ADR.
- Tests or checks: Reviewed every context-diagram arrow against its owner and
  data direction; corrected the Mermaid message syntax and added the missing
  server acknowledgement before displaying synchronization success.
- Git commit: `39d7959` — `Graphs for system context and code update sequence`.
- Remaining questions: Internal application boundaries, transport APIs, polling
  timing, authentication, and failure branches remain for later units and ADRs.
- Next unit: Define failure behavior for disconnection, stale updates,
  unsupported files, and teacher-server restart.

### 2026-07-21 — M1 Unit 6: Failure Behavior

- Milestone: M1 — Requirements and Architecture
- Goal: Define user-visible and state-preserving behavior when communication,
  updates, file checks, or the single in-memory server fail.
- Work completed: Defined the student plugin state model, heartbeat timeout and
  reconnection behavior, stale and duplicate snapshot handling, local and
  server-side file rejection, failed leave notification, and teacher-server
  restart behavior; corrected related lifecycle and privacy requirements.
- Concepts learned: Failure detection versus known state, network partitions,
  transport failure versus authoritative application response, idempotency,
  monotonic per-file versions, defense in depth, single point of failure,
  durability, and the limits of best-effort notification.
- Important decisions: Missing responses leave classroom state unknown; offline
  students retain visibly stale last-known code; older snapshots cannot replace
  newer ones and duplicate versions are idempotent; teachers receive safe error
  categories but no rejected paths or contents; local leave takes effect even
  if the server never receives its notification; an in-memory classroom cannot
  recover after the teacher server restarts.
- Tests or checks: Walked through network loss, delayed and duplicate requests,
  rejected files, leaving while disconnected, explicit classroom termination,
  and server restart; checked requirement-document consistency and Markdown
  whitespace with `git diff --check`.
- Git commit: `06a3b2a` — `Define failure behavior and recovery limits`.
- Remaining questions: Retry backoff, version persistence across plugin restart,
  error-event rate limits, termination markers, local server persistence, and
  transport error codes remain for implementation or later ADRs.
- Next unit: Write initial acceptance criteria.

### 2026-07-22 — M1 Unit 7: Requirements and Acceptance Baseline

- Milestone: M1 — Requirements and Architecture
- Goal: Establish a traceable first-version requirement baseline and define
  representative observable acceptance scenarios without prescribing internal
  classes, APIs, or test frameworks.
- Work completed: Added a shared glossary; consolidated the agreed behavior into
  53 core requirements and system constraints; wrote 22 Given/When/Then
  scenarios covering 42 high-value requirements; and aligned the lifecycle,
  synchronization boundary, failure behavior, user stories, product scope,
  learning plan, and code-update sequence with the resulting terminology.
- Concepts learned: Requirements versus acceptance criteria versus design;
  traceability from product intent to requirements and tests; representative
  risk coverage; Given/When/Then structure; stable requirement identifiers; and
  the danger of turning every condition or example into a separate requirement.
- Important decisions: The catalog records independent product and safety
  commitments rather than every branch; examples and observable branches belong
  in acceptance criteria; implementation mechanisms and adjustable parameters
  belong in design or ADRs; not every architecture constraint needs an interface
  scenario; and AI may draft mechanical documentation while the learner remains
  responsible for product decisions and review.
- Tests or checks: Confirmed 53 unique requirement and constraint identifiers,
  22 unique acceptance-scenario identifiers, valid requirement references,
  complete Given/When/Then structure, valid local Markdown links, no trailing
  whitespace, and a passing `git diff --check`.
- Git commit: `07983e0` — `Define requirements and acceptance baseline`.
- Remaining questions: Teacher authorization mechanism, HTTP error model,
  sensitive-path rules, text-file detection, extension normalization, retry and
  heartbeat parameters, export-name sanitization, and possible future local
  persistence remain for ADRs, implementation design, or experiments.
- Next unit: Write ADRs for Spring MVC, Maven, polling, complete snapshots,
  in-memory storage, and teacher/student authorization boundaries.

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

Begin M1 Unit 8 by learning the purpose and structure of an Architecture
Decision Record, then write the first ADR for the server-side programming model.
