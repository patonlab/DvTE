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

Description: This Jupyter Notebook proceses the inputed quasicaliscal molecular dynamics simulations to generate inpute files for vertical triplet energies for a selected number of frames using the ACME package (link).

Instructions:

1) Files Preparation:

Before intiating the code, the necessary quasiclasical MD trajecotries need to be computed. The code works with any trajectory file, however testing has been mainly performed using the MILO package developed by the Ess group (link) which is interfaced with Guassian16. This workflow can be form of MD simulations such as force fields, semiempirical methods (e.g. GNF2-xTB) and Density Functional Theory (DFT) as well as other methods. Currenly benchmaking has only performed usign quasiclassical MD at the M06-2X/MIDI! level of theory which we recommmend for use.

Recommendations based on current available benchmarkig:

```
Package: MILO
Level of theory: M06-2X/MIDI! (inclusion of implict solvation is optional)
No of trajectories: 25
Trajectory lenght: 1000 fs
Trajectory timestep: 1 fs
```

A set of example trajectory files generated using MILO can be found in the folder /Example_Trajectories

Note: the dynamics should be performed on the ground state surface (i.e. S0, multiplicity = 1)

2) Install Necessary Dependencies

```bash
$ pip install acme
```
3) Download and open the jupyter notebook in working directory containing the all the trajectory files

```bash
$ jupyter notebook DvTEGen.ipynb
```
Note: Ensure that the corect Conda environment with the necessary dependencies is opened before the notebook is opened

4) Execute the contents of the notebook

Note: The code has been tested only for Gaussian16, but the ACME package (link) allows for generation of ORCA input files (please see ACME instructions manual). Parameter for the file preparations are set by default based on our recommendations, however these can be easily changed in the "Define Parameters for QM input file generation" cell. Currently, the triplet energy predictions has been benchmarked for the default desttings. Any changes in basis set and functional will require empirical determination of the population cutoff (see DcTEProc for details) for accurate predictions of triplet energies.

Current Recommendations:
```
#Step Number for Coordinate Extraction
step_size = 8 #Step size for trajectory sampling (Default = 8)
i_step = 1 #First Step in the sampled trajectories (Default = 1)
f_step = 1000 #Final Step in the sampled trajectories (Default = 1000)
#QM inputs
qm_input='m062x/6-31G* scf=xqc' #Level of theory for vertical Triplet Enegy calculations
program='gaussian' #Program used for QM calculations (Options: gaussian and orca)
mem='64GB' #Memory used (See ACME specifications)
nprocs=32 #Number of processors (See ACME specifications)
```

5) Congratulations, all your QM input files have been generated and can be submitted for calculations on your HPC resources

## Dynamic Vertical Triplet Energy Processor (DvTEProc)

[Description]

## Example Workflow

1) Run the necessary quasiclassical molecular dynamics trajectories.
   
3) Generate QM input files using DvTEGen (see above for instructions)

5) Execute QM calculations on your local HPC resources

6) Analyse the data using DvTEProc (see bove for instructions) for triplet energy prediction and other visualizations
