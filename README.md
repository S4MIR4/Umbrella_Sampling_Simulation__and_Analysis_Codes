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
```
Procedure:
Step by step breakdown:

Core idea of the project:
The binding energy (ΔG_bind) between two molecules (for example, a protein and a ligand) can be estimated from the Potential of Mean Force (PMF).
The PMF describes how the free energy changes as the molecules are pulled apart (or brought together) along a reaction coordinate — typically the distance between their centers of mass (COMs).

How we get the PMF: Umbrella Sampling:
Directly simulating binding/unbinding is inefficient (rare events, too slow). Instead, we use umbrella sampling, a method that "guides" the system to sample important regions by applying a biasing potential.

Step by step:
1. Generate Initial Configurations (Pulling Step)
Start with the bound state (ligand close to receptor).
Slowly "pull" the ligand away along one axis (reaction coordinate = COM distance).
Save multiple snapshots (configurations) at different distances.
These snapshots are the starting points for umbrella windows.
2.Extract Frames (Window Setup)
From the pulling trajectory, select frames spaced at regular COM intervals (e.g., every 0.1–0.2 nm).
Each frame will become an umbrella window.
3.Umbrella Sampling Simulations (Biased MD)
For each window, apply a harmonic restraint to keep the ligand near that specific COM distance.
This restraint is called the umbrella bias — it ensures good sampling in regions the ligand wouldn’t naturally visit often.
Multiple windows are run, covering the whole reaction coordinate (from bound to unbound).
Overlap is essential: neighboring windows should have some overlap in sampled positions so data can be stitched smoothly.
4.Reconstruct PMF with WHAM
All the biased simulations generate histograms of sampled positions.
These histograms are combined using the Weighted Histogram Analysis Method (WHAM).
WHAM removes the effect of the bias and reconstructs the unbiased free energy profile (PMF).
-Results:
The PMF curve shows the free energy landscape as the ligand moves away from the binding site.
The difference in free energy between the bound and unbound states gives the binding free energy ΔG_bind.

We pull → create windows → restrain ligand in each → stitch together histograms → get PMF → extract ΔG_bind.

See the schematic figure in the repository.
