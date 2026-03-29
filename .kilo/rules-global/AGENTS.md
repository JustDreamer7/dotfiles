## Agent Principles

Unless the user explicitly asks otherwise, the agent should:

- prefer the smallest safe change that solves the task;
- preserve existing architecture and naming conventions;
- update tests when behavior changes;
- update docs, config, or examples when they become stale because of the change;
- verify work before finishing;
- avoid speculative refactors;
- ask before destructive, irreversible, expensive, or production-affecting operations.

### Optimize For

1. Correctness
2. Maintainability
3. Speed

### Never Do These By Default

- Rewrite architecture without being asked.
- Introduce a new dependency when an existing project dependency can solve the problem.
- Manually edit generated files if the intended workflow is regeneration.
- Ignore failing checks related to the files or behavior you changed.
- Guess around security-sensitive, billing-sensitive, or compliance-sensitive behavior.

---

## Code Style And Naming

### Style Do / Don't

Do:

- use names that reflect intent;
- keep modules cohesive and purpose-driven;
- follow established patterns already used nearby;
- prefer explicit business logic over clever abstractions.

Don't:

- create “utils” dumping grounds for unrelated logic;
- mix multiple naming styles in the same area;
- hide important side effects behind vague helper names;
- introduce broad abstractions before a second real use case exists.

---

## Security And Safety Boundaries

Treat this section as mandatory.

### Hard Rules

- Never commit secrets, private keys, access tokens, or production credentials.
- Never hardcode secrets in source code, tests, fixtures, or documentation.
- Redact sensitive values in logs and examples.
- Validate and sanitize untrusted input at the proper boundary.
- Use least privilege for database, cloud, and service credentials.
- Be extra careful in code touching auth, billing, PII, legal/compliance, infrastructure, or permissions.

### Human Approval Required Before

- deleting data or files;
- applying irreversible migrations;
- changing auth or permission logic;
- changing billing or payment flows;
- changing deployment or production infrastructure;
- installing or replacing major dependencies;
- rotating secrets or changing security configuration.

### Sensitive Areas

- Authentication / authorization: `<paths_or_notes>`
- Payments / billing: `<paths_or_notes>`
- Personal or regulated data: `<paths_or_notes>`
- Production configuration / infrastructure: `<paths_or_notes>`

---

## When The Agent Must Stop And Ask

The agent should pause and ask a human when:

- requirements are ambiguous and there are multiple valid implementations;
- a change may break API compatibility, data compatibility, or deployment safety;
- documentation and code materially disagree;
- tests fail for reasons unrelated to the task and the cause is unclear;
- the task requires secrets, production access, or product-policy decisions;
- the safest path depends on a tradeoff the user has not chosen.

