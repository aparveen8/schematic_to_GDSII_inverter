# CMOS Inverter Design and GDSII Generation using Cadence Virtuoso (GPDK90)

This repository documents the design, simulation, and layout process for a **CMOS Inverter** using **Cadence Virtuoso** with **GPDK90 technology**.

## Table of Contents

1. [ Overview](#Overview)
2. [Tools & Technologies](#tools--technologies)
3. [Project Workflow](#project-workflow)
   - [Schematic Design](#1-schematic-design)
   - [Testbench Setup](#2-testbench-setup)
   - [Analysis Setup](#3-analysis-setup)
   - [Simulation Results](#4-simulation-results)
   - [Layout Design](#5-layout-design)
   - [DRC & LVS Checks](#6-drc--lvs-checks)
   - [RC Parasitic Extraction](#7-rc-parasitic-extraction)
   - [Pre-Layout and Post-Layout Simulations](#8-pre-layout-and-post-layout-simulations)
   - [GDSII File Generation](#9-gdsii-file-generation)
4. [Conclusion](#conclusion)

##  Overview

This project explores the design and analysis of a CMOS inverter using the **GPDK90 technology node**. The workflow includes schematic design, simulations, layout generation, DRC & LVS verification, parasitic extraction, and the final generation of the GDSII file for tapeout. Additionally, pre-layout and post-layout simulations are conducted to evaluate the impact of layout parasitics on inverter performance, specifically delay. 

## Tools & Technologies

- **Cadence Virtuoso**: The primary software used for schematic design, simulations, and layout generation.
- **GPDK90 Technology**: A 90nm CMOS process technology used for the design of the CMOS inverter.

## Project Workflow
To begin with, Cadence was launched. The next step involved creating a new library in the Library Manager. This was achieved by selecting File → New → Library from the Library Manager's menu, which prompted the "New Library" form. In this form, the library name **inverter** was entered in the Name section. Next, in the "Technology File for New Library" form, the option Attach to an existing techfile was chosen, and upon clicking OK, the "Attach Design Library to Technology File" form appeared. From the cyclic dropdown menu in this form, the gpdk090 technology file was selected and confirmed by clicking OK. These steps successfully created the new library and linked it to the chosen technology file, proceed with File → New → cell view to create schematic.

### 1. Schematic Design
The first step in the design process involved creating the schematic of the CMOS inverter. The schematic was carefully constructed to ensure that both PMOS and NMOS transistors were properly sized to meet the desired electrical characteristics. Following the schematic design, a symbol for the CMOS inverter was generated, allowing it to be reused in subsequent stages. For step by step design process, can refer the manual attached above. 
<p align="center">
  <img src="inv img/sch inv.png" />
</p>
<p align="center">
  <img src="inv img/symbol inv.png" />
</p>

### 2. Testbench Setup

To evaluate the inverter’s performance, a testbench was created in the simulation environment. The testbench was configured to stimulate the CMOS inverter with a range of input signals, allowing for the observation of its response and the extraction of key performance parameters such as the **Voltage Transfer Characteristics (VTC)** and the **threshold voltage**.
<p align="center">
  <img src="inv img/tb inv.png" />
</p>

### 3. Analysis Setup

The **Analog Design Environment (ADE)** was set up for transient and DC sweep analysis. The transient analysis allowed for the observation of dynamic behavior, while the DC sweep analysis helped in determining the inverter’s VTC and threshold voltage.
<p align="center">
  <img src="inv img/ade l step 1.png" />
</p>
<p align="center">
  <img src="inv img/ade l step 2.png" />
</p>
<p align="center">
  <img src="inv img/ade l step 3.png" />
</p>
<p align="center">
  <img src="inv img/ade l step 4.png" />
</p>
<p align="center">
  <img src="inv img/ade l step.png" />
</p>

### 4. Simulation Results

Both **pre-layout** and **post-layout** simulations were performed:
- **Pre-Layout Simulation**: Conducted with ideal models for all components and no parasitic effects. The **VTC** and threshold voltage were extracted.
<p align="center">
  <img src="inv img/dc and transient inv.png" />
</p>

- **Post-Layout Simulation**: Parasitics were introduced based on the extracted RC parasitic values, and delay was recalculated.

### 5. Layout Design

The physical layout of the CMOS inverter was created, ensuring that it adheres to the design rules for the GPDK90 process technology. The layout design incorporates the placement of both transistors, routing of interconnections, and optimization for performance and area.
<p align="center">
  <img src="inv img/layout inv.png" />
</p>

### 6. DRC & LVS Checks

The design underwent **Design Rule Check (DRC)** and **Layout Versus Schematic (LVS)**. The DRC ensures that the layout meets the manufacturing process’s design constraints, while the LVS check ensures that the layout matches the schematic design, verifying functional correctness.
<p align="center">
  <img src="inv img/drc inv.png" />
</p>

<p align="center">
  <img src="inv img/lvs inv.png" />
</p>

### 7. RC Parasitic Extraction

Once the layout was verified, the RC parasitics (resistances and capacitances of interconnects) were extracted. These parasitics impact the delay and overall performance of the circuit, and their extraction is essential for accurate post-layout simulation results.
<p align="center">
  <img src="inv img/sch inv.png" />
</p>

### 8. Pre-Layout and Post-Layout Simulations

Pre-layout simulations were conducted using ideal models for the components, without considering the parasitic effects of the layout. Post-layout simulations, on the other hand, incorporated the extracted parasitics, providing a more realistic performance assessment. A detailed comparison of the results from both simulations reveals the impact of layout parasitics on delay and signal integrity.

#### - Pre-Layout Results:
  The simulation results for the pre-layout design yielded a delay of 118.1 ps and the expected Voltage Transfer Characteristics (VTC).
<p align="center">
  <img src="inv img/dc and delay inv.png" />
</p>
  
#### - Post-Layout Results:
After including the parasitic effects, the post-layout simulation results showed an increased delay of 135.4 ps, as expected due to the added parasitics.


### 9. GDSII File Generation

Finally, the GDSII file, which contains the geometric data necessary for fabrication, was generated. This file represents the final layout, ready for fabrication at the foundry.

## Conclusion

The CMOS inverter design was successfully completed, encompassing schematic design, simulation, layout creation, and GDSII file generation. A thorough comparison between pre-layout and post-layout simulations was conducted, demonstrating a slight increase in delay post-layout due to the parasitic effects introduced by the layout. The final GDSII file is now prepared for tapeout, marking the completion of the design process.

