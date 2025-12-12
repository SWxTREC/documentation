# Next Generation 3D Solar Wind Interactive Data Visualizations

This visualization tool allows interaction with the 3D output of solar wind models. The model is hosted and run in a cloud environment, enabling multiple users rapid access to large volumes of data from any browser.

## Select a model run
Enlil model runs by SWPC are currently being automatically ingested as soon as they become available.

Select a model run by clicking on its row and clicking SELECT.

To select a new model run, open the model run table by clicking on the model run title at the top of the visualization.

If there are multiple values for the CME metadata in the table that means the run includes multiple CMEs.

**Time at 21.5R**: Time when CME leaves the Sun.

**Cone half angle**: The width of the CME as input to the model run.

**Latitude**: The latitude of the CME as input to the model run.

**Longitude**: The longitude of the CME as input to the model run.

**Radial Velocity**: The radial velocity of the CME as input to the model run.

## Mouse zoom
Toggle whether you want to be able to zoom in and out with the mouse.

## Orientation menu (globe)
**Ecliptic** Snap to view the ecliptic plane from above.

**Meridional** Snap to view the meridional plane from the side.

**Oblique** Snap to view from an oblique angle.

**Reset zoom** Click to reset to the default zoom.

## Axes
**X** The axis perpendicular to the plane made by the Y and Z axes.

**Y** The Sun to Earth line.

**Z** The axis from north pole to the south pole on the Sun.

## Time player
The time player along the bottom of the visualizer shows which timestep is being displayed. You can click anywhere along the timeline to see the corresponding image. Once you have clicked the selected timeplayer timestep, you can use the right and left arrows to go forward and backwards along the timeline.

Press the Play button to automatically play through the event.

Press the Pause button or click anywhere on the timeline to stop the playing.

### Capturing image sequences for download
To save a sequence of images to download as a set of images or an mp4 movie, click the "Capture image sequence" button.

An image sequence includes any new image created when:
- playing through the timeline
- clicking on the timeline and using the right and left arrow keys (best to wait for render between clicks)
- clicking on different places on the timeline
- rotating
- snaping
- zooming

The video does not allow changing the image size, so you can't resize while recording and then download a video.

Once you have recorded your image sequence, click stop.

Images saved for download can be downloaded by clicking the download icon and selecting either a series of frames/images or a movie.

## Features

**Magnetic fieldlines** Magnetic field lines in the solar wind model that show the structure and connectivity of the Sun's magnetic field throughout the heliosphere.

**Satellite fieldlines** Magnetic field lines that extend from the Sun to the satellite (object orbiting the Sun) in question.

**Satellites** Objects orbiting the Sun. Currently this includes: STEREO A, STEREO B, and Earth.

## Slices

**Equatorial slice** There are two options to select from:

&nbsp;&nbsp;&nbsp;&nbsp;**Solar equator** A plane through the solar equator.

&nbsp;&nbsp;&nbsp;&nbsp;**Ecliptic** A plane from the center of the Sun through the orbit of the Earth.

**Meridional slice**
A plane perpendicular to the solar equator.

**Radial slice at 1AU**
A radial surface at 1 Astronomical Unit from the Sun (approximately the distance from the Sun to the Earth).

## Surface

Create a surface based on the value of a variable.

The surface is the 3D rendering of the colors on the 2D slices.

You can use the colors in the slices to target the relevant value of the selected surface. For example, select the ecliptic and meridional slices to make them visible. Color them by the relevant variable. You might see a shape or a "shock" around a CME in the planes. To view a 3D rendering, set the surface variable to the same variable and select the value that corresponds to the color of the shock you desire. You can then turn off the slices to view the selected 3D surface alone.

You can drag the button on the slider to change the value of the surface or use the arrow keys to step up and down the slider.

### Density
### Radial velocity
### Ram pressure
Dynamic pressure
### Temperature
### Br
### CME tracer


## Color

The variable to use to color all the slices and surfaces. The value of the variable will be displayed as the corresponding color in the selected colormap.

The color variable along slices will vary.

If the color variable is the same as the surface variable, the surface will have a single color since the value of the surface is, by definition, constant.

If the color variable is different from the surface variable, the surface will share the same colormap as the slices and will vary. The values shown in the color bar are the color variable and do not correspond to the selected surface value.

### Density
### Radial velocity
### Ram pressure
Dynamic pressure
### Temperature
### Br
Use "Divergent" or "Cool to warm" scales with the variable since it can have both positive and negative values.
### CME tracer

### SWPC default colormap
The custom color scale seen on the traditional Enlil product produced by SWPC here: [SWPC Enlil](https://www.swpc.noaa.gov/products/wsa-enlil-solar-wind-prediction). This color scale is good at clearly showing a wide range of values, so it best set to cover the entire available range.

### Opacity slider
This slider sets an opacity gradient for the colors that represent the lower values to the higher values. For example, if the lower value on the slider is 50% and the higher value is 100%, the colors that represent the lowest values in the visualization will be 50% opaque and the highest values will be 100%, or fully, opaque.

If you do not desire an opacity gradient, you can set each slider to the same value for a single opacity value.

Adjusting the opacity can help "see through" selected slices and surfaces.

## Plots
The timeseries plots are linked to the visualizer timeline. You will see corresponding crosshairs across the plots and the time player as you hover and move the mouse. If you click on a time of interest in a plot, the corresponding image will render in the visualizer.

You can add plots, remove plots, and rearrange plots.

Check the Show legend cards box to display full-featured legend cards and be able to arrange datasets by dragging and dropping them in new plots or overplotting in existing plots.

### Solar images
Select a time series of images of the sun.

### Model data at Earth
Display a time series of the values of the model as predicted at Earth.

This time might be in the future.

#### Density
#### Radial velocity
#### Temperature
#### Ram pressure

### Observed Data at L1
Display a time series of the real-time solar wind product from the ACE spacecraft at Lagrange point 1 (L1).

If the time of the event goes into the future—as predictive models are meant to do—there will not yet be real-time data at L1.

Observed plots are best used for evaluating how well the model predicted the event. Observed data is by definition in the past.

#### Density
#### Radial velocity
#### Temperature

