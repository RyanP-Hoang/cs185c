In this project, I will investigate the effects of the 1998-2001 La Niña event on ocean temperatures and wind patterns along the coast of Japan. In particular, I will explore the following science question:

How did the 1998-2001 La Niña event influence ocean temperature and wind-driven upwelling in the waters surrounding Japan?

To investigate this question, I will construct a model that spans the island nation of Japan and includes the surrounding Kuroshio and Oyashio currents. I will run simulations from the year 1998 to 2001, which was characterized by significant La Niña conditions. The experiment will include two runs: one with the observed wind patterns of 1998-2001 and one without wind conditions. I anticipate that the La Niña-influenced winds will lead to changes in the intensity of upwelling and result in cooler surface temperatures compared to the neutral scenario, due to stronger wind-driven mixing and upwelling of deeper, colder water.

For initial conditions, I will use the state of the ECCO Version 5 Model in January 1998. Boundary and external forcing conditions will also be derived from ECCO Version 5 outputs. To analyze the results, I will create a timeseries of temperature changes along the coast and evaluate the differences between the two models over time. Additionally, I will visualize the temperature anomalies and wind patterns through movies, and compare between the one with wind and without wind.

### Step 1: Create the Model Files
Several input files need to be created to run the model. Generate the following list of files using the notebooks indicated in paratheses:
- Model Grid (notebooks/Grid by Ryan Hoang.ipynb)
- Bathymetry (notebooks/Bathymetry by Ryan Hoang.ipynb)
- Initial Conditions (notebooks/Initial Conditions by Ryan Hoang.ipynb)
- External Forcing Conditions (notebooks/External Forcing Conditions by Ryan Hoang.ipynb)
- Boundary Conditions (notebooks/Boundary Conditions by Ryan Hoang.ipynb)
The model files should be placed into the  `input` directory.

### Step 2: Add files to the computing cluster
Once the input files have been created, the model files can be transferred to the computing cluster. Begin by cloning a copy of [MITgcm](https://github.com/MITgcm/MITgcm) into your scratch directory and make a folder for the configuration, .e.g.
```
mkdir MITgcm/configurations/cs185c_project
```
Then, use the `scp` command to send the `code`, `input`, and `namelist` directories to your configuration directory. 

### Step 3: Compile the model
Once all of the files are on the computing cluster, the model can be compiled. Make a `build` directory in the configuration directory and run the following lines:
```
../../../tools/genmake2 -of ../../../tools/build_options/darwin_amd64_gfortran -mods ../code -mpi
make depend
make
```

### Step 4.1: Run the model with wind
After the compilation is complete, run the model with the wind. Move to the run directory, link everything from `input` and `code`, and the submit the job script:
```
sbatch cs185c.slm
```

### Step 4.2: Run the model without wind
Next, run the model without wind to complete the experiment. Again, link everything from `input` and `code` to a directory called `run_no_wind`. Then, edit the `data.exf` file to point to the modified wind files (see the External Forcing Conditions by Ryan Hoang.ipynb notebook for details). Then, submit the job script again to rerun the model.

### Step 5: Analyze the Results
There are two notebooks provided for analysis:
1. Analyzing Model Results

   This notebook is provided to have a quick look at spatial and temporal variations in the temperature field in the model with wind. It also generates the visualization provided in the figures directory.
   
2. Answering the Science Question
   
   This notebooks provided some analysis plot to address the science question posed above.
