# Dynamic Vertical Triplet Energies (DvTE) Generation and Processign

<div align="center">
  <img src="./DvTE.png" alt="Description" width="300">
</div>

[Under Development]

## Synopsis:

Workflow and protocol for recording dynamic vertical triplet energies (DvTEs) based on the following pre-print (Link).

The code is based on two main packages: Dynamic Vertical Triplet Energy Generation (DvTEGen) which prepares input files for quantum mechanical (QM) calculations from input molecular dynamics (MD) trajectory files, and Dynamic Vertical Triplet Energies Processor (DvTEProc) which analyses the output QM files to provide a prediction of molecular triplet energies.

The code is currently designed to work with the Gaussian16 environment with plans for integration with other QM packages such as ORCA and QChem. Currently the user is require to provide dynamic trajectories and execute separately the QM calculations, however future plans include development of a complete automated workflow for the UNIX environment.

## Dynamic Vertical Triplet Energy Generation (DvTEGen)

Description: This Jupyter Notebook proceses the inputed quasicaliscal molecular dynamics simulations to generate inpute files for vertical triplet energies for a selected number of frames. The code works with any trajectory file, however testing has been mainly performed using the MILO package developed by the Ess group which is interfaced with Guassian16. This workflow can be form of MD simulations such as force fields, semiempirical methods (e.g. GNF2-xTB) and Density Functional Theory (DFT) as well as other methods. Currenly benchmaking has only performed usign quasiclassical MD at the M06-2X/MIDI! level of theory and an empirical cutoff population is currenly only available for this specific level of thory. Any change in level of theory will require empirical determination of the population cutoff for triplet energy analysis. Following the instruction in the notebook, the necessary QM input files will be generated based on the ACME package. The code has been tested only for Gaussian16, but the ACME package (link) allows for generation of ORCA input files (please see ACME instructions manual). An overview of the necessary steps is described below:

1) Install Necessary Dependencies

     pip install [...]

## Dynamic Vertical Triplet Energy Processor (DvTEProc)

[Description]

## Example Workflow

1) Run the necessary quasiclassical molecular dynamics trajectories.
   
3) Generate QM input files using DvTEGen (see above for instructions)

5) Execute QM calculations on your local HPC resources

6) Analyse the data using DvTEProc (see bove for instructions) for triplet energy prediction and other visualizations
