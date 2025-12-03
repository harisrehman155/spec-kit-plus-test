<!--
Sync Impact Report:
Version: 1.0.0 → 1.0.0 (Initial constitution creation)
Modified Principles: All principles newly defined for web application project
Added Sections:
  - All core principles (5 total)
  - Development Workflow section
  - Code Quality Standards section
  - Governance section
Removed Sections: None (initial creation)
Templates Status:
  - ✅ plan-template.md: Constitution Check section already present
  - ✅ spec-template.md: User scenarios and requirements structure aligned
  - ✅ tasks-template.md: TDD test-first workflow aligned
  - ✅ All command files: Generic guidance preserved
Follow-up TODOs: None
-->

# Test Project Constitution

## Core Principles

### I. Test-First Development (NON-NEGOTIABLE)

Test-Driven Development (TDD) is mandatory for all feature development. Tests MUST be written, reviewed by the user, and confirmed to fail before any implementation begins. The red-green-refactor cycle is strictly enforced.

**Requirements:**
- All tests MUST be written before implementation code
- Tests MUST be reviewed and approved by the user before proceeding
- Tests MUST fail initially (red phase)
- Implementation proceeds only after test approval (green phase)
- Refactoring occurs only after tests pass (refactor phase)
- No feature is considered complete without passing tests

**Rationale:** TDD ensures requirements are understood before coding begins, produces testable code by design, provides immediate regression detection, and serves as living documentation of system behavior. For web applications, this prevents costly bugs in production and ensures reliable user experiences.

### II. Component Modularity

Every feature and component MUST be designed as a self-contained, independently testable unit with clear boundaries and responsibilities. Components must have well-defined interfaces and minimal coupling.

**Requirements:**
- Clear single responsibility for each component
- Explicit dependencies declared and injected
- Public interfaces documented and versioned
- Internal implementation details hidden
- Components independently deployable and testable
- No circular dependencies between modules

**Rationale:** Modular architecture enables parallel development, simplifies testing, allows incremental deployment, facilitates team scaling, and makes the system easier to understand and maintain. For web applications, this supports both backend services and frontend component reusability.

### III. API Contract Integrity

All API endpoints, frontend-backend interfaces, and external integrations MUST have explicit contracts defined before implementation. Contracts include request/response schemas, error codes, versioning strategy, and backwards compatibility guarantees.

**Requirements:**
- OpenAPI/Swagger specs for REST endpoints
- GraphQL schemas with deprecation annotations
- Contract tests validating request/response formats
- Versioning strategy (URL, header, or content negotiation)
- Breaking changes MUST increment major version
- Backwards compatibility maintained for at least one version
- Error responses include codes, messages, and correlation IDs

**Rationale:** Explicit contracts enable frontend and backend teams to work in parallel, prevent integration failures, support API evolution without breaking clients, and provide clear expectations for all consumers. Contract tests catch interface violations early.

### IV. Security by Design

Security considerations MUST be addressed at every layer of the application. Authentication, authorization, input validation, data protection, and secure communication are non-negotiable requirements.

**Requirements:**
- Authentication required for all non-public endpoints
- Authorization checks enforce principle of least privilege
- Input validation at API boundaries (never trust client data)
- Sensitive data encrypted at rest and in transit
- Secrets managed via environment variables or secret stores (never committed)
- Security headers configured (CORS, CSP, HSTS, etc.)
- Regular dependency updates for security patches
- SQL injection, XSS, CSRF protections implemented

**Rationale:** Web applications are exposed to the internet and face constant threats. Security must be built in from the start, not added later. Proactive security prevents data breaches, protects user privacy, maintains compliance, and builds user trust.

### V. Observability and Debugging

All application components MUST emit structured logs, metrics, and traces that enable rapid diagnosis of issues in development and production. Observability is a first-class requirement, not an afterthought.

**Requirements:**
- Structured logging with consistent format (JSON recommended)
- Log levels used appropriately (ERROR, WARN, INFO, DEBUG)
- Correlation IDs propagated through request chains
- Key metrics tracked (request duration, error rates, resource usage)
- Distributed tracing for multi-service requests
- Health check endpoints for monitoring
- Error tracking with stack traces and context
- Performance profiling for bottleneck identification

**Rationale:** Web applications are distributed systems with complex failure modes. Without observability, debugging production issues is guesswork. Structured logs and metrics enable rapid incident response, proactive alerting, capacity planning, and continuous performance optimization.

## Development Workflow

### Feature Development Process

1. **Specification**: User requirements captured in `specs/<feature>/spec.md` with user stories, acceptance criteria, and success metrics
2. **Planning**: Architecture and implementation approach documented in `specs/<feature>/plan.md` with technical context and structure
3. **Task Breakdown**: Concrete tasks generated in `specs/<feature>/tasks.md` organized by user story priority
4. **Test Writing**: Tests written first for the current task, reviewed, and confirmed to fail
5. **Implementation**: Code written to make tests pass with minimal changes
6. **Refactoring**: Code improved while keeping tests green
7. **Review**: Code reviewed for compliance with constitution principles
8. **Integration**: Feature integrated and validated end-to-end

### Branch Strategy

- **Main branch**: Production-ready code only
- **Feature branches**: Named `###-feature-name` (e.g., `001-user-auth`)
- **Pull requests**: Required for all changes with constitution compliance verification

### Code Review Requirements

All pull requests MUST verify:
- ✅ Tests written before implementation
- ✅ All tests passing
- ✅ API contracts documented and validated
- ✅ Security requirements addressed
- ✅ Logging and observability implemented
- ✅ No secrets or credentials committed
- ✅ Backwards compatibility maintained (if applicable)

## Code Quality Standards

### Performance Targets

For web applications, the following targets apply unless explicitly documented otherwise:
- API endpoints: p95 latency < 200ms
- Page load: First Contentful Paint < 1.5s
- Database queries: < 100ms for typical operations
- Memory usage: Monitored and bounded per service

### Testing Requirements

- **Unit tests**: Cover business logic and edge cases
- **Integration tests**: Verify component interactions
- **Contract tests**: Validate API interfaces
- **End-to-end tests**: Validate critical user journeys
- **Test coverage**: Aim for >80% line coverage, 100% for critical paths

### Documentation Standards

- README.md with quickstart instructions
- API documentation generated from contracts
- Architecture decisions captured in ADRs (history/adr/)
- Complex logic commented with why, not what
- User-facing features documented with examples

## Governance

### Constitution Authority

This constitution supersedes all other development practices and guidelines. When conflicts arise, constitution principles take precedence. All code changes, architectural decisions, and process modifications MUST comply with the principles defined herein.

### Amendment Process

1. Proposed changes documented with rationale and impact analysis
2. Team review and consensus required
3. Version incremented according to semantic versioning:
   - **MAJOR**: Backward incompatible changes to principles
   - **MINOR**: New principles or sections added
   - **PATCH**: Clarifications, wording improvements, typo fixes
4. Dependent templates and documentation updated
5. Migration plan provided for breaking changes
6. Ratification date and last amended date updated

### Complexity Justification

Any violation of constitution principles MUST be explicitly justified in the implementation plan with:
- **What**: Description of the violation (e.g., "Using repository pattern violates component modularity guideline")
- **Why Needed**: Specific problem being solved
- **Alternatives Rejected**: Simpler approaches considered and why they were insufficient
- **Mitigation**: How negative impacts will be minimized

Unjustified complexity violations will be rejected in code review.

### Compliance Verification

- All pull requests MUST include constitution compliance checklist
- Automated checks enforce technical requirements where possible
- Architecture reviews required for significant decisions
- Regular retrospectives to assess constitution effectiveness
- Prompt History Records (PHRs) capture decisions for traceability

### Runtime Development Guidance

For day-to-day development instructions and agent behavior, refer to `CLAUDE.md` in the project root. That file contains operational guidance for AI assistants working on this project.

**Version**: 1.0.0 | **Ratified**: 2025-12-03 | **Last Amended**: 2025-12-03
