# Advanced Visualizer for 3D Heliospheric Modeling

This visualization tool affords in-depth exploration/analysis of the 3D output of heliospheric models. The tool is hosted and run in a cloud environment, enabling multiple users rapid access to large volumes of data from any browser.

## Model Run Selection
Upon launching the H3lioviz application, the user is presented with a listing of available model runs (see image below), affording selection of the run of interest. Currently, results of SWPC's operational WSA-Enlil model runs are being automatically populated as they become available, in real time.

<img width="920" alt="H3lioviz_run_selector_example" src="https://github.com/user-attachments/assets/b5271dd6-1848-4c24-993e-e349d45a5ad6" />

The Run selection menu includes 7 key metadata values (model run timing info and the CME “cone” parameters) for each run, in addition to a “More info” button affording access to the full model output metadata listing, as needed. The key metadata consists of the following fields:

- **Time of run**: Describes the UTC time at which a given model run was executed.

- **Run id**: Specifies the model run id.

- **Time at 21.5Rs**: Lists the UTC time for each CME at 21.5 Solar Radii (the inner boundary of the Enlil model domain) included within a given model run. For runs with multiple CMEs, the values appear in a vertical list with the earliest CME first, in descending order.

- **Cone half angle**: Describes the angular half width of each CME with multiple CME values appearing as described above (earliest first).

- **Latitude**: Identifies the solar latitudinal center-point of each CME.

- **Longitude**: Identifies the solar longitudinal center-point of each CME.

- **Radial velocity**: Identifies the radial speed of the CME at the inner boundary of the Enlil domain.

Upon selection of the desired model run from the selection menu, clicking “SELECT” at the bottom right will close the selection menu and load the desired model results into the visualizer. Selecting “CANCEL” will close the menu and return the user to the visualizer interface. An overview of the visualizer is shown below.

## Visualizer Components
<img width="920" alt="Screenshot 2025-12-11 at 2 46 45 PM" src="https://github.com/user-attachments/assets/ee3cc8b2-90cc-4968-b9d1-1eb02ee51012" />


The visualizer's main Menu bar includes three links: **H3lioviz**, **Visualizer**, and **Documentation**. Selecting **H3lioviz** will direct the user to the utility's splash screen. The **Visualizer** option is illustrated in the above image. Finally, **Documentation** directs to the User documentation.

The Control bar immediately below the main Menu bar includes options to  **[Show/Hide] CONTROLS** (left) and **PLOTS** (right). A dropdown menu at center displays the model run time and the model run id associated with the currently selected model run, also affording selection of different model runs via the model run selection menu.

The main visualization interface displays the simulation time in the upper left corner, corresponding to the current position of the interactive time slider at the bottom of the visualization window. Immediately below this timestamp are displayed the CME cone parameters (i.e., the key metadata described in the model run selection section, above). For model runs including multiple CMEs, values are listed sequentially, with those associated with the earliest CME appearing first. The **Mouse zoom** option (top center) toggles optional zooming within the visualization window via mouse wheel. Finally, the "globe" icon at top right allows for quick switching between various predefined "Snap to view" options including: **Ecliptic**, **Meridional**, **Oblique**, and **RESET ZOOM**, as shown in the image below.

<img width="241" height="214" alt="Screenshot 2025-12-11 at 2 27 20 PM" src="https://github.com/user-attachments/assets/19c946a5-9b7f-45bf-bbda-54c740dc4b74" />

The current orientation of the reference frame (X: from Earth to the Sun, Y: perpendicular to the X and Y axes, and Z: aligned with the solar rotational axis) and several keyboard shortcut commands (allowing for enhanced perspective manipulation) are included at the bottom left of the visualization window.

Finally, at the very bottom of the interface window are the time controls. An interactive slider here allows for immediate manipulation of the time within the model's simulated timeframe. Min/max times are displayed at respective ends of the time slider, with the currently selected time (corresponding to the position of the slider) appearing centered over the "play" button. As its nature implies, the play button initiates animation of the visualization window contents. The user may freely select any point on the timeline to immediately move to the corresponding instant. Additionally, once the timeline has been activated by mouse selection, the arrow keys may subsequently be employed to advance/regress the current time.

Animations may also be exported as either sets of individual images or as mp4 movies. To do so, activate the "Save image sequence" button, complete the sequence of events you desire to be captured, and then select the appropriate download type (image set or mp4). Such animations may include any new images created, for example, when:

- playing through an interval of the timeline
- clicking on the timeline and using the right and left arrow keys (best to wait for render between clicks)
- selecting a sequence of distinct instants on the timeline
- rotating
- snapping
- zooming

Note that the video does not allow changing the image size, so it is not possible to resize (including opening/closing control panel) while recording an animation. As soon as any images have been created and saved for download, the "Saving images for download" button will pulse and a download icon will appear. When all desired images have been generated, pause any animation, and downloading may be initiated by clicking the download icon and selecting the desired type of download (i.e., a series of frames or as movie). Once a download type has been selected or "Saving image sequence" has been deactivated (toggled), the "Save image sequence" button will reset and be ready to record a new sequence once activated.

## Visualizer Controls
Selecting the **SHOW CONTROLS** menu from the top left of the interface will open the visualization controls. The controls panel consists of 4 sections:
- **Features**: Activation of miscellaneous informational enhancements relating to magnetic field connectivity and indication of satellite locations.
- **Slices**: Determination of relevant surface slices to visualize.
- **Surface**: Controls for rendering surfaces at specified threshold values of parameters of interest (e.g., indicative of CME volume/shock surface).
- **Color**: Controls for plotting parameters of interest on surfaces of interest and with specified color tables.

### Features
The **Features** Menu consists of the following options:
1. **Magnetic fieldlines**: Enables magnetic field lines (including polarity) visualization within the **Equatorial slice**. *Note, the **Equatorial slice** does not have to be selected in the **Slices** menu in order for this option to function*.
2. **Satellite fieldlines**: Enables visualization of magnetic fieldlines connecting the all satellites of interest (Earth & STEREO-A/B) to the inner boundary of the model domain. *Note that the **Satellites** option does not have to be concurrently active in order for this option to function.*
3. **Satellites**: Enables plotting of markers indicating the location of the STEREO spacecraft.

### Slices
The **Slices** Menu affords flexibility in determining which slices are of most interest to the user in their analysis of model run results. All slices selected for plotting will display the plasma parameters of interest selected via the **Colors** menu (see description below). The menu consists of the following options:

1. **Equatorial slice**: Enables plotting of the equatorial slice plane. Further options include specifying whether this plane is to be rendered as representing the Ecliptic or the Solar equatorial plane.
2. **Meridional slice**: Enables plotting of the meridional slice plane.
3. **Radial slice at 1AU**: Enables plotting of a surface at a fixed radial distance of 1AU. This surface can provide insight, for instance, into a CME's transverse extent as it transits the surface in the vicinity of the Earth (or other locations of interest).

### Surface
This menu provides functionality which supports the rendering of isosurfaces (surfaces defined by a fixed value of a given plasma parameter or derived quantity of interest). Opening this menu exposes the option to enable visualization of a **Surface contour by variable**. Activating this option further exposes control mechanisms to manipulate the rendered surface. Specifically, a dropdown **Contour variable** menu appears, affording selection of the variable of interest, complemented by an interactive slider embedded within the parameter range associated with that variable. The variables appearing in the dropdown menu consist of **Density** (scaled by r<sup>2</sup>), **Radial Velocity**, and **Ram Pressure** (scaled by r<sup>2</sup>). An additional **MORE OPTIONS...** entry provides access to supplemental variables including **TEMPERATURE**, **Br** (the radial magnetic field), and **CME tracer** (an artificial, massless fluid inserted as a "marker" into the injected CME volume at the inner boundary). Upon selection of the variable of interest, the slider may be freely adjusted (or the arrow keys used) to step up and down the slider to select the desired value.

This feature is particularly useful in analyzing the 3-dimensional structure of CMEs and plasma streams (for instance) within the solar wind. It should be noted that, if the **Color variable** selected from the **Color** menu (described below) is chosen such that it corresponds to the **Contour variable** selected within the **Surface** menu, the color of the rendered isosurface will indeed match the color contours within any **Slices** the surface intersects. Conversely, if the **Color variable** is set to a different variable than that selected for the **Contour variable**, the color distribution across the face of the isosurface will represent the values of that **Color variable** on the surface. This affords the ability to investigate, for instance, the radial flow (**Radial velocity** as **Color variable**) of the "CME shock surface" as indicated by **Ram pressure** (selected as **Contour variable**).

### Color
This menu supports selection of the **Color variable** (with available options corresponding to those described above in the **Surface** section) as well as the desired **Colormap**. Several **Colormaps** are provided with the **SWPC-default** corresponding to that used in SWPC's long-standing [WSA-Enlil product](https://www.swpc.noaa.gov/products/wsa-enlil-solar-wind-prediction). The **Color variable** selected here determines the variable which is plotted in any **Slices** or **Surfaces** and with the colors defined by the selected **Colormap**.

The **Opacity** slider sets an opacity gradient for the colors that represent the lower values to the higher values. For example, if the lower value on the slider is 50% and the higher value is 100%, the colors that represent the lowest values in the visualization will be 50% opaque and the highest values will be 100% (i.e., fully) opaque.

If you do not desire an opacity gradient, you can set each slider to the same value for a single opacity value.

Adjusting the opacity can help "see through" selected slices and surfaces.

## Timeseries Plots
Selecting the **SHOW PLOTS** menu from the top right of the interface will open the Plot timeseries datasets controls. By default, the model run timeseries data corresponding to the plasma density and solar wind speed at L1 are plotted (see image below).

<img width="903" alt="Screenshot 2025-12-11 at 7 34 56 PM" src="https://github.com/user-attachments/assets/93063eb8-2071-43f5-a95d-3af7f645333c" />

The timeseries plots are linked to the visualizer timeline (in the left pane). Note the synced behavior: as the crosshairs in the plots (right pane) or in the timeline player in the visualizer (left pane), follow the mouse, the crosshairs in the complementary pane do as well. Selecting a time of interest in a plot immediately renders the corresponding image in the visualizer, and vice versa.

Plots may be added, removed, or rearranged. Check the Show legend cards box to display full-featured legend cards and be able to arrange datasets by dragging and dropping them in new plots or overplotting in existing plots.

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
