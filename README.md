# Dynamic Vertical Triplet Energies (DvTE) Generation and Processign

<div align="center">
  <img src="./DvTE.png" alt="Description" width="300">
</div>

[Under Development]

## Synopsis:

Workflow and protocol for recording dynamic vertical triplet energies (DvTEs) based on the following pre-print (Link).

The code is based on two main packages: Dynamic Vertical Triplet Energy Generation (DvTEGen) which prepares input files for quantum mechanical (QM) calculations from input trajectory files, and Dynamic Vertical Triplet Energies Processor (DvTEProc) which analyses the output QM files to provide a prediction of molecular triplet energies.

The code is currently designed to work with the Gaussian16 environment with plans for integration with other QM packages such as ORCA and QChem. Currently the user is require to provide dynamic trajectories and execute separately the QM calculations, however future plans include development of a complete automated workflow for the UNIX environment.

## Dynamic Vertical Triplet Energy Generation (DvTEGen)

[Description]

## Dynamic Vertical Triplet Energy Processor (DvTEProc)

[Description]

## Example Workflow

1) Run the necessary quasiclassical molecular dynamics trajectories.
       Code has been deveoped mainly for use with MILO, however any trajectory file is compatible. Currenetly, MILO and JProgDyn have confirmed to be supported.
       Recommendations: 25 Trajectories, 1000 fs simulation lenght, 1 fs times step
   
3) Generate QM input files using DvTEGen (see above for instructions)

4) Execute QM calculations on your local HPC resources

5) Analyse the data using DvTEProc (see bove for instructions) for triplet energy prediction and other visualizations
