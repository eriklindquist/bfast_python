#bfastmonitor_gpu

This is a repo with work originally done by Derek Van de Ven and available here: DerekvdVen/bfastmonitor_GPU_SEPAL
However, it is envisaged that this current repo will be actively maintained and updated. 

This github repository contains scripts for using the python bfast algorithm in SEPAL. 

NOTEBOOKS
- develop_rasterio_test.ipynb
    Run BFAST with either python or opencl backends using rasterio functions for reading and writing rasters

#### These are not working at the moment ####
- bfastmonitor_GPU_stack.ipynb 
    If you want to run over a big data set in one go, you may run this code on a timeseries data set. 
- bfastmonitor_GPU.ipynb
    This is a script for running over SEPAL time series tile directories within a time-series folder. 

#### This is also not working at the moment ####   
FROM TERMINAL
- bfastmonitor_GPU_stack.py -o [output_dir] -t [timeseries_dir]
    You can run bfast_stack.py from the terminal, the terminal will prompt the user for parameters.
        example: python3 bfast_stack.py -o Guyana -t ../../downloads/Time_series_2020-09-09_13-02-40/
        example: python3 bfast_stack.py -o Australia -t /home/dven/downloads/Time_series_2020-09-09_13-02-40/
- bfastmonitor_GPU_array.sh
    If you want to run bfastmonitor-GPU over folders in different folder locations, do multiple runs to test parameters etc. you may use this bash script. It calls bfastmonitor_GPU_stack_bash.py using parameters in bash arrays. 
- bfastmonitor_GPU_stack_bash.py
    Is called by bfastmonitor_GPU_array.sh.


PYTHON FUNCTIONS
- functions.py
    Contains general functions.
- plotting_funcs.py
    Contains functions for plotting. 
- time_series.py
    Contains the Timeseries Class.
- widgets.py
    Contains the ipy widgets used in the notebooks. 

TIF OUTPUTS
The scripts provide the following tif outputs

- stored_time_series/[name of input]/[number of tile]/bfast_outputs.tif
    This is a 2-band raster with Band 1 containing breakpoints in decimal year format. Band 2 contains magnitude. Raster is same width/height as original raster.

#### At the moment, none of these other outputs are produced
- breaks_indexed
    Indexes of the breaks, base output of bfastmonitor_GPU. -1 denotes no break is found. -2 denotes absence of enough data to find breaks.
- breaks_binary
    Presence of all breaks in 0 or 1.
- breaks_binary_negative
    Presence of negative breaks 0 or 1.
- breaks_julian
    Julian dates of breaks.
- breaks_julian_negative
    Julian dates of negative breaks.
- magnitudes
    All means of MOSUM process (deviation between model and data) floats.
- magnitudes_negative
    Negative means of MOSUM process (deviation between model and data) floats.
- magnitudes_classified_result
    COLORED Means of MOSUM process classified into 10 classes -999(no data), 1,2,3,4,5,6,7,8,9


    # 1 = no change (mean +/- 1 standard deviation)
    # 2 = negative small magnitude change      (mean - 2 standard deviations)
    # 3 = negative medium magnitude change     (mean - 3 standard deviations)
    # 4 = negative large magnitude change      (mean - 4 standard deviations)
    # 5 = negative very large magnitude change (mean - 4+ standard deviations)
    # 6 = postive small magnitude change       (mean + 2 standard deviations)
    # 7 = postive medium magnitude change      (mean + 3 standard deviations)
    # 8 = postive large magnitude change       (mean + 4 standard deviations)
    # 9 = postive very large magnitude change  (mean + 4+ standard deviations)

- magnitudes_classified
    Same as above, but not colored
