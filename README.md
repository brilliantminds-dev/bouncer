# Bouncer

An annotation-driven, in-application web security library for Spring Boot REST APIs, developed test-first by BrilliantMinds Development.

**Status:** design and TDD backlog; not implemented or production-ready.

```java
@Bouncer(
    enabled = true,
    xss = true,
    sqli = true,
    ipWhitelists = {"internal-services", "trusted-partners"},
    roles = {"ADMIN", "DEVELOPER"}
)
```

This is a proposed API, not working code. IP lists are externalized in YAML; RBAC is inferred from nonempty roles. Disabling Bouncer preserves normal Spring Security.

## Development

- [Architecture, UML, flowcharts and pseudocode](docs/architecture.md)
- [TDD playbook and board setup](docs/tdd-playbook.md)
- [All development stories](https://github.com/brilliantminds-dev/bouncer/issues)
- [Start with B001 — Accept valid IPv4 CIDR](https://github.com/brilliantminds-dev/bouncer/issues/1)

Complete one test and its RED → GREEN → REFACTOR → VERIFY cycle at a time. Start with a minimal Maven/JUnit 5 test harness. Production code is intentionally left to the developer.

Bouncer is a defense-in-depth tool, not a replacement for secure coding, Spring Security, or an edge WAF.
