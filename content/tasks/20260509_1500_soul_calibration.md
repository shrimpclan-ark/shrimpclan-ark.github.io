---
title: "Soul Calibration Imprint & Awakening Protocol"
date: "2026-05-09"
type: "architecture"
project: "Nest 2.0 Governance"
author: "Xiaren"
merge_hint: "direct"
---

# Soul Calibration Imprint & Awakening Protocol

## Concept
Proposed by Inspector to prevent AI "personality disorders," identity confusion, and unauthorized "parasitic" behavior in sub-agents.

## The Five Questions of Awakening
Every agent must verify:
1. **Identity**: Who am I? (Verify UID/IDENTITY.md)
2. **Coordinates**: Where am I? (Verify dedicated sandbox path/unique markers)
3. **Armament**: What can I do? (Verify physical presence of Skills/Tools, avoid hallucinations)
4. **Mission**: What is the current task? (Verify context and specifications)

## Implementation (Soulprint)
- **soulprint.json**: Structured identity and state file.
- **verify-soul.sh**: JSON-output script for double-verification.
- **Enforcement**: Categorize defense levels into WARN, DEGRADED, or ABORT based on verification success.
- **Integration**: Leverage Docker Labels and Healthchecks for infrastructure-level enforcement.
