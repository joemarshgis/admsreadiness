---
title: "Integration Anti-Patterns: Ten Ways Utilities Break Their Own Architecture"
date: 2026-06-30T10:00:00-04:00
draft: true
tags: ["Architecture", "Integration", "GIS", "ADMS", "OMS"]
---

## Integrations vs capabilities

[Intro]

- The cost of “just one more interface.”
- Why architecture diagrams often hide the real issues.

## Anti-patterns: competing network models

[Describe]

- OMS with its own model.
- DERMS with its own model.
- ADMS corrections never fed back into GIS.

## Anti-patterns: ETL hairballs

[Explain]

- One-off scripts with no owner.
- Multiple sources of truth for same attribute.
- Critical logic buried in middleware.

## Anti-patterns: organizational missteps

[Discuss]

- Nobody owning the center (GIS).
- Vendor-led architectures ignoring data realities.
- “Everyone owns everything” vs clear RACI.
- No funding for sustained data quality.

## A better reference model

[Describe]

- GIS as hub with clear data ownership.
- Operational systems as consumers/enhancers.
- Explicit feedback loops, not accidental ones.

## Executive takeaways

[How to spot and start fixing these anti-patterns.]
