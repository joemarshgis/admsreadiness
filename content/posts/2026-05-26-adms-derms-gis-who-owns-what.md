---
title: "ADMS vs DERMS vs GIS: Who Owns What in a High-DER Grid?"
date: 2026-05-26T10:00:00-04:00
draft: false
tags: ["ADMS", "DERMS", "GIS", "DER"]
---

## The alphabet soup problem

[Intro]

- ADMS, DERMS, GIS all pitched as the “brain.”
- This is really a question of data and responsibility.

## Clear roles in a high-DER architecture

[Explain roles]

- GIS: network model (as-built).
- ADMS: as-operated view and control.
- DERMS: DER coordination and optimization.

## Integration flows that make sense

[Describe]

- GIS → ADMS/DERMS: topology and context.
- ADMS ↔ DERMS: limits, constraints, control.
- Feedback into GIS when the physical network changes.

## What happens when roles blur

[Examples]

- DERMS maintaining its own network model.
- ADMS diverging from GIS.
- Operational and governance consequences.

## Designing the governance

[Discuss RACI]
```mermaid
graph LR
  classDef R fill=#2ecc71,stroke=#1e8449,color=#fff;
  classDef A fill=#3498db,stroke=#21618c,color=#fff;
  classDef C fill=#f1c40f,stroke=#9a7d0a,color=#000;
  classDef I fill=#e5e7e9,stroke=#b2babb,color=#000;

  subgraph Legend
    lR[R = Responsible]
    lA[A = Accountable]
    lC[C = Consulted]
    lI[I = Informed]
    class lR R;
    class lA A;
    class lC C;
    class lI I;
  end

  %% Columns
  gis[GIS]
  adms[ADMS]
  derms[DERMS]

  %% Rows as labels (not connected, just anchors)
  nt_ab[Network topology (as-built)]
  nt_ao[Network topology (as-operated)]
  ar[Asset ratings]
  der_ic[DER interconnection data]
  rt_ops[Real-time grid operations]
  der_opt[DER optimization strategy]
  constraints[Constraint definitions]
  sync[Model synchronization]

  %% Row: Network topology (as-built)
  nt_ab --- nt_ab_gis((A))
  nt_ab --- nt_ab_adms((C))
  nt_ab --- nt_ab_derms((C))
  class nt_ab_gis A;
  class nt_ab_adms C;
  class nt_ab_derms C;

  %% Row: Network topology (as-operated)
  nt_ao --- nt_ao_gis((C))
  nt_ao --- nt_ao_adms((A))
  nt_ao --- nt_ao_derms((C))
  class nt_ao_gis C;
  class nt_ao_adms A;
  class nt_ao_derms C;

  %% Row: Asset ratings
  ar --- ar_gis((A))
  ar --- ar_adms((C))
  ar --- ar_derms((I))
  class ar_gis A;
  class ar_adms C;
  class ar_derms I;

  %% Row: DER interconnection data
  der_ic --- der_ic_gis((A))
  der_ic --- der_ic_adms((C))
  der_ic --- der_ic_derms((R))
  class der_ic_gis A;
  class der_ic_adms C;
  class der_ic_derms R;

  %% Row: Real-time grid operations
  rt_ops --- rt_ops_gis((I))
  rt_ops --- rt_ops_adms((A))
  rt_ops --- rt_ops_derms((C))
  class rt_ops_gis I;
  class rt_ops_adms A;
  class rt_ops_derms C;

  %% Row: DER optimization strategy
  der_opt --- der_opt_gis((I))
  der_opt --- der_opt_adms((C))
  der_opt --- der_opt_derms((A))
  class der_opt_gis I;
  class der_opt_adms C;
  class der_opt_derms A;

  %% Row: Constraint definitions
  constraints --- constraints_gis((C))
  constraints --- constraints_adms((A))
  constraints --- constraints_derms((A))
  class constraints_gis C;
  class constraints_adms A;
  class constraints_derms A;

  %% Row: Model synchronization
  sync --- sync_gis((A))
  sync --- sync_adms((R))
  sync --- sync_derms((R))
  class sync_gis A;
  class sync_adms R;
  class sync_derms R;
```
  
- Who owns what data.
- How changes are coordinated across the three.

## Executive takeaways

[Bullets on clarifying responsibilities and avoiding “three brains.”]


this is what i know about derms and data requirements; some from gis DERMS represents a module of ADMS that consists of a set of functionalities, ranging from planning
studies for integration of new DERs, through real-time monitoring and awareness of DERs, to the
constraint management and optimization of systems with high DER penetration in both real-time and
look-ahead (future) periods. 
As VVO and FLISR, DERMS also has Distribution Power Flow-based and SCADA-based approaches. The
Distribution Power Flow-based approach is more accurate and beneficial for Alliant since the
functionality relies on the State Estimation results, not only SCADA readings. As DERMS is aimed at
resolving DER-imposed issues such as under-/over-voltages, overloads on transformers/sections,
reverse power flows, etc., it is extremely important to have complete insight into the network state
to provide the full benefits of DERMS. 
Inputs: 
 Internal Model. 
 SCADA Resources: tap changers, capacitor banks, DERS settings. 
 Function Profile. 
 Types and number of customers/DERS to be added. 
 Load/Generation curves. 
 Weather data. 
 AMI data: voltage readings, voltage poll, Historical data from AMI, AMI Active Power,
Reactive Power. 
 Exclusion list.