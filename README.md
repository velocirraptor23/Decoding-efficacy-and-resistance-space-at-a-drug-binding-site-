# Decoding-efficacy-and-resistance-space-at-a-drug-binding-site
This repo is for the paper entitled "Decoding efficacy and resistance space at a drug binding site" by Altmann  et al.
Link for the preprint. https://www.biorxiv.org/content/10.1101/2025.07.25.666894v1

The workflow implemented is divided into three parts: a), b) and c), and some more details are provided in d).

`a) MD simulations and clustering`

We developed a homology model, which is provided in the MD_simulation folder. We use the homology model to produce some simulation time, following the following settings:

System preparation and molecular dynamics. The protein–ligand complex was prepared for simulation using Schrödinger’s Maestro/Desmond workflow. The complex was parameterised with the OPLS4 force field; ligand parameters were assigned using the same force field and the Desmond/Schrödinger ligand preparation pipeline. The system was placed in an orthorhombic periodic box with dimensions 155.56 × 206.82 × 146.69 Å (box vectors as used during production), solvated with explicit TIP3P water, and neutralised with counterions. Additional salt was added to a final ionic strength of 0.15 M NaCl. Energy minimisation was performed until convergence using the Desmond default minimiser.

Systems were equilibrated using the standard Desmond relaxation protocol. In brief: (i) Brownian dynamics (NVT) at 10 K for 100 ps with solute heavy-atom restraints (force constant 50 kcal mol⁻¹ Å⁻²); (ii) 12 ps NVT at 10 K with Langevin thermostat (τ = 0.1 ps), restraints retained; (iii–iv) two 12 ps NPT steps at 10 K with restraints retained (Langevin thermostat τ = 0.1 ps; barostat τ = 50 ps); and (v) 24 ps NPT at 10 K with restraints removed (barostat τ = 2 ps).

Production simulations were performed in the NPT ensemble at 300 K and 1 atm using the Martyna–Tobias–Klein barostat (τ = 2 ps) and a Langevin thermostat (τ = 1 ps). A RESPA multiple-time-step integrator was used with an inner timestep of 2 fs and outer (long-range) timestep of 6 fs (timestep = [0.002 0.002 0.006]). Long-range electrostatics were treated with the U-series method and a 9 Å short-range cutoff. Initial velocities were sampled from a Maxwell–Boltzmann distribution at 300 K (random seed = 2007). Production length was 80 ns; coordinates were written every 100 ps and energies every 1.2 ps. Trajectories were saved in Desmond .dtr format and centred on the solute for analysis.

We clustered the simulation by RMSD, and then we selected some clusters as described in the paper. The folder MD_clusters contains the PDB cluster files.

`b) Free energy MMGBSA/Calculations`

Free energy MMGBSA/Calculations were performed for each of the clusters with mutations. For these calculations, we provide PDB files from each cluster; however, the calculation needs to be run externally using the Schrodinger suite (Residue Scanning Tool, 2023-2). We provide the final csv file with results ('all_combined_final.csv'). This tool implements a high-throughput workflow for testing mutations with the free energy associated (calculated with the MM/GBSA method) using wild-type as reference (baseline).

`c) EVO2 predictions`

We predicted EVO2 Scores using a Colab platform. To run the Evo2 prediction, we have provided a notebook guide; however, you may need to install additional packages depending on your environment. If you have any more questions, please visit. https://github.com/ArcInstitute/evo2.git. (Python version 3.12.11)

We first made all nucleotides that encode the protein, and we mutated each codon in the binding site. Then we subtracted the scores for each mutant and normalised from 0 to 1 with specific cutoffs (see paper details). A full colab notebook is provided in the Evo2_colab folder. The collected results were plotted using a notebook example in the Notebooks folder, as shown in Figure 7. In this notebook, we also combined MMGBSA/Calculations with Evo2 scores to obtain the final heatmaps.

`d) Additional information`

To recreate figures 6 and 7, please use these package versions

-Python 3.13.2
-matplotlib: 3.10.3
-seaborn: 0.13.2
-numpy: 2.2.4
-pandas: 2.2.3
-pycirclize: 1.9.1
