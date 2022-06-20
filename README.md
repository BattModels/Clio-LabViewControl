# Clio-LabViewControl

LabView control suite for Clio instrument.

![](figures/clio_diagram_upgraded.png?raw=true)

Clio is liquid electrolyte specific laboratory automation, custom built into a glovebox for the purpose of accelerating design/optimization of materials utilizing liquid electrolytes.

The repo is organized as follows:
1. **1_TopLevel** : HTTP-level APIs that summarize orchestration per individual experimental runs (i.e. of a given electrolyte).
    + *RUNfast_derated2.vi*: main experiment VI making a liquid electrolyte and measuring conductivity, viscosity, and density
    + *RINSE.vi*: clean-up VI that runs between each electrolyte
    + *sync.vi*: updating an inventory CSV between runs
2. **2_Bundles** : one step lower APIs (not HTTP facing), these tend to summarize orchestration per 
