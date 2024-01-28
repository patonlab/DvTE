# Dynamic Vertical Triplet Energies (DvTE) Generation and Processing

<div align="center">
  <img src="./DvTE.png" alt="Description" width="800">
</div>

[Under Development]

## Synopsis:

Workflow and protocol for recording dynamic vertical triplet energies (DvTEs) based on the following preprint (Link).

The code is based on two main packages:

Dynamic Vertical Triplet Energy Generation (DvTEGen) which prepares input files for quantum mechanical (QM) calculations from input molecular dynamics (MD) trajectory files.

Dynamic Vertical Triplet Energy Processor (DvTEProc) which analyses the output QM files to provide predictions of molecular triplet energies.

The code is currently designed to work with the Gaussian16 environment, with plans for integration with other QM packages such as ORCA and QChem. Currently, the user is required to provide dynamic trajectories and execute the QM calculations separately; however, future plans include the development of a complete automated workflow for the UNIX environment.

## Dynamic Vertical Triplet Energy Generation (DvTEGen)

Description: This Jupyter Notebook processes the inputted quasiclassical molecular dynamics simulations to generate input files for vertical triplet energy calculations, using a selected number of frames.

Instructions:

1) Files Preparation:
Before initiating the code, the necessary quasiclassical MD trajectories need to be computed. The code works with any trajectory file, however, testing has been primarily performed using the MILO package developed by the Ess group (https://github.com/DanielEss-lab/milo) which is interfaced with Gaussian16. This workflow can be in the form of MD simulations such as force fields, semiempirical methods (e.g., GFN2-xTB), and Density Functional Theory (DFT), as well as other methods. Currently, benchmarking has only been performed using quasiclassical MD at the M06-2X/MIDI! level of theory, which we recommend for use.

Recommendations based on current available benchmarking:

```
Package: MILO
Level of theory: M06-2X/MIDI! (inclusion of implict solvation is optional)
No of trajectories: 25
Trajectory lenght: 1000 fs
Trajectory timestep: 1 fs
```

A set of example trajectory files generated using MILO can be found in the folder /Example_Trajectories.

Note: The dynamics should be performed on the ground state surface (i.e., S0, multiplicity = 1).

2) Install Necessary Dependencies

```bash
$ pip install acme
```
3) Download and open the Jupyter notebook in the working directory containing all the trajectory files.

```bash
$ jupyter notebook DvTEGen.ipynb
```
Note: Ensure that the correct Conda environment with the necessary dependencies is activated prior to executing the notebook.

4) Execute the contents of the notebook.
   
Note: The code has been tested only for Gaussian16, but the AQME package (link) allows for the generation of ORCA input files (please see the ACME instructions manual). Parameters for the file preparations are set by default based on our recommendations; however, these can be easily changed in the "Define Parameters for QM input file generation" cell. Currently, the triplet energy predictions have been benchmarked for the default settings. Any changes in basis set and functional will require empirical determination of the population cutoff (see DvTEProc for details) for accurate predictions of triplet energies.

Current Recommendations:
```
#Step Number for Coordinate Extraction
step_size = 8 #Step size for trajectory sampling (Default = 8)
i_step = 1 #First Step in the sampled trajectories (Default = 1)
f_step = 1000 #Final Step in the sampled trajectories (Default = 1000)

#QM inputs
qm_input='m062x/6-31G* scf=xqc' #Level of theory for vertical Triplet Enegy calculations
program='gaussian' #Program used for QM calculations (Options: gaussian and orca)
mem='64GB' #Memory used (See AQME specifications)
nprocs=32 #Number of processors (See AQME specifications)
```

5) Congratulations, all your QM input files have been generated and can be submitted for calculations on your HPC resources.

## Dynamic Vertical Triplet Energy Processor (DvTEProc)

Description: This Jupyter Notebook processes the QM output files and performs the data analysis to provide a prediction of triplet energy for the given molecular system. The code follows the following steps:

  a) Extract electronic energies from QM files and compile them as a .csv document.
  b) Fit a normal distribution to the compiled data.
  c) Construct a cumulative distribution function using the mean and standard deviation of the fitted normal distribution.
  d) Generate graphics and Quartile-Quartile plots to analyze the data.
  e) Provide a prediction of triplet energy based on the selected population cutoff using the CDF.

Instructions:

1) File Preparations:

Ensure that all QM output files are compiled in one folder for each individual molecule to be analyzed.

2) Install Necessary Dependencies

```bash
$ pip install pandas
$ pip install numpy
$ pip install scipy
$ pip install sklearn
```

3) Download and open the jupyter notebook

```bash
$ jupyter notebook DvTEGen.ipynb
```
Note: Ensure that the correct Conda environment with the necessary dependencies is activated prior to executing the notebook.

4) Execute the contents of the notebook.
   
  a) Provide the Path(s) and structure name(s) of the files to be analyzed.
  b) Select a population for which a predicted triplet energy will be determined.

NOTE: As mentioned previously, this value is empirically determined and currently, the value of 0.008 performs best using the M06-2X/6-31G(d)//M06-2X/MIDI! level of theory.

5) Congratulations, you now have a prediction for the triplet energy for your chosen system(s).


## Example Workflow

1) Run the necessary quasiclassical molecular dynamics trajectories.
2) Generate QM input files using DvTEGen (see above for instructions).
3) Execute QM calculations on your local HPC resources.
4) Analyze the data using DvTEProc (see above for instructions) for triplet energy prediction and other visualizations.
   
## (Re)Benchmarking set

The compiled DvTEs dataset of 20 molecules reported in the preprint (link) at the M06-2X/6-31G(d)//M06-2X/MIDI! is available in the /Benchmark folder, together with an additional notebook called Dynamic Vertical Triplet Energy Benchmarking (DvTEBench). This code utilizes the compiled .csv dataset of vertical triplet energies generated using DvTEProc (i.e., {MoleculeName}_output.csv) and calculates predicted triplet energies using a range of populations starting from 0.001 to 0.050 in steps of 0.001. The code then compares different models against experimentally determined triplet energy values and reports the best population to be used for future predictions. Additionally, the code can also compare the performance of Gaussian Mixture Models (GMMs) instead of simple normal distributions.

This set can be utilized to benchmark other levels of theory and different flavors of MD simulations (e.g., force fields, semi-empirical, ML-potentials) for the determination of the population cutoff. If you have benchmarking data with any additional level of theory, please reach out and we will include it in the list below.

Currently available benchmarking data:
```
M06-2X/6-31G(d)//M06-2X/MIDI! - (quasiclassical MD) : population = 0.008
```

## References:
TBA

