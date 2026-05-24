---
title: "Tracing Once, Using Everywhere: Propagated Values for OMS and ADMS"
date: 2026-05-23T20:18:00-07:00
draft: false
description: "Why propagated values in traces and Export Subnetwork can reduce custom extractor, ETL, and middleware logic for OMS and ADMS integrations."
tags:
  - arcgis utility network
  - oms
  - adms
  - integration
  - tracing
  - export subnetwork
categories:
  - utilities
  - gis
mermaid: true
images:
  - /images/blog/trace-oms-adms/hooknose.jpg
  - /images/blog/trace-oms-adms/network-detail.jpg
  - /images/blog/trace-oms-adms/controlroom.jpg
---

![Utility network lines and grid concept](/images/hooknose.jpg)

# Tracing Once, Using Everywhere: Propagated Values for OMS and ADMS

ArcGIS Utility Network tracing already gives us the path through the network, but OMS and ADMS usually need more than a list of traversed features.[web:1645][web:1665] Export Subnetwork is intended to produce JSON that external systems can consume, and propagated values let that export carry network-derived answers instead of forcing those systems to recalculate them downstream.[web:1644][web:1665][web:1645]

## Traces are necessary, but not sufficient

A trace is great at answering a structural question: what is connected, and what can be traversed under the current rules.[web:1665][web:1666] That matters for feeders, switching, outage impact, and operational analysis, but OMS and ADMS also care about the values each feature effectively sees as part of that traced path.[web:1645][web:1644]

If all we send downstream is a feature list, every extractor, ETL job, or middleware layer ends up re-deriving context that GIS already knows.[web:1644][web:1645] That is where integrations get heavier than they need to be, especially when the real requirement is simple and the network model already contains the logic needed to compute the answer.[web:1645][web:1666]

## Connectivity, traversability, and propagation

It helps to keep three ideas separate. Export Subnetwork can return connectivity information based on network features connected through geometric coincidence or connectivity associations, while traces use network attributes and conditions to determine what is actually traversable.[web:1665][web:1666]

- **Connectivity** is the structural graph: features are linked through geometric coincidence or valid associations in the network model.[web:1665]
- **Traversability** is connectivity plus rules: the trace only moves through connected features that satisfy barriers, status, phase, or other network-attribute logic.[web:1666][web:1645]
- **Propagation** is the payoff: Esri describes propagators as deriving values for features downstream of subnetwork controllers as features are traversed during update or analytic events.[web:1645]

That third part is what makes the result export-friendly for OMS and ADMS.[web:1645][web:1644]

![Detailed network map with highlighted path](/images/network-detail.jpg)

## Why OMS and ADMS need different values

OMS and ADMS often need values that are not a simple copy of what sits on an individual GIS feature, because the useful operational value is frequently a network-derived value rather than a stored edit value.[web:1645][web:1666] Esri’s propagation documentation explicitly describes creating measurable fields, assigning network attributes, and optionally storing propagated values such as an energized phase that is derived from traversal logic.[web:1645]

That difference matters in practice. GIS might store configured phase or asset settings one way, while OMS or ADMS needs the effective phase, limiting value, or downstream state as seen from the feeder or controller context.[web:1645][web:1644]

## When code freezes block schema changes

I’ve worked with utilities, a GIS vendor, and an ADMS vendor where neither side wanted to make a schema change because a code freeze was already in place. The ask was usually simple, but the delivery path turned into custom extractor extensions, extra ETL logic, and middleware rules to solve something GIS could already reason about from the network.

That pattern is expensive because every downstream component ends up re-implementing a little bit of network intelligence outside the Utility Network. By contrast, Esri’s propagation model lets you configure how values are derived during traversal, and Export Subnetwork can emit JSON for external systems, which is exactly why propagating values for export feels so sweet in this integration space.[web:1645][web:1644][web:1665]

> [!note]
> **Code freeze reality:** when neither vendor wants a schema change, teams often compensate by extending extractors, layering ETL transforms, or teaching middleware to infer context that the network already knows. Propagated values shift that logic closer to the source by letting the trace or subnetwork export carry the answer downstream.[web:1645][web:1644]

## Why propagation is the elegant option

Attribute propagation is configured in the Utility Network by defining fields, coded domains, inline network attributes, and propagators in the subnetwork definition so values can be derived as traversal occurs.[web:1645][web:1661] Export Subnetwork also supports including network attributes and producing JSON for external systems, which makes it a natural handoff point for OMS and ADMS integration patterns.[web:1643][web:1665]

That means you can change the **behavior** of the trace result without demanding a physical schema change in every connected system.[web:1645][web:1643] In a frozen environment, that is often the difference between a clean configuration-driven solution and one more layer of custom logic that someone will have to maintain for years.[web:1645][web:1644]

## A practical example

Imagine GIS stores configured phase on devices and lines, but ADMS really wants the effective energized phase as seen downstream from the controller. Esri’s documentation describes a common pattern where a field such as “Phases Current” is paired with an inline network attribute and an optional propagated field such as “Phases Energized,” using coded values for A, B, C, and their combinations.[web:1645]

In that model, the propagated value is derived during traversal rather than manually maintained on every feature.[web:1645] Once Export Subnetwork includes the relevant results, the integration can map the exported value into OMS or ADMS logic without adding another permanent field to every downstream schema.[web:1643][web:1644][web:1665]

## From trace to OMS/ADMS

{{< mermaid >}}
flowchart LR
    subgraph GIS["GIS / Utility Network"]
      A[Network model<br/>Connectivity and associations]
      B[Trace and subnetwork configuration<br/>Attributes, barriers, propagators]
    end

    subgraph TRACE["Traversal logic"]
      C[Run trace<br/>Connected plus traversable]
      D[Propagate values<br/>Phase, voltage, pressure, status]
      E[Derive context<br/>What each feature effectively sees]
    end

    subgraph EXPORT["Export"]
      F[Export Subnetwork JSON<br/>IDs, attributes, derived values]
    end

    subgraph SYSTEMS["Downstream systems"]
      G[OMS<br/>Outage impact and affected customers]
      H[ADMS<br/>Operations and analysis]
    end

    A --> B --> C --> D --> E --> F
    F --> G
    F --> H
{{< /mermaid >}}

This is the pattern I like most: trace once in GIS, propagate the values that matter, and export results in a form OMS and ADMS can consume.[web:1644][web:1645][web:1665] It keeps the network intelligence close to the network instead of scattering it across extractors, ETL, and middleware.[web:1645][web:1666]

![Electric operations control room](/images/controlroom.jpg)

## Why this scales better

A static-field strategy sounds simple at first, but it tends to spread operational assumptions across multiple systems and teams. Propagation centralizes the logic in the Utility Network’s configuration, and Export Subnetwork provides a JSON-based delivery path for external consumers.[web:1645][web:1644][web:1665]

That is why I see propagated trace and subnetwork export results as more than a nice feature. They are a practical way to reduce unnecessary integration code when OMS and ADMS need values that differ from raw GIS storage or from what other downstream systems expect.[web:1645][web:1644]

## Image notes

Place these images in your Hugo `static/images/blog/trace-oms-adms/` folder so the paths above resolve correctly.[web:1664]

- `hero-grid.jpg`
- `network-detail.jpg`
- `control-room.jpg`