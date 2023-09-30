# Geoelectric Field Model

An estimate of the geoelectric field for the past 24-hours, updated every hour.

## Description

The real-time geoelectric field model produces estimates of the
geoelectric field over the past 24-hours across the United States of America.
It is a real-time implementation of the historical hazard analyses which
have been produced by the United States Geological Survey (USGS).

## Operational set up

The model requires the latest ground magnetic field data to produce a forecast. Which is downloaded every model run. The model runs **every 30 minutes past the hour**. The model has several calculation steps that are outlined below, but more
detail can be found in the associated references.

1. **Download magnetic field data from USGS observatories**
   We download 1-minute data covering the past 24-hours from
   the 9 observatories located in the contiguous US.

2. **Remove a linear trend line to remove the baseline offset**
   We are not interested in the main field, so we remove that to get a
   rough approximation of the geomagnetic
   disturbance field.

3. **Interpolate the observatory data onto a grid**
   We use the spherical elementary current system (SECS) method for
   this interpolation step. The [pysecs](https://github.com/greglucas/pysecs)
   Python package is used for these interpolations.

4. **Calculate the geoelectric field at all grid locations**
   We calculate the geoelectric field as a convolution of the
   magnetic field with magnetotelluric impedance at that grid point.
   We use the [bezpy](10.5281/zenodo.3765860) Python package for these
   calculations.

## Input Data

There are two input datasets required to calculate the estimated geoelectric fields: geomagnetic field data and magnetotelluric impedances.

1. **Geomagnetic field** data is provided by the [USGS Geomagnetism Group](https://geomag.usgs.gov)
   The data are accessed via [SWx TREC's Space Weather Data Portal](https://lasp.colorado.edu/space-weather-portal).

2. **Magnetotelluric impedances** are provided by the USGS on a gridded domain
   covering the United States. This gridded impedance dataset is generated through
   through an inverse process that regresses against the magnetotelluric
   survey data available within the domain.

The magnetotelluric impedances don't change very often, and are thus cached until
updates are made to that gridded model. The magnetic field data is downloaded every
single model run to get the latest data.

## Output Data

The model outputs both a gridded geomagnetic field and gridded geoelectric field
product. The geoelectric field is null where there is not any data to calculate
the solution, for example over the oceans.

We provide an API to obtain the latest model output at
<https://livegeoelectric-api.dev.swx-trec.com/livegeoelectric_model>.
The output data format is JSON and the structure is as follows.

```JSON
{"data": {
  "time": [...],
  "latitude": [...],
  "longitude": [...],
  "bh": [[[...], ...], ...],
  "eh": [[[...], ...], ...],
  "obs": [...]
  }
}
```

With `time`, `latitude`, and `longitude` containing 1D arrays of each
variable. The `bh` and `eh` are 3D arrays indexed by `[time][latitude][longitude]` corresponding to the grid of the respective 1D arrays.
The `obs` array contains the observatories that were used in this
model run to produce the predictions.

## References

```bibtex
Lucas, G., Love, J. J., Kelbert, A., Bedrosian, P. A., & Rigler, E. J. (2020).
A 100-year geoelectric hazard analysis for the U.S. high-voltage power grid.
Space Weather, 18, e2019SW002329.
https://doi.org/10.1029/2019SW002329
```

## Credits

**Greg Lucas:** Model creator and cloud storage solutions

**Anna Kelbert:** Gridded impedances

**Josh Rigler:** Magnetic field interpolations

**Brandon Stone:** Back-end software development

**Jennifer Knuth:** Front-end and visualization

We acknowledge support for this work from NASA grant 80NSSC20K1477
"Pushing the Frontiers of Operational Geoelectric Hazard Modeling".

## Contacts

Please contact Greg Lucas <greg.lucas@lasp.colorado.edu> with any questions.
