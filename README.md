# multica-skills

Skills for running MSP (Managed Service Provider) operations with [Multica](https://multica.ai) agents.

## Skills

| Skill | Description |
|---|---|
| [msp-work-record](skills/msp-work-record/SKILL.md) | Turns raw MSP email threads into structured, traceable work records |

## msp-work-record

Operators paste raw customer email threads into an agent chat, and the agent organizes them into a consistent record with six labels: **Summary, Request, Trigger, Findings, Actions, Follow-ups**.

Design principles:

- **Organize, don't summarize.** No information loss; every fact goes in exactly one place.
- **Preserve identifiers.** IPs, paths, accounts, and error messages stay verbatim. Credentials are masked.
- **Inspired by the Google SRE postmortem template.** Concepts like root cause vs. assumption, temporary mitigation, action item owners, and timeline are applied within the existing label structure.

> Customer-specific context (organization names and identification hints) lives in a separate private `org-context` skill and is not included in this repository. All examples use fictional values.

## Structure

```
skills/
└── msp-work-record/
    └── SKILL.md
```

## Versioning

Each skill follows [Semantic Versioning](https://semver.org/). The current version is noted at the top of each `SKILL.md`.
