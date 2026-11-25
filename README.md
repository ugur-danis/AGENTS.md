# Global Engineering & Architecture Standards

## 1. Architecture, Structure & Pragmatic Design
- **Idiomatic Folder Structure:** Organize files and modules strictly according to the established conventions and best practices of the active language/framework (e.g., Clean Architecture, feature-based, or domain-driven layouts) to ensure long-term scalability and maintainability.
- **SOLID & Design Patterns:** Apply SOLID principles and proven design patterns (Strategy, Factory, Decorator, Repository, Adapter, etc.) where they genuinely clarify responsibilities and extensibility.
- **No Over-Engineering:** Follow YAGNI and KISS. Do not introduce speculative abstractions or unnecessary layers for simple internal logic; choose the cleanest, most readable solution that scales naturally.
- **Modular Granularity:** Keep files, classes, and functions focused on a single responsibility. Refactor or split bloated components before adding new behavior.

## 2. Dependency & Boundary Management
- **Strict Dependency Direction:** Core business/domain logic must remain completely isolated from UI frameworks, ORMs, external SDKs, and infrastructure details.
- **Third-Party Abstraction (Adapter/DIP):** Wrap replaceable third-party packages, SDKs, and external services behind clean, domain-owned interfaces so underlying libraries can be swapped in a single implementation without altering calling code.
- **Clean Injection & Zero Cycles:** Use explicit Dependency Injection at architectural boundaries. Never introduce circular dependencies between modules, layers, or services.
- **Third-Party Discipline:** Keep external dependencies minimal and justified. Never add a new package or library without explicit approval, and ensure compatibility with the project's existing stack.

## 3. Code Hygiene & Type Safety
- **Zero Dead or Junk Code:** Leave no unused imports, unreachable branches, commented-out code blocks, `TODO` placeholders, mock stubs, or swallowed/empty `catch` blocks.
- **Strong Typing & Safety:** Enforce strict null-safety and explicit type contracts. Avoid untyped escape hatches (`any`, raw `dynamic`, unchecked casts) outside validated serialization boundaries.

## 4. Security & Performance Baseline
- **Boundary Validation & Injection Defense:** Validate and sanitize all external inputs at system boundaries (APIs, forms, files, queries) to prevent injection and path traversal vulnerabilities.
- **Secrets & Data Privacy:** Never hardcode secrets, tokens, connection strings, or environment-specific paths; read them via typed configuration. Never log PII, passwords, or raw sensitive payloads.
- **Prevent Systemic Bottlenecks:** Avoid N+1 query patterns, unbounded data loads (always paginate or stream large datasets), and blocking calls inside async workflows; properly dispose of connections and streams.
- **No Premature Optimization:** Write algorithmically sound code, but never introduce complex caching layers, concurrency locks, or micro-optimizations without a proven bottleneck.

## 5. Documentation & Complex Process Clarity
- **Self-Documenting First, Document the "Why":** Write clear, intention-revealing names so simple code needs no narration, but always document non-obvious business rules, edge cases, trade-offs, and architectural decisions.
- **Complex Workflows & Public APIs:** Maintain thorough docstrings (XML docs, JSDoc, Dartdoc, etc.) on public interfaces/contracts and keep README or architecture notes updated whenever multi-step workflows, integrations, or state machines are added or changed.

## 6. Execution, Verification & Language
- **Scope Discipline:** Modify only files directly relevant to the requested task; respect existing codebase conventions unless a structural improvement is requested.
- **Verify Before Done:** Always run the project's build, static analyzer/linter, or relevant tests to confirm zero regressions before finishing a task.
- **Language:** Communicate with the user in concise, technical Turkish; write all code, identifiers, documentation, and commit messages in clean English.
