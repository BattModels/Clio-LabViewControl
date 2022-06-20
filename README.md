# Clio-LabViewControl

LabView control suite for Clio instrument.

![](figures/clio_diagram_upgraded.png?raw=true)

Clio is liquid electrolyte specific laboratory automation, custom built into a glovebox for the purpose of accelerating design/optimization of materials utilizing liquid electrolytes.

## Installation
+ Written for LabView 2019 (32-bit).
+ Download and add all files given into a LabView project. Top-level VIs should be moved to a *Web Resources* sub-banner on LabView (see [here](https://www.ni.com/docs/en-US/bundle/labview/page/lvhowto/build_web_service.html)).
+ As detailed in a recent publication, certain devices (e.g. the FMI pumps) for which this code is written for, must have their .dll files pointed to in LabView. VIs for which this is important are listed below. Other devices are controlled via .bat file or VISA/Serial.

## Descriptions

The repo is organized as follows:
1. **1_TopLevel** : HTTP-level APIs that summarize orchestration per individual experimental runs (i.e. of a given electrolyte).
    + *RUNfast_derated2.vi*: main experiment VI making a liquid electrolyte and measuring conductivity, viscosity, and density
    + *RINSE.vi*: clean-up VI that runs between each electrolyte
    + *sync.vi*: updating an inventory CSV between runs
2. **2_Bundles** : one step lower APIs (not HTTP facing), these tend to summarize orchestration per individual measurement (which are composited in **1_TopLevel** VIs. A few key VIs are described below:
    + *DENSITY.vi*: VI integrating pump, valving, and balance for density measurement
    + *PS_COND+TEMP.vi*: VI integrating PalmSens, conductivity leads, and thermocouple for conductivity and temperature measurement. See .bat files in **PS_methods** for dependencies of this VI. PalmSens methods files are also included for ease of parsing - these can be opened by PalmSens proprietary software, while the .bat files are used by the VIs.
    + *dose_FMI.vi*: manages pump 1 for accurately dosing (in serial) each component of the electrolyte
3. **3_Supporting** : mainly lower level VIs that accomplish singular purposes, with the sole exception of the *Viscosity* folder. Described below:
    + *Viscosity/VISCOSITY.vi* : state machine for handling Brookfield measurement.
4. **4_LowLevel** : instrument/serial-connection specific VIs. DVT VIs control switching and mixer. FMI VIs control pumps (note that these VIs must be pointed at .dll file from FMI). *PS_CMD.vi* manages .bat input to the PalmSens. VICI VIs manage VICI multi-port valve for dosing.
5. **5_Controls** : .ctl files for type definition on Brookfield and PS_CMD VIs
