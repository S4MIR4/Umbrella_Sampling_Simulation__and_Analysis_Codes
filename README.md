# Umbrella_Sampling_Simulation_and_Analysis_Codes
Tutorial on pulling simulations in GROMACS to calculate binding energy (ΔGbind) using umbrella sampling and WHAM. Covers system setup, pull code configuration, and PMF extraction. Designed for users familiar with GROMACS basics and topology organization.
```
Pulling-Simulations
├── 01_setup/ System preparation & topology
│ ├── ions.mdp
│ ├── minim.mdp
│ └── equilibration.mdp
│
├── 02_pulling/ Pulling simulation inputs
│ ├── pull.mdp
│ └── index.ndx
│
├── 03_umbrella/ Umbrella sampling setups
│ ├── umbrella.mdp
│ ├── confXXX.gro Window configurations
│ └── run.sh
│
├── 04_wham/ WHAM analysis
│ ├── wham.sh
│ └── pmf.xvg

```
