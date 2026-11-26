# TDD development playbook

## Start here

Create a minimal Maven/JUnit 5 test harness before B001 (no production implementation). Choose a supported Java/Spring Boot baseline before introducing the starter. Run tests locally before CI.

[First story — B001](../issues/1) (absolute link: https://github.com/brilliantminds-dev/bouncer/issues/1)

1. RED: write one JUnit test, create only declarations needed to compile, and confirm it fails for the intended reason.
2. GREEN: implement the minimum behavior to pass.
3. REFACTOR: improve names, responsibilities and duplication without adding behavior.
4. VERIFY: rerun targeted test, then `mvn test` (or `mvn verify` once integration tests exist).
5. REVIEW: inspect changes, commit, close issue only after all acceptance criteria pass. If unfinished, resume same story next time.

35-minute session: 5 minutes review, 5 test, 10 implement, 5 refactor, 5 verify, 5 commit. One active story at a time.

## First JUnit example

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CidrValidatorTest {
    @Test
    void shouldAcceptValidIpv4Cidr() {
        CidrValidator validator = new CidrValidator();
        CidrRange result = validator.validate("192.168.1.0/24");
        assertNotNull(result);
        assertEquals(24, result.getPrefixLength());
        assertArrayEquals(new byte[]{(byte)192, (byte)168, 1, 0},
                          result.getNetworkAddress());
    }
}
```

Write implementation yourself. Next test: B002, invalid prefix 33. Do not start it until B001 is green, refactored and verified.

## Project board setup

The issue titles have stable order IDs B001–B071 and phase identifiers. Create an organization GitHub Project named Bouncer — TDD Development, use Board layout, and add all open issues from this repository. Set Status options to Backlog, Ready, RED, GREEN, Refactor, Verify, In Review, Done. Initial status B001 Ready; all others Backlog. Group by Status; sort by Title ascending where available. Close stories only when done. Actual project creation, milestones and status field updates require the GitHub UI or an authorized CLI, not the available ChatGPT connector.

| Phase | Stories |
|---|---|
| M01 Networking | B001–B028 |
| M02 IP Whitelisting | B029–B035 |
| M03 Request Resolution | B036–B042 |
| M04 Threat Detection | B043–B048 |
| M05 Security Engine | B049–B053 |
| M06 Configuration | B054–B058 |
| M07 RBAC | B059–B061 |
| M08 Spring Integration | B062–B066 |
| M09 Release | B067–B071 |

Some stories contain multiple related test cases; repeat the entire TDD cycle for each case before closing the story. Shared models, interfaces and minimal build scaffolding can emerge earlier as tests require them.

## References

- [JUnit 5 user guide](https://junit.org/junit5/docs/current/user-guide/)
- [Spring MVC interceptors](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-config/interceptors.html)
- [Spring Security method authorization](https://docs.spring.io/spring-security/reference/servlet/authorization/method-security.html)
- [OWASP XSS prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [OWASP SQL injection prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
