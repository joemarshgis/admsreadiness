---
title: "GIS in the Center: The Architecture Utilities Actually Operate On"
date: 2026-04-25
draft: false
tags:
  - GIS
  - utilities
  - ADMS
  - OMS
categories:
  - Architecture
cover:
  image: "https://pplx-res.cloudinary.com/image/upload/pplx_search_images/ec0e46fada53e0ecb01ce0756b6d7c70fd69f9fb.jpg"
  alt: "Utility grid control room with operators and large wall displays"
  caption: "Modern utility operations depend on a shared network model."
---

Utilities often talk about “integrated systems,” but in practice most integrations already revolve around one platform: GIS. Not as a mapping tool—but as the operational system of record that defines how the grid actually exists.

## The reality behind the diagram

The diagram in this post is closer to how utilities actually operate than most vendor slideware:

```mermaid
flowchart LR
  GIS["GIS (Network Model)"]:::center
  
  OMS["OMS"]
  ADMS["ADMS / DMS"]
  SCADA["SCADA"]
  DERMS["DERMS"]
  FIELD["Field / Work Mgmt"]
  PLAN["Planning / Engineering"]
  EAM["EAM / Asset Mgmt"]
  CIS["CIS"]
  AMI["AMI / MDMS"]
  
  GIS --> OMS
  GIS --> ADMS
  GIS --> SCADA
  GIS --> DERMS
  GIS --> FIELD
  GIS --> PLAN
  GIS --> EAM
  GIS --> CIS
  GIS --> AMI
  
  OMS -. feedback .-> GIS
  ADMS -. feedback .-> GIS
  
  classDef center fill=#01696f,stroke=#0c4e54,color=#ffffff;
```

- GIS is in the center as the system of record for the network model.
- OMS, ADMS, SCADA, DERMS, field, planning, asset, CIS, and AMI/MDMS all radiate out from that center.
- A few systems have dashed feedback loops back into GIS, where it makes sense to feed data and results into spatial and engineering analysis.

![Utility grid control room with operators and large wall displays](https://pplx-res.cloudinary.com/image/upload/pplx_search_images/ec0e46fada53e0ecb01ce0756b6d7c70fd69f9fb.jpg)

The architecture only matters if it helps people operate the grid in real time. For leaders in OMS, ADMS, and operations, the point of putting GIS at the center is not “better diagrams” — it is better situational awareness, decision support, and operational coordination.

If you treat this as just another “IT architecture picture,” you miss the point. It’s really a statement about data ownership and operational responsibility.

## Why GIS ends up in the middle

Modern utilities run a complex ecosystem of systems:

- OMS
- ADMS / DMS
- SCADA
- DERMS
- Engineering analysis tools
- Distribution planning tools
- Asset management (EAM / APM)
- Mobile workforce / field mobility / work management
- CIS
- AMI / MDMS

On paper, you can draw these as neat layers. In reality, they all depend on the same foundational data: the distribution network model. That model lives in GIS.

![Electrical utility substation at sunset](https://pplx-res.cloudinary.com/image/upload/pplx_search_images/ea9f379c4147aa97a415502acb213839f3ceccff.jpg)

At a practical level, GIS is what ties the physical system to the digital one. It is where substations, feeders, devices, and connectivity become a model that downstream systems can actually use.

GIS is the only place where all of these coexist in one model:

- Connectivity – how assets are actually connected.
- Topology – upstream/downstream relationships.
- Attribution – phase, voltage, conductor, device details.
- Spatial accuracy – where assets physically exist.
- Asset identity – stable IDs that other systems can reference.

No other system maintains all of that together. As a result:

- OMS consumes GIS connectivity and device modeling.
- ADMS depends on accurate phasing and feeder models.
- SCADA references GIS asset IDs and locations.
- DERMS needs spatial and electrical context.
- Engineering and planning tools rely on GIS for as‑built conditions.
- Field systems synchronize work against GIS features.

Whether intentional or not, GIS becomes the hub the rest of the ecosystem orbits around.

## Reading the diagram like an operator, not an architect

The diagram breaks that hub‑and‑spoke reality into three views that execs and program leaders can use:

**Operations – OMS, ADMS/DMS, SCADA, field/work management**

- Solid arrows from GIS show where those systems take their model and context from.
- Cross‑links between OMS, ADMS, and SCADA reflect how those systems have to agree on the same network model to support switching, FLISR, outage prediction, and DER operations.

**Planning & analysis – engineering studies and distribution planning**

- They pull the as‑built model from GIS, run studies, and inform future changes.
- Their results can feed back into GIS when planners modify how the network should be built or operated.

**Enterprise & customer – EAM, CIS, AMI/MDMS, DERMS**

- EAM tracks the lifecycle of the same assets GIS locates and connects.
- CIS and AMI/MDMS rely on accurate customer‑to‑meter and meter‑to‑network relationships.
- DERMS needs the GIS/ADMS model to understand where DERs really sit on the grid.

![Utility worker in bucket truck repairing electrical lines](https://pplx-res.cloudinary.com/image/upload/pplx_search_images/3c4ae761ef385b5d6bfba6edeb57c51c92a6e69b.jpg)

Field systems are one of the clearest reminders that the model has to work outside the control room. If crews cannot trust the location, connectivity, or asset context coming from GIS, the rest of the integration stack starts breaking down quickly.

The dashed arrows back into GIS—from OMS and ADMS in your diagram—represent feedback loops where it actually makes sense to bring data and results back into the spatial model:

- Outage and event history, so you can analyze where the system is fragile or recurring problems cluster.
- Switching and study results, so you can do spatiotemporal analysis of how the network is operated versus how it was designed.

That’s where executives and directors start seeing value beyond “integration for its own sake”: you get a model that supports continuous learning about the system, not just a one‑time ADMS go‑live.

## Where utilities get into trouble

The architecture itself is not the problem. Utilities run into trouble when GIS is treated as:

- A passive map.
- A downstream reporting tool.
- “Good enough” for operations.

Common failure patterns include:

- Self‑intersecting or disconnected lines.
- Missing or invalid phase designation.
- Invalid or missing operating voltage.
- Inconsistent feeder boundaries.
- Null or duplicate facility IDs.

Those issues don’t stay in GIS—they show up as:

- ADMS model failures and bad power flow results.
- OMS prediction inaccuracies.
- SCADA mismatches and suspect alarms.
- Field crews not trusting what they see on the screen.
- Longer restoration times and more operational risk.

## What actually works in practice

Utilities that succeed with ADMS, DERMS, and grid modernization generally do three things:

### 1. Treat GIS as a production system

- GIS changes are controlled, validated, and aligned to operations, not edited casually.
- There is a clear owner for “what is the network model?” and how it gets updated.

### 2. Perform real data readiness assessments

Before ADMS, DERMS, or OMS upgrades they deliberately assess:

- Network connectivity and topology.
- Phase and voltage integrity.
- Modeling consistency (devices, conductors, equipment).
- Attribute completeness for the functions they care about.

This is not a one‑time cleanup; it becomes a recurring discipline.

### 3. Design architecture around data ownership, not software logos

Instead of “everyone owns everything,” they define:

- GIS: authoritative for structure, connectivity, and core attributes.
- ADMS/OMS/SCADA: authoritative for real‑time states, switching, and control.
- DERMS and analytics: authoritative for specific optimization and forecasting use cases.

Integration flows respect those boundaries. Systems consume and enhance the model—they don’t silently redefine it.

## The executive takeaway

You don’t need another architecture drawing. You need a stronger center.

When GIS is treated as the authoritative network model—and the architecture is built around that reality—every downstream system performs better: ADMS, DERMS, OMS, SCADA, planning, and customer‑facing tools.

If your ADMS, OMS, or DERMS initiatives feel harder than they should, the issue is often not the application—it’s the data and ownership model at the center. The diagram isn’t just a technical picture; it’s a reminder to decide, explicitly:

- What does GIS own?
- What does each operational system own?
- Where do we want feedback loops back into GIS so we can actually learn from how we operate the grid?

Those are questions executives and program leaders can act on—without having to debug the diagram itself.


## Subscribe

If you prefer RSS, you can subscribe here:

- [RSS feed for ADMS Readiness](https://joemarshgis.github.io/admsreadiness/index.xml)
- [Posts feed](https://joemarshgis.github.io/admsreadiness/posts/index.xml)

If you want new posts by email, subscribe below.

{{< newsletter >}}