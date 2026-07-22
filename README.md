# Hydropower Teaching Simulators

This repository holds two self-contained, no-dependency HTML teaching tools.
Open either file directly in any modern browser (Chrome / Edge / Firefox) — no
server, build step or libraries required.

| File | What it is |
|---|---|
| [`hydro-bernoulli-simulator.html`](hydro-bernoulli-simulator.html) | **Penstock & turbine — Bernoulli hydraulics simulator** (see below) |
| [`governor-simulator.html`](governor-simulator.html) | Kaplan bulb-turbine governor hydraulic-system simulator |

---

## Penstock & Turbine — Bernoulli Hydraulics Simulator

A physics-informed, steady-state model of a two-reservoir hydropower scheme:
a **headrace** (upper reservoir) and **tailrace** (lower reservoir) joined by a
**penstock** with a **turbine** in the line. It solves the extended Bernoulli
(energy) equation *with real losses* and turbine head, updating a live
cross-section, numeric readouts and grade-line charts as you drive the controls.

### The physics

Energy balance between the two free surfaces (both at atmospheric pressure,
both effectively still because the reservoirs are large):

```
z₁ + p₁/ρg + V₁²/2g  =  z₂ + p₂/ρg + V₂²/2g  +  h_turbine + h_loss
        ⟶        H_gross = h_turbine + h_loss
```

* **Head loss** `h_loss = (f·L/D + ΣK)·V²/2g` — Darcy–Weisbach friction plus
  entrance/exit/bend minor losses. The Darcy factor `f` is found from the
  **Swamee–Jain** correlation (laminar `64/Re` below Re = 2300) and iterated
  with the flow so it stays consistent with velocity and temperature.
* **Turbine + wicket gate** behave as a variable nozzle,
  `Q = C_d·A_throat·(gate) · √(2g·H_net)`, so closing the gate throttles the
  flow and re-partitions the available head. Shaft power `P = η·ρg·Q·H_net`.
* **Water properties** (density, viscosity, vapour pressure) are interpolated
  from standard tables at the chosen temperature; **pipe roughness** ε comes
  from the selected material.

### User-controllable inputs

* Gross head between the two free surfaces
* Intake depth below the upper surface
* **Turbine centre height below the upper surface** — moves the machine up or
  down (changing its submergence and cavitation margin) while the gross head is
  held constant; the outlet submergence below the tailwater is derived from it
* Penstock length, draft length and inside diameter
* Pipe material (PVC → riveted steel) and water temperature
* Wicket-gate opening, turbine throat diameter and efficiency
* Minor-loss coefficients and turbine discharge coefficient (assumptions)

### What it computes

Flow rate, pipe velocity, Reynolds number and flow regime, friction factor,
net head, head-loss breakdown, turbine **inlet/outlet pressures** (gauge and
absolute), pressure drop across the turbine, hydraulic and shaft power, NPSH and
Thoma cavitation number — plus **Energy- and Hydraulic-Grade-Line** and
**power-vs-gate** charts.

### Warnings

The tool flags **cavitation** (minimum absolute pressure reaching the water's
vapour pressure, or low Thoma σ), **backflow / no-flow** (tailrace at or above
the headrace), a **closed gate**, high penstock velocity, and laminar/
transitional flow. This is a steady-state teaching model — it does not resolve
water-hammer transients or real turbine efficiency curves; values are indicative.

---

## Kaplan Bulb Turbine — Governor Hydraulic System Simulator

Interactive HTML teaching model of the turbine & governor control system
(ANDRITZ Hydro drawing **NBE-102-02-001**, New Bong Escape HPP).

## How to run

No installation, no server, no libraries needed:

1. Open the folder in VSCode.
2. Right-click `governor-simulator.html` → **Open with Live Server** (if you have the
   extension), **or** simply double-click the file to open it in any browser
   (Chrome / Edge / Firefox).

## What it simulates

| System | KKS |
|---|---|
| Oil pumps + unloader solenoids + relief valves | MEX11 / MEX12 |
| Oil cooling pump, cooler, cooling-water solenoid | MEX14 |
| Piston accumulators + N₂ bottles + safety valves + pressure switches | MEX16 / MEX17 |
| Leakage oil pumps and tank | MEX18 / MEX19 |
| Wicket-gate proportional valve (pilot + main stage), dual filter, ESD check valves, throttle | MEX20 |
| Runner-blade proportional valve, throttles, hub oil tank + replenishing valves | MEX30 |
| ESD solenoids, hydraulic valves, cartridge valves | MEX70 |
| Mechanical overspeed device + position switch | MEA70 AA201 / CG201 |
| Sump-tank level switches | MEX10 CL101/102/103 |

## Suggested lesson sequence

1. Switch **Oil pump 1 ON** — watch the accumulators charge to 63 bar.
2. Open the **wicket gates** with the slider (interlocked below 50 bar) —
   the runner blades follow automatically on the combinator cam.
3. Close the **generator breaker** at 95–105 % speed (use *Governor speed control*).
4. Press **LOAD REJECTION** — the speed rises and the electrical overspeed
   protection (115 %) trips the unit through the ESD circuit.
5. Disable the electrical trip and repeat — the **mechanical overspeed device
   MEA70 AA201 (140 %)** acts as the backup.
6. Try the red **ESD pushbutton**, the ESD solenoids (click them in the diagram),
   hub-tank replenishing, cooling and the leakage pumps.

Hover any component in the diagram to see its KKS code and function;
click pumps, solenoids and isolating valves to operate them.
Every oil path animates in the colour of its function (pressure, control,
drain, leakage, cooling, N₂, trip signal) so the flow can be followed live.
