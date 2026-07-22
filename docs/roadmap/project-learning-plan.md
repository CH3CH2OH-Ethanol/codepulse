# CodePulse Project Learning Plan

## 1. Purpose

CodePulse is a project-based path for learning:

- TypeScript and the JavaScript ecosystem;
- HTTP and Java Web fundamentals;
- Spring Boot and Spring MVC;
- VS Code extension development;
- browser-based frontend development;
- requirements, architecture, testing, Git, documentation, security, packaging,
  and deployment.

The main success criterion is not how quickly CodePulse is completed. Success
means the learner can explain the system, implement its important parts, review
trade-offs, diagnose problems, and make later changes with confidence.

## 2. Learning Method

Each learning unit should normally take 30 to 60 minutes.

The default cycle is:

1. The Agent explains the problem and the minimum necessary concepts.
2. The learner discusses the design and confirms the acceptance criteria.
3. The learner writes the code or engineering document.
4. The Agent reviews the work using questions and hints first.
5. The learner revises and runs the relevant checks.
6. The learner creates one focused Git commit.
7. The Agent summarizes what was learned and why the solution was chosen.

The learner owns the main implementation. The Agent writes code only when
explicitly asked to handle a clearly scoped part.

## 3. Product Baseline

### 3.1 Product Goal

CodePulse is a classroom real-time code observation platform.

Students continue using their own VS Code, local runtime, and local debugger.
The extension synchronizes observable classroom code to a server running on the
teacher's computer. The teacher reads the code and decides whether a student
needs help.

The system is not:

- an online IDE;
- a remote code execution service;
- an assignment submission platform;
- an automatic judge;
- a cheating-prevention or surveillance system;
- an automatic diagnosis system that claims to know whether a student is stuck.

### 3.2 First Usable Version

- Supports no more than 30 students in one classroom.
- Runs over the same local network.
- Supports VS Code only.
- The student explicitly joins a classroom and chooses the classroom workspace.
- The student always sees that synchronization is active and can leave.
- The teacher configures an allowlist of file extensions for the classroom.
- The teacher sees a student list and one selected student's current
  synchronized file.
- The dashboard separately displays:
  - the last time the server accepted a code snapshot;
  - the last time the server received a text-edit activity event.
- The dashboard highlights students after a configurable inactivity threshold,
  initially five minutes.
- The highlight is only evidence for teacher attention; it is not an automatic
  conclusion.
- Classroom data is held in memory by default.
- The teacher may end the classroom and download a ZIP containing the final
  accepted version of every file that appeared during the session. In-memory
  classroom data remains until the teacher confirms the download was saved or
  explicitly abandons it.
- The system does not preserve a full edit history.
- HTTP is permitted only for controlled integration tests using synthetic,
  non-sensitive code. A classroom-ready release requires verified transport
  encryption and teacher-server identity validation.

### 3.3 Deferred Capabilities

The following are intentionally deferred until the core local-network version
has been learned, implemented, and tested:

- run success or failure detection;
- ordinary terminal command observation;
- WebSocket or Server-Sent Events;
- WebFlux and reactive programming;
- database persistence;
- React, Vue, or another frontend framework;
- Cloudflare Tunnel and remote classroom access;
- IntelliJ IDEA support;
- whole-project upload at classroom join;
- character-level differential synchronization;
- editing history and playback;
- automated stuck-state classification.
- direct directory export through browser file-system access.
- security hardening beyond the classroom-ready transport minimum, including
  controlled traffic inspection, abuse testing, fuzzing, and attack simulation.

## 4. Architecture Baseline

The system contains three applications:

1. **VS Code extension**
   - Written in TypeScript.
   - Observes the selected workspace.
   - Filters files before transmission.
   - Sends code snapshots, activity information, and heartbeats.

2. **Teacher server**
   - Written in Java with Spring Boot and Spring MVC.
   - Runs on the teacher's computer.
   - Authenticates students and the teacher.
   - Stores the current classroom state.
   - Rejects stale updates and exposes teacher APIs.
   - Generates the optional final ZIP snapshot.

3. **Teacher dashboard**
   - Written with HTML, CSS, Vite, and plain TypeScript.
   - Displays the student list and selected student's current code.
   - Polls the teacher server for updated state.
   - Contains presentation logic, not authoritative classroom rules.

The first implementation uses complete file snapshots after a short debounce
rather than character-level changes. This is simpler to reason about and allows
a later snapshot to repair an earlier lost or delayed update.

## 5. Milestones

## M0: Environment, Terminal, and Git

### Learning goals

- Understand the relationship between the terminal, shell, command, process,
  executable, PATH, runtime, package manager, and version manager.
- Understand why projects pin tool versions.
- Learn the basic Git working tree and commit model.

### Units

1. Inspect the current shell and PATH.
2. Compare the system Node.js installation with NVM-managed Node.js.
3. Select Node.js 24 LTS through the existing NVM installation.
4. Inspect Java installations and select Java 21.
5. Understand npm and its relationship to Node.js.
6. Understand why the project will use Maven Wrapper instead of requiring a
   global Maven installation.
7. Practice `git status`, `git diff`, `git add`, `git commit`, `git log`, and
   `.gitignore`.
8. Learn focused commits and milestone branches.

### Acceptance

- The learner can explain which executable each command resolves to.
- Node.js 24 and Java 21 can be selected predictably in a new terminal.
- The learner can inspect and commit one documentation-only change.

## M1: Requirements and Architecture

### Learning goals

- Convert an idea into explicit scope and testable behavior.
- Distinguish requirements, architecture, implementation, and operations.
- Learn the purpose of Architecture Decision Records.

### Units

1. Write teacher and student user stories.
2. Write product goals and non-goals.
3. Define classroom joining and leaving flows.
4. Define the privacy and file synchronization boundary.
5. Draw the system context and one code-update sequence.
6. Define failure behavior for disconnection, stale updates, unsupported files,
   and server restart.
7. Establish a traceable requirement catalog and write initial acceptance
   criteria.
8. Write ADRs for Spring MVC, Maven, polling, complete snapshots, in-memory
   storage, and teacher/student authorization boundaries.

### Acceptance

- Another person can explain the first version without relying on chat history.
- Important terms such as activity, inactivity, online, current synchronized
  file, and final snapshot have precise definitions.
- Every major technology choice records alternatives and consequences.

## M2: TypeScript Foundations Through Project Exercises

### Learning goals

- Learn JavaScript runtime concepts before relying on TypeScript types.
- Learn how TypeScript checks code and how the generated JavaScript runs.
- Learn Node.js, npm, modules, configuration, and unit testing.

### Units

1. Values, variables, conditions, loops, functions, objects, and arrays.
2. JavaScript modules and the Node.js runtime.
3. `package.json`, npm scripts, and local development dependencies.
4. Type annotations, inference, object types, interfaces, and type aliases.
5. Union types, optional values, narrowing, and exhaustive handling.
6. `tsconfig.json` and strict type checking.
7. Model a participant, activity state, and file snapshot.
8. Implement the five-minute inactivity rule as a pure function.
9. Implement extension allowlisting and sensitive-file rejection.
10. Write unit tests with Vitest.
11. Produce simulated classroom state as JSON from a command-line program.

### Acceptance

- The learner can explain the difference between JavaScript runtime behavior and
  TypeScript static checking.
- The simulated state program builds, runs, and has tests.
- Invalid and unknown states are represented explicitly instead of hidden with
  unsafe casts.

## M3: Java Web Foundations for Spring

### Learning goals

- Understand the web concepts that Spring MVC builds upon.
- Understand what a web server and Servlet container do.
- Learn Maven and Java testing before Spring automation is introduced.

### Units

1. HTTP requests, responses, methods, URLs, headers, bodies, and status codes.
2. Localhost, ports, TCP at the level required for application development.
3. Inspect requests with a browser and `curl`.
4. Maven coordinates, dependencies, lifecycle, tests, and packaging.
5. JUnit 5 fundamentals.
6. Implement a minimal HTTP endpoint with the JDK `HttpServer`.
7. Rebuild the endpoint with an embedded Servlet container.
8. Learn Servlet request, response, routing, and lifecycle concepts.
9. Convert Java objects to and from JSON with Jackson.
10. Separate transport handling, application logic, and in-memory storage.
11. Compare manual wiring with dependency injection.

### Explicit exclusions

- JSP and JSTL;
- manual JDBC;
- a database;
- application-server WAR deployment;
- traditional XML-based Spring configuration.

### Acceptance

- The learner can trace a request from the network port to Java application
  logic and back to the client.
- The learner can explain which repetitive responsibilities a framework could
  remove.
- The Java Web exercise has focused unit and HTTP-level tests.

## M4: Spring Boot and Spring MVC

### Learning goals

- Understand Spring beans, dependency injection, component scanning, application
  context, auto-configuration, and the Boot lifecycle.
- Build the first real CodePulse server incrementally.

### Units

1. Generate a minimal project with Spring Initializr and inspect every file.
2. Understand Maven Wrapper and the generated `pom.xml`.
3. Rebuild the M3 endpoint with Spring MVC.
4. Learn controllers, request mapping, parameter binding, DTOs, and JSON.
5. Learn constructor injection and bean ownership.
6. Introduce services and an in-memory repository only when responsibilities
   require them.
7. Add Bean Validation.
8. Design a consistent HTTP error format.
9. Test business rules with JUnit and HTTP behavior with MockMvc.
10. Add classroom creation and joining.
11. Add student state synchronization and teacher read APIs.
12. Add teacher and student token boundaries with Spring Security.
13. Add classroom closure, discard, and final ZIP export.
14. Compare Maven concepts with their Gradle equivalents without maintaining a
    second build.

### Acceptance

- The learner can explain which behavior comes from Java, Spring Framework,
  Spring Boot, Spring MVC, Spring Security, Maven, and application code.
- Core business rules can be tested without starting the full server.
- Authorization prevents a student from reading teacher APIs or another
  student's code.

## M5: VS Code Extension

### Learning goals

- Apply TypeScript in an event-driven host application.
- Learn extension manifests, activation, commands, resources, and integration
  testing.

### Units

1. Create and inspect the minimal extension structure.
2. Understand extension activation and deactivation.
3. Add an explicit “join classroom” command.
4. Let the student choose the classroom workspace.
5. Store the temporary token with `SecretStorage`.
6. Observe the active editor and text document changes without treating cursor,
   selection, or file-focus changes as editing activity.
7. Send one eligible initial active-file snapshot after explicit consent.
8. Apply extension allowlists, sensitive-file filters, relative paths, text-only
   checks, and size limits.
9. Debounce edits and limit transmission frequency.
10. Add persistent monotonically increasing per-file snapshot versions.
11. Keep one latest pending snapshot per changed file during disconnection.
12. Send HTTP requests and handle timeout, jittered backoff, and reconnection.
13. Require renewed confirmation after an extension-process restart.
14. Display persistent synchronization status and allow the student to leave.
15. Test pure logic separately from VS Code API integration.
16. Package the extension as a VSIX.

### Acceptance

- Files outside the selected workspace cannot be transmitted.
- Rejected files provide a visible reason instead of failing silently.
- A reconnect sends the latest pending snapshot for every changed eligible file.
- Disposables and timers are cleaned up when synchronization stops.

## M6: Teacher Dashboard with Plain TypeScript

### Learning goals

- Learn browser execution, the DOM, events, fetch, asynchronous state, rendering,
  and frontend testing before adopting a framework.

### Units

1. Create a Vite plain TypeScript application.
2. Understand HTML structure, CSS layout, browser modules, and the development
   server.
3. Fetch classroom overview data.
4. Model loading, success, empty, stale, and error states.
5. Render a student list.
6. Select one student and request the current synchronized file.
7. Render code as text, never executable HTML.
8. Copy the currently displayed single-file code snapshot with clear success and
   failure feedback.
9. Display code synchronization and editing-activity times independently.
10. Calculate and display the five-minute attention highlight.
11. Poll once per second and avoid overlapping requests.
12. Separate network access, application state, and DOM rendering.
13. Test sorting, time formatting, and status conversion with Vitest.
14. Build static assets for Spring Boot to serve.

### Acceptance

- The teacher can identify offline and inactive students and inspect one current
  synchronized file.
- Student-controlled text cannot become executable HTML.
- Temporary network errors do not destroy the last known classroom view.

## M7: Integration, Reliability, Testing, and Packaging

### Learning goals

- Learn to validate behavior across process and network boundaries.
- Learn failure modeling, load testing, packaging, and classroom operations.

### Units

1. Connect the extension, server, and dashboard.
2. Define request timing, heartbeat timing, and offline thresholds.
3. Reject out-of-order client sequences.
4. Handle file switching, renaming, deletion, unsupported files, and oversized
   files.
5. Verify classroom discard and export behavior.
6. Build a simulator for up to 30 students.
7. Measure update latency and server resource use.
8. Package the dashboard inside the executable Spring Boot JAR.
9. Package and install the VSIX.
10. Write a classroom runbook and troubleshooting guide.
11. Keep HTTP integration builds marked as test-only until a later transport
    security ADR defines and verifies the classroom-ready mechanism.

### Initial timing targets

- Send a code snapshot about 500 milliseconds after input settles.
- Send no more than one code snapshot per student per second.
- Send a heartbeat every 10 seconds.
- Consider a student offline after 30 seconds without a heartbeat.
- Display a normal code update within two seconds under the target classroom
  load.

The targets must be tested and may be revised through an ADR.

### Acceptance

- A 30-student simulation meets the measured latency target.
- Delayed requests cannot overwrite newer code.
- Reconnection restores the current view.
- Export contains final file versions but no edit history.
- Discard leaves no classroom source code on disk.
- The system can be started from documented classroom instructions.

## M8: Remote Classroom Support

### Learning goals

- Understand the network and security implications of exposing a local service.

### Units

1. Learn NAT, public addresses, DNS, TLS, and reverse tunnels.
2. Expose the already working local service with a temporary Cloudflare Tunnel.
3. Compare Quick Tunnel and Named Tunnel behavior.
4. Revisit authentication, rate limiting, request size, logging, and secret
   handling for public access.
5. Test disconnects and temporary tunnel replacement.
6. Document remote-classroom setup and limitations.

### Acceptance

- The local-network application protocol does not need to be redesigned.
- Public access is authenticated and does not expose source code through logs.
- The limitations of the selected tunnel mode are documented.

## 6. Testing Strategy

Testing is introduced with the behavior it protects:

- TypeScript pure logic: Vitest.
- Java domain and application logic: JUnit 5.
- Spring MVC HTTP behavior: MockMvc.
- VS Code API behavior: VS Code Extension Test CLI.
- Cross-application behavior: local integration tests and a simulated classroom.
- Security and privacy: explicit negative tests for unauthorized access,
  sensitive files, absolute paths, traversal attempts, and oversized input.

Tests should begin narrow and fast, then expand toward integration. A learning
unit is not complete only because the happy path works manually.

## 7. Git and Documentation Practice

- Use one focused commit per accepted learning unit.
- Prefer a milestone branch named `learn/mN-short-topic`.
- Inspect `git diff` before staging.
- Do not commit generated build output, downloaded dependencies, secrets, or
  classroom source snapshots.
- Record important architecture decisions in `docs/adr/`.
- Keep `docs/roadmap/progress.md` current after each accepted unit.
- Chat is temporary context; repository documents are the durable source of
  truth.

## 8. Toolchain Baseline

Versions are pinned when the relevant milestone begins and remain fixed during
that milestone unless a security or compatibility issue requires a documented
change.

- Java: 21 LTS.
- Node.js: 24 LTS, managed through the existing NVM installation.
- npm: the version bundled with the selected Node.js release.
- Maven: Maven Wrapper; no global Maven installation is required.
- Spring Boot: 4.1.x when the Spring milestone begins.
- Spring web stack: Spring MVC, not WebFlux.
- TypeScript: 6.x with strict type checking when the TypeScript milestone begins.
- Dashboard build tool: Vite 8.1.x.
- TypeScript unit tests: Vitest.
- Editor: VS Code; the minimum extension engine version is fixed when M5 begins.

The project uses Maven. Gradle is explained through comparison but is not added
as a second build system.

## 9. Definition of Learning Completion

A unit is complete when:

- the learner produced the main work;
- the relevant build and tests pass;
- the learner can explain the concept and chosen trade-off;
- the learner can identify where a small requirement change would be made;
- the change is reviewed;
- the Git commit contains only the unit's work;
- the next unit and any remaining questions are recorded.
