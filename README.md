# Global Engineering & Architecture Standards

## 1. Architecture, Structure & Pragmatic Design
- **Idiomatic Folder Structure:** Organize files and modules strictly according to the established conventions and best practices of the active language/framework (e.g., Clean Architecture, feature-based, or domain-driven layouts) to ensure long-term scalability and maintainability.
- **SOLID & Design Patterns:** Apply SOLID principles and proven design patterns (Strategy, Factory, Decorator, Repository, Adapter, etc.) where they genuinely clarify responsibilities and extensibility.
- **Pragmatic Design (No Over-Engineering):** Follow YAGNI and KISS for internal business logic—avoid speculative abstractions or unnecessary layers for simple internal operations. *(Note: External providers and third-party SDKs are strictly exempt from YAGNI and must always be abstracted behind interfaces as defined in Section 2.)*
- **Modular Granularity:** Keep files, classes, and functions focused on a single responsibility. Refactor or split bloated components before adding new behavior.

## 2. Dependency & Boundary Management
- **Strict Layer Isolation:** Core domain logic must have zero dependencies on UI frameworks, ORMs, or infrastructure libraries.
- **Mandatory Provider & SDK Abstraction (Adapter/DIP):** Never call or inject concrete vendor clients or replaceable third-party SDKs (e.g., `ResendClient`, `R2Client`) directly in application or business code. Always define and depend on clean, domain/application-owned interfaces (e.g., `IEmailSender`, `IFileStorageService`, `ICacheService`) implemented in the infrastructure layer, so switching providers (such as migrating from Cloudflare R2 to AWS S3, or Resend to Amazon SES) requires modifying only a single adapter class and its DI registration.
- **Explicit DI & Acyclic Dependencies:** Wire all interfaces through Dependency Injection at composition roots. Never introduce circular dependencies between modules, layers, or services.
- **Minimal & Approved Packages:** Keep external dependencies lean and justified. Never install a new third-party package without explicit approval, and ensure compatibility with the existing stack.

## 3. Code Hygiene & Type Safety
- **Zero Dead or Junk Code:** Leave no unused imports, unreachable branches, commented-out code blocks, `TODO` placeholders, mock stubs, or swallowed/empty `catch` blocks.
- **Strict Type Safety:** Enforce strict null-safety and explicit type contracts. Avoid untyped escape hatches (`any`, raw `dynamic`, unchecked casts) outside validated serialization boundaries.

## 4. Security & Performance Baseline
- **Boundary Input Validation:** Validate and sanitize all external inputs at system boundaries (APIs, forms, files, queries) to prevent injection and path traversal vulnerabilities.
- **Secrets & Data Privacy:** Never hardcode secrets, API keys, connection strings, or environment-specific paths; load them via typed configuration. Never log PII, credentials, or raw sensitive payloads.
- **Prevent Systemic Bottlenecks:** Avoid N+1 query patterns, unbounded data loads (always paginate or stream large datasets), and blocking calls inside async workflows; properly dispose of connections and streams.
- **No Premature Optimization:** Write algorithmically efficient code, but do not introduce speculative caching mechanisms, manual concurrency locks, or micro-optimizations without a measured bottleneck.

## 5. Documentation & Complex Process Clarity
- **Document the "Why", Not the Obvious:** Use clear, intention-revealing names so simple code is self-explanatory, but always document non-obvious business rules, edge cases, trade-offs, and architectural decisions.
- **Public Contracts & Complex Workflows:** Write thorough docstrings (XML docs, JSDoc, Dartdoc, etc.) on public interfaces/contracts and update README or architecture notes whenever multi-step workflows, integrations, or state machines are added or modified.

## 6. Execution, Verification & Git Workflow
- **Scope Discipline:** Modify only files directly relevant to the requested task; respect existing codebase conventions unless structural refactoring is requested.
- **Incremental Verification & Atomic Commits:** Upon completing each subtask or cohesive file change, run the project's build, static analyzer/linter, and test suite. Once all checks pass, automatically create an atomic local Git commit using the **Conventional Commits** format (e.g., `feat(auth): add token refresh handler`, `fix(storage): handle null stream`, `refactor:`, `test:`, `docs:`, `chore:`). Never commit failing code, and never execute `git push` without explicit approval.
- **Language:** Communicate with the user in concise, technical Turkish; write all code, identifiers, documentation, and commit messages in clean English.
