# Decoding-efficacy-and-resistance-space-at-a-drug-binding-site
This repo is for the paper entitled "Decoding efficacy and resistance space at a drug binding site" by Altmann  et al.
Link for the preprint. https://www.biorxiv.org/content/10.1101/2025.07.25.666894v1

The workflow implemented is divided in three parts a), b) and c)and some more details are provided d).

a) 
We developed a homology model and we provide full homology model in MD_clusters folder. We use the homology models to produce some simulation time following the next settings:
System preparation and molecular dynamics. The protein–ligand complex was prepared for simulation using Schrödinger’s Maestro/Desmond workflow. The complex was parameterised with the OPLS4 force field; ligand parameters were assigned using the same force field and the Desmond/Schrödinger ligand preparation pipeline. The system was placed in an orthorhombic periodic box with dimensions 155.56 × 206.82 × 146.69 Å (box vectors as used during production), solvated with explicit TIP3P water, and neutralised with counterions. Additional salt was added to a final ionic strength of 0.15 M NaCl. Energy minimisation was performed until convergence using the Desmond default minimiser.

Systems were equilibrated using the standard Desmond relaxation protocol. In brief: (i) Brownian dynamics (NVT) at 10 K for 100 ps with solute heavy-atom restraints (force constant 50 kcal mol⁻¹ Å⁻²); (ii) 12 ps NVT at 10 K with Langevin thermostat (τ = 0.1 ps), restraints retained; (iii–iv) two 12 ps NPT steps at 10 K with restraints retained (Langevin thermostat τ = 0.1 ps; barostat τ = 50 ps); and (v) 24 ps NPT at 10 K with restraints removed (barostat τ = 2 ps).

Production simulations were performed in the NPT ensemble at 300 K and 1 atm using the Martyna–Tobias–Klein barostat (τ = 2 ps) and a Langevin thermostat (τ = 1 ps). A RESPA multiple-time-step integrator was used with an inner timestep of 2 fs and outer (long-range) timestep of 6 fs (timestep = [0.002 0.002 0.006]). Long-range electrostatics were treated with the U-series method and a 9 Å short-range cutoff. Initial velocities were sampled from a Maxwell–Boltzmann distribution at 300 K (random seed = 2007). Production length was 80 ns; coordinates were written every 100 ps and energies every 1.2 ps. Trajectories were saved in Desmond .dtr format and centred on the solute for analysis.

We clustered the simulation by RMSD. adn we selected some clusters as it is described in the paper. Folder with PDB cluster files is in MD_clusters folder.

b) Free enegy MMGBSA/Calculations for each of the clusters with mutations. For this calculations we provide PDB files from each cluster but the calculation needs to be run externally with Schrodinger suite (﻿﻿Residue scanning tool, 2023-2). We provide the final csv file with results ('all_combined_final.csv')

c) We made a prediction for EVO2 Scores using a colab platform.
For running Evo2 prediction we deployed a notebook guidance but you may need to install packages depending of your enviroment.
For further questions, please visit. https://github.com/ArcInstitute/evo2.git
-Python version 3.12.11
We first made all nucleotides that encode the protein and we mutate each codon. Then we substracted the scores for each mutant and normalized from 0 to 1 with specific cutoffs (see paper details).
Collected results were plotted following a notebook example in Notebooks folder, Figure 7.
In notebook 7 we also conmbined MMGBSA/Calculations with Evo2 scores to get the final heatmaps.

d) To recreate figures 6 and 7, please use these package versions

-Python 3.13.2
-matplotlib: 3.10.3
-seaborn: 0.13.2
-numpy: 2.2.4
-pandas: 2.2.3
-pycirclize: 1.9.1
