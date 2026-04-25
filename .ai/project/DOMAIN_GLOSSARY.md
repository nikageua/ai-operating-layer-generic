# Domain Glossary

Use this file for business and product terms that are easy to misuse.

Add a term only when:
- it was misused,
- it was aliased incorrectly,
- or it had to be rediscovered more than once.

Suggested shape:

```md
- **Tenant** — The top-level customer isolation boundary. Canonical: `repo:identity-api/...`
- **Workspace** — A user-visible working area inside a tenant. Canonical: `repo:web-app/...`
```

Keep entries short.
If a term does not change implementation or review behavior, it probably does not belong here.
