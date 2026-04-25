---
title: "GIS in the Center: The Architecture Utilities Actually Operate On"
date: 2026-04-25
draft: true
tags:
  - GIS
  - utilities
  - ADMS
  - OMS
categories:
  - Architecture
---# GIS in the Center: The Architecture Utilities Actually Operate On

Utilities often talk about “integrated systems,” but in practice,
most integrations already revolve around one platform:

**GIS.**

Not as a mapping tool—but as the operational system of record
that defines how the grid actually exists.

## The Reality of Utility Architecture

Modern utilities run a complex ecosystem of systems:

- OMS
- ADMS / DMS
- SCADA
- DERMS
- Engineering Analysis
- Distribution Planning
- Asset Management (EAM / APM)
- Mobile Workforce / Field Mobility
- Work Management
- CIS
- AMI / MDMS

On architecture diagrams, these systems are often drawn in neat layers
or point-to-point integrations.

In the real world, they all depend on **the same foundational data**:
the electric network model.

That model lives in GIS.

## Why GIS Ends Up in the Middle

GIS uniquely combines:

- **Connectivity** – how assets are electrically connected
- **Topology** – upstream/downstream relationships
- **Attribution** – phase, voltage, conductor, device status
- **Spatial accuracy** – where assets physically exist
- **Asset identity** – consistent IDs across systems

No other system maintains *all* of these together.

As a result:

- OMS consumes GIS connectivity and device modeling
- ADMS requires accurate phasing and feeder models
- SCADA references GIS asset IDs and locations
- DERMS depends on spatial and electrical context
- Engineering tools rely on GIS for as-built conditions
- Field mobility systems synchronize work against GIS features

Whether intentional or not, **GIS becomes the hub**.

## A Practical “GIS-in-the-Center” Model

A more honest architecture diagram looks like this:

- **GIS at the center**
- All operational and analytical systems integrating outward
- Data flowing *from* GIS to consuming systems
- Select feedback loops returning status or measurements

In this model:
- GIS is authoritative for structure, connectivity, and attributes
- Other systems are authoritative for:
  - Real-time telemetry
  - Outage states
  - Switching operations
  - Analytics and forecasting

This separation of responsibility is critical.

## Where Utilities Run Into Trouble

Problems arise when GIS is treated as:

- A passive map
- A downstream reporting tool
- “Good enough” for operations

Common failure points include:
- Self-intersecting or disconnected lines
- Missing or invalid phase designation
- Invalid or missing operating voltage
- Inconsistent feeder boundaries
- Null or duplicate facility IDs

These issues don’t just affect GIS—they cascade into:
- ADMS model failures
- OMS prediction inaccuracies
- SCADA mismatches
- Field crew confusion
- Longer restoration times

## What Actually Works

Utilities that succeed tend to do three things:

### 1. Treat GIS as a Production System
GIS changes are controlled, validated, and aligned to operations—
not edited casually.

### 2. Perform Data Readiness Assessments
Before OMS or ADMS implementations or upgrades, they assess:
- Network connectivity
- Phase and voltage integrity
- Modeling consistency
- Attribute completeness

### 3. Design Architecture Around Data Ownership
Instead of “everyone owns everything,” they define:
- GIS owns structure and connectivity
- Operational systems consume and enhance—but don’t redefine—the model

## The Bottom Line

Utilities don’t need *more* integrations.
They need a **stronger center**.

When GIS is treated as the authoritative network model—
and architected accordingly—
every downstream system performs better.

Not because GIS does more,
but because it finally does what it’s uniquely positioned to do.

---

*If OMS, ADMS, or DERMS struggles feel familiar, the problem is often not the application—it's the data at the center.*
