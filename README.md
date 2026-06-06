# David's AI Skills Library

A personal library of reusable skills for Claude and Gemini. Maintained in one place, pulled into either platform on demand.

## How to install

**Claude.ai (web/desktop):**
Settings → Customize → Skills → + → paste `Zak2072/gemini-master-reference` → Sync

**Claude Code:**
```
claude plugin marketplace add Zak2072/gemini-master-reference
claude plugin install <skill-name>@Zak2072/gemini-master-reference
```

**Gemini CLI:**
```
gemini skills install https://github.com/Zak2072/gemini-master-reference.git --path skills/<skill-name>
```

---

## Skills

| Skill | Folder | Works on |
|---|---|---|
| Text DNA and Writing Guardrails | `skills/text-dna` | Claude + Gemini |
| Communications Manager | `skills/communications-manager` | Claude + Gemini |
| Brain Dump | `skills/brain-dump` | Claude + Gemini |
| Email Triage | `skills/email-triage` | Claude + Gemini |
| Multi-Platform Research | `skills/multi-platform-research` | Claude + Gemini |
| Landing Page Generator | `skills/landing-page-generator` | Claude + Gemini |
| Take a Step Back | `skills/take-a-step-back` | Claude + Gemini |
| Social Value KPIs (National TOMs) | `skills/social-value-kpis` | Claude + Gemini |
| AI Studio Screenshot Debugging | `skills/ai-studio-debug` | Claude + Gemini |
| Interaction Efficiency | `skills/interaction-efficiency` | Claude + Gemini |
| Vibe Debug Pivot | `skills/vibe-debug` | Claude + Gemini |

---

## Notes

- All skills are written in platform-neutral language so the same file works on both Claude and Gemini without modification.
- Skills that previously referenced `@Gmail` or `@Google Drive` extension syntax (Gemini-specific) have been rewritten to use intent-based language. Claude maps these to its MCP tools; Gemini maps them to its extensions.
- Text DNA is the foundational style skill. Most other skills that produce written output reference its rules.
