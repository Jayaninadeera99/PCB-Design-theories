# 📘 PCB Design Theory Essentials
 
A condensed reference of the **most important PCB design theories** the core concepts most frequently tested in exams, interviews, and used in real design work.
 
---
 
## 📑 Table of Contents
 
- [1. What is a PCB](#1-what-is-a-pcb)
- [2. PCB Types](#2-pcb-types)
- [3. Materials](#3-materials)
- [4. Layer Stack-up](#4-layer-stack-up)
- [5. Design Flow](#5-design-flow)
- [6. Trace Width & Current Capacity](#6-trace-width--current-capacity)
- [7. Vias](#7-vias)
- [8. Power & Ground Planes](#8-power--ground-planes)
- [9. Signal Integrity](#9-signal-integrity)
- [10. EMI / EMC](#10-emi--emc)
- [11. Thermal Management](#11-thermal-management)
- [12. Design Rules (DRC)](#12-design-rules-drc)
- [13. DFM / DFA](#13-dfm--dfa)
- [14. High-Speed Design](#14-high-speed-design)
- [15. Testing (DFT)](#15-testing-dft)
- [16. Quick Revision Table](#16-quick-revision-table)
---
 
## 1. What is a PCB
 
A **Printed Circuit Board** mechanically supports and electrically connects components using copper traces etched onto an insulating substrate.
 
**Why PCBs:**
- Reliable, repeatable connections (no loose wiring)
- Compact, mass-producible via automated assembly
- Controllable electrical properties (impedance, capacitance)
- Better heat dissipation via copper planes
---
 
## 2. PCB Types
 
| Type | Description |
|---|---|
| **Single-sided** | Copper on one side only  simplest, cheapest |
| **Double-sided** | Copper both sides, connected via vias |
| **Multilayer** | Alternating copper/dielectric layers needed for density & controlled impedance |
| **Rigid** | Standard fixed FR4 board |
| **Flex** | Polyimide-based, bendable |
| **Rigid-flex** | Rigid sections + flexible joints |
| **HDI** | Microvias, fine-pitch traces for high pin-density |
 
---
 
## 3. Materials
 
| Material | Dk (εr) | Use |
|---|---|---|
| FR4 | 4.2–4.8 | General purpose |
| Polyimide | ~3.4 | Flex PCBs |
| Rogers / PTFE | 2.2–3.5 | RF/microwave |
| Metal-core | — | High thermal dissipation |
 
- **Copper weight**: 1 oz ≈ 35 µm higher weight = more current capacity
- **Core** = pre-laminated copper-clad sheet; **Prepreg** = uncured resin/glass layer that bonds cores together during lamination
- **Surface finishes**: HASL (cheap, uneven), ENIG (flat, fine-pitch), OSP (cheap, short shelflife)
---
 
## 4. Layer Stack-up
 
> **Golden rule**: Every signal layer should sit next to a **solid reference plane** (ground or power).
 
Typical 4-layer stack:
```
L1  Signal   (Top)
L2  Ground
L3  Power
L4  Signal   (Bottom)
```
 
- Keeps impedance controlled
- Keeps signal return current path short and continuous
- Symmetric stack-up avoids board warping
---
 
## 5. Design Flow
 
```
Requirements → Schematic Capture → Component Placement
     → Routing → DRC / ERC → Gerber/Drill/BOM Output
     → Fabrication → Assembly → Test
```
 
---
 
## 6. Trace Width & Current Capacity
 
Governed by **IPC-2221**. Depends on:
- Trace width & copper thickness (wider/thicker = more current)
- Allowed temperature rise
- Internal traces carry **less** current than external (worse heat dissipation)
---
 
## 7. Vias
 
| Via Type | Connects |
|---|---|
| Through-hole | All layers (drilled through entire board) |
| Blind | Outer layer ↔ inner layer(s) |
| Buried | Inner layers only |
| Microvia | HDI boards, laserdrilled, ≤150 µm |
| Via-in-pad | Directly inside a component pad (fine-pitch BGA) |
 
---
 
## 8. Power & Ground Planes
 
- Solid ground plane → low-impedance return path, less EMI/crosstalk
- Power + ground planes close together → extra high-frequency decoupling capacitance
- **Never route a signal across a plane split** — it breaks the return current path
- Place decoupling caps (e.g., 100 nF + 10 µF) **as close as possible** to IC power pins
---
 
## 9. Signal Integrity
 
| Issue | Cause | Fix |
|---|---|---|
| Reflection | Impedance mismatch | Controlled impedance + termination |
| Crosstalk | Coupled adjacent traces | 3W spacing rule, ground shielding |
| Ringing | Fast edges, mismatched Z | Series termination resistor |
| Ground bounce | Shared return path noise | Solid plane + decoupling |
 
**Controlled impedance**: single-ended ~50 Ω, differential ~90–100 Ω — set by trace width, dielectric thickness, and Dk.
 
---
 
## 10. EMI / EMC
 
- Minimize current **loop area** (signal + return path close together)
- Avoid gaps in reference plane under high-speed traces
- Add ferrite beads/common mode chokes near noise sources
- Terminate transmission lines properly
---
 
## 11. Thermal Management
 
- Use copper pours + thermal vias to spread/conduct heat
- Increase copper weight on high current layers
- Consider metal-core PCBs for power/LED applications
- Watch CTE mismatch on BGA/QFN packages
---
 
## 12. Design Rules (DRC)
 
| Rule | Typical Value |
|---|---|
| Min trace width/spacing | 0.15–0.2 mm |
| Min via drill | 0.2–0.3 mm |
| Min annular ring | 0.05–0.15 mm |
| Min board-edge clearance | 0.5–1 mm |
 
**ERC** (schematic-level) catches unconnected pins, conflicting outputs, missing power connections.
 
---
 
## 13. DFM / DFA
 
- Stay within fabricator's min trace/space/drill capability
- Avoid acid traps (acute copper angles)
- Consistent copper density → even etching
- Clear silkscreen polarity/pin-1 marks
- Adequate spacing for pick-and-place & rework
---
 
## 14. High-Speed Design
 
- Treat trace as a transmission line once length is significant relative to signal rise time
- Match differential pair / bus lengths
- No stubs on high-speed nets
- Follow vendor layout guides (e.g., DDR memory)
---
 
## 15. Testing (DFT)
 
| Method | Notes |
|---|---|
| ICT | Bed-of-nails, probes test points |
| Flying probe | No fixture, good for prototypes |
| Boundary scan (JTAG) | Tests digital IC interconnects |
| AOI | Camera-based solder defect inspection |
| X-ray | Hidden joints (e.g., under BGA) |
 
> Add test points on nets that can't be probed directly (e.g., under a BGA).
 
---
 
## 16. Quick Revision Table
 
| Concept | Remember |
|---|---|
| PCB purpose | Mechanical support + reliable interconnection |
| Stack-up | Signal layers next to solid reference planes |
| Trace width | Set by current capacity + impedance target |
| Vias | Through hole → blind/buried/microvia (HDI) |
| Decoupling | Caps as close as possible to IC power pins |
| Crosstalk | 3W rule, adjacent ground plane |
| Return path | Never cross a plane split under a signal |
| DFM | Design within fabricator's capability |
| DFT | Test points + boundary scan for hidden nets |
 
---
 
📌 *Condensed from a full PCB Design Theory study note — see the companion Word document for detailed explanations, diagrams, and worked examples.*
