---
title: "From Tickets to Topology: Designing OMS Integrations Around the Network Model"
date: 2026-05-05T10:00:00-04:00
draft: true
tags: ["OMS", "GIS", "ADMS", "Integration"]
---

## OMS is only as good as its model

[Intro – 1–2 paragraphs]

- Example outage where OMS prediction was wrong.
- Set up the idea that the issue was the network model, not just the OMS app.

## The role of GIS and ADMS in OMS

### GIS: where the network actually lives

[Paragraph(s) about GIS as network model, connectivity, topology, IDs.]

### ADMS: as-operated view on top of that

[Paragraph(s) on ADMS knowing switch states, feeder configuration.]

### OMS: incident and prediction layer

[Explain OMS as prediction/workflow engine that depends on the shared model.]

## Integration patterns that work

### One network model, multiple consumers

[Describe GIS as source, OMS/ADMS as consumers.]

### Robust GIS → OMS synchronization

[How often to sync, versioning, guardrails.]

### OMS and ADMS walking in lockstep

[Examples of shared model and state between OMS and ADMS.]

## Failure patterns when OMS has its own model

[Bullets / paragraphs]

- Divergent network models.
- Orphaned customers, wrong outage extents.
- “Local fixes” in OMS/ADMS that never reach GIS.

## Designing for operations, not interfaces

[Discuss governance, validation, simple QA dashboards.]

## Executive takeaways

[5–7 bullets a VP/Director can act on.]
