# Dst Model Description

## Overview
LiveDst is a machine learning (ML) model that predicts the Dst geomagnetic disturbance index in real time. The target for the model is the Real Time Dst value published by the World Data Center for Geomagnetism in Kyoto, Japan (Kyoto (https://wdc.kugi.kyoto-u.ac.jp/dstdir/). These Real Time values may be adjusted later to Quicklook, Provisional, or Final index values that differ slightly from the Real Time values used by the LiveDst model but are generally not available when the LiveDst mode is run.
 
LiveDst is run at 45 minutes past the hour and gives 1-, 2-, 3-, 4-, 5- and 6-hour predictions of the Real Time Dst index with quantified uncertainties that are valid at the top of the hour. For instance, the model run at 13:45 UT produces predictions that are valid for 14:00 UT and beyond. Only the 6-hour prediction is shown by default on the plot – to see the other plots go to “Add Plots” and select “LiveDst Model Runs” from the options. 
 
The model is based on multi-fidelity boosted neural networks (Hu, Camporeale, & Swiger, 2022), that ingest real-time data solar wind observed by ACE at the 1st Lagrangian point (https://www.swpc.noaa.gov/products/ace-real-time-solar-wind). In addition, the time history of Dst is used.
 

## Operational set up
The model requires the latest hourly Real Time Dst value from Kyoto to produce a forecast. However, that value is not immediately available at the top of an hour. Hence, the model runs **every 45 minutes past the hour**, checking to see if the Real Time Dst for that hour has been released from Kyoto. However, as in terrestrial weather forecasts, the forecast produced at 45 minutes past the hour is valid only for the top of the next hour and beyond. 


## Input Data
The following inputs are ingested by the neural networks: solar wind density, velocity, amplitude of Interplanetary Magnetic Field (IMF), z-component of IMF, IMF clock angle, Earth's dipole tilt angle, and Real Time Dst values. Solar wind quantities and IMF are taken in real-time from https://services.swpc.noaa.gov/text/ and the Dst index from the World Data Center for Geomagnetism, Kyoto (https://wdc.kugi.kyoto-u.ac.jp/dstdir/).
See the reference paper (Hu, Camporeale, Swiger, 2022) for details.


## Output Data
The model outputs predictions in terms of Gaussian distributions, where the **LiveDst prediction**, shown as a continuous line is the mean of the Gaussian distribution, and the shaded area is one standard deviation. In other words, the model predicts a 68% probability for Dst to lie within the shaded region.

In the default settings, the top panel shows the observed Real Time Dst for the past 24 hours, and the model predicted Dst for the future 6 hours (prediction are always made for the top of the hour), each shown with its confidence interval (one standard deviation).
However, the user can overlay predictions made with **different lead times** (t+1, t+2,... t+6 being 1, 2,...,6 hours ahead).
The timeseries labeled **Kyoto Data // Real Time Dst (nT)** shows the Dst (in units of nanoTesla) used as inputs and available at the time when the model was run. 

Finally, the Dst predicted from the U. Michigan Geospace model, run operationally at the NOAA Space Weather Prediction Center (https://www.swpc.noaa.gov/products/geospace-geomagnetic-activity-plot) can be shown, labeled as **Michigan Geospace V2 model results**. Note that that is not the official SWPC forecast, instead it is a model guidance which forecasters can use to assist them in generating the official forecast. Real-time outputs are obtained from https://nomads.ncep.noaa.gov/pub/data/nccf/com/swmf/prod/, while historical storms have been simulated offline by Qusai Al Shidi at the University of Michigan (those results have been reported in Al Shidi et al., 2022). The user can also display the Temerin & Li Dst prediction (Temerin & Li, 2002).


<!--
### File Structure
Each hourly model run is stored in a separate NetCDF file. All times are in UTC.

**Coordinates:**
* `model_time` - Base time for the model run (top-of-hour; e.g. `2022-11-07T17:00:00`)
* `time` - Time tags for the output data points (e.g. `2022-11-07T18:00:00`)
* `calibration` - Calibration file key names (e.g. `'mean_std_delay1'`)
* `inputs` - Input dataset key names (e.g. `'dst'`)
* `models` - Sub-models that this model depended on (N/A)

**Data variables:**
* `dst` (time, model_time) - Predicted Dst value (e.g. `-94.86`) or input Dst (delta=`00:00:00`)
* `stddev` (time, model_time) - Standard deviation (e.g. `6.487`) or `0.0` if input Dst
* `delta` (time) - Time offset from model_time (e.g. `01:00:00`)
* `calibration_files` (calibration) - Calibration files used (e.g. `'mean_std_1_-90_6.h5'`)
* `input_files` (inputs, model_time) - Input files used / created (e.g.
    `'SpaceWeatherPortal_kyoto_dst_index_service_20221107T050000_27bbeacf_527bc3236f27.nc'`)
* `model_files` (models, model_time) - Sub-model output files used (N/A)
* `creation_time` (model_time) - File create time (e.g. `2022-11-15T21:34:54.573102`)
* `status` (model_time) - Model run quality flag (e.g. `16706` for generated new local output file)

**Attributes:**
* `name` - Name of the model (i.e. `DstModel`)
* `version` - Version of the model (e.g. `v0.0.2`)
* `frequency` - Frequency model output is generated at (e.g. `H` for hourly)
* `args_json` - Model configuration (e.g. `{"npredictions": 6, "boost_num": 6, "criteria": "resi_std...`)
* `status_string` - String representation of the model `status`
    (e.g. `WRITE_PASS|RECOVER_SKIP|GENERATE_PASS|EXISTING_NONE`)
* `model_run_tag` - Unique identifier appended to all input and output files associated with this model run
    (e.g. `1b75a5f048da`)


Example of a file opened and printed to console using the [Xarray](https://docs.xarray.dev/en/stable/index.html)
 Python library:
```text
Dimensions:            (model_time: 1, calibration: 90, inputs: 3, models: 0, time: 6)
Coordinates:
  * model_time         (model_time) datetime64[ns] 2022-11-07T17:00:00
  * inputs             (inputs) <U10 'dst' 'ace_mag' 'ace_plasma'
  * calibration        (calibration) <U27 'mean_std_delay1' 'param_std_per_delay1' ... 'param_dst_delay6_boost5'
  * models             (models) <U32
  * time               (time) datetime64[ns] 2022-11-07T18:00:00 2022-11-07T19:00:00 ... 2022-11-07T23:00:00
Data variables:
    status             (model_time) uint64 16706
    calibration_files  (calibration) <U37 'mean_std_1_-90_6.h5' ... 'params_new_6--90-49-5resi_std.pt'
    input_files        (inputs, model_time) <U83 'SpaceWeatherPortal_kyoto_dst_index_service_20221107T050000_27bbeacf...
    model_files        (models, model_time) <U32
    creation_time      (model_time) datetime64[ns] 2022-11-15T22:09:29.247773
    dst                (time, model_time) float64 -94.86 -102.9 -104.4 -105.1 -105.3 -105.5
    stddev             (time, model_time) float32 6.487 7.32 7.478 7.946 9.661 9.021
    delta              (time) timedelta64[ns] 01:00:00 02:00:00 03:00:00 04:00:00 05:00:00 06:00:00
Attributes:
    name:           DstModel
    version:        v0.0.2
    frequency:      H
    args_json:      {"npredictions": 6, "boost_num": 6, "criteria": "resi_std", "boost_method": "linear"}
    status_string:  WRITE_PASS|RECOVER_SKIP|GENERATE_PASS|EXISTING_NONE
    model_run_tag:  527bc3236f27
```

**File naming pattern:**
* `DstModel` - Model name
* `v0.0.2` - Model version
* `20031130T230000` - Model run time (top-of-hour; UTC)
* `1H` - Model run frequency
* `7d79096db134` - Unique model run identifier

Example: `DstModel_v0.0.2_20031130T230000_1H_7d79096db134.nc`

!-->
## References
A. Hu, E. Camporeale, B. Swiger (2022) **Multi-Hour Ahead Dst Index Prediction Using Multi-Fidelity Boosted Neural Networks**, Space Weather, 21, 4,  https://doi.org/10.1029/2022SW003286

Al Shidi, Q., Pulkkinen, T., Toth, G., Brenner, A., Zou, S., & Gjerloev, J. (2022). **A Large Simulation Set of Geomagnetic Storms–Can Simulations Predict Ground Magnetometer Station Observations of Magnetic Field Perturbations?**, *Space Weather*, https://doi.org/10.1029/2022SW003049

Temerin, M. & Li, X., (2002). **A new model for the prediction of Dst  on the basis of the solar wind**, *JGR Space Physics*, 107, A12, https://doi.org/10.1029/2001JA007532

## Credits
Enrico Camporeale: original idea and project supervision

Andong Hu: implementation and training of machine learning models

Brandon Stone: back-end software development

Jennifer Knuth: front-end and visualization

Greg Lucas: cloud storage solutions

Tom Berger: forecasting conops development

We acknowledge support for this work from NASA grant 80NSSC20K1580.

## Contacts
Please contact Enrico Camporeale (enrico.camporeale@colorado.edu) for any questions.

#### Disclaimer
The forecast presented on this webpage is a research product and is provided to the public on an "as is" basis with no guarantees of completeness, accuracy, usefulness or timeliness.
