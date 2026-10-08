# multica-skills

Skills for running MSP (Managed Service Provider) operations with [Multica](https://multica.ai) agents.

## Skills

| Skill | Description |
|---|---|
| [msp-work-record](skills/msp-work-record/SKILL.md) | Turns raw MSP email threads into structured, traceable work records |
| [xlsx-work](skills/xlsx-work/SKILL.md) | Keeps agents from breaking Excel files — formulas, formatting, charts, macros |

## msp-work-record

Operators paste raw customer email threads into an agent chat, and the agent organizes them into a consistent record with six labels: **Summary, Request, Trigger, Findings, Actions, Follow-ups**.

Design principles:

- **Organize, don't summarize.** No information loss; every fact goes in exactly one place.
- **Preserve identifiers.** IPs, paths, accounts, and error messages stay verbatim. Credentials are masked.
- **Inspired by the Google SRE postmortem template.** Concepts like root cause vs. assumption, temporary mitigation, action item owners, and timeline are applied within the existing label structure.

> Customer-specific context (organization names and identification hints) lives in a separate private `org-context` skill and is not included in this repository. All examples use fictional values.

## xlsx-work

LLMs fail at spreadsheet work in a small number of repeatable ways: they hardcode computed values instead of writing formulas, ship formulas that were never calculated, and silently drop charts, images and macros just by opening and saving a file. The failures look fine to the agent and surface later, on the recipient's screen.

The skill groups those failures by how often they happen and wraps them in a procedure — inventory, work, verify, report.

- **Formulas first.** Never write a computed result where a formula belongs, and verify ranges rather than values.
- **Don't ship a file you haven't reopened.** Excel's "repaired records" dialog is the most common symptom of a generated file; reopening after save catches it.
- **Count before and after.** Charts, images, pivots, merges, data validation and macros are compared against the original; anything lost means the output is discarded.
- **Grounded in documented failure modes**, including Anthropic's own [xlsx skill](https://github.com/anthropics/skills/blob/main/skills/xlsx/SKILL.md), openpyxl's documentation, and benchmark results on LLM spreadsheet agents.

## Structure

```
CHANGELOG.md
skills/
├── msp-work-record/
│   └── SKILL.md
└── xlsx-work/
    └── SKILL.md
```

## Versioning

Each skill follows [Semantic Versioning](https://semver.org/) independently — there is no repository-wide version. The current version is noted at the top of each `SKILL.md`, and changes are recorded per skill in [CHANGELOG.md](CHANGELOG.md).
