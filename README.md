# Kaplan Bulb Turbine — Governor Hydraulic System Simulator

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
