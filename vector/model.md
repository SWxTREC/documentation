# VECTOR (Vehicle Environment Coupling and TrajectOry Response)

## Overview

The VECTOR code is publicly available on our [GitHub repository](https://github.com/SWxTREC/vector). VECTOR uses the Semi-Empirical Satellite Accommodation coefficient Model
(SESAM) to calculate the coefficient of drag, projected area,
and force coefficient from a given set of input parameters.
The code was developed by Marcin Pilinski and the theoretical framework
for this is written up in his [thesis](https://pdfs.semanticscholar.org/912d/411295e005da3a531bf5c0fb03b749f48461.pdf).

## API

The VECTOR model can be accessed through a programmatic interface to get
results without needing to install the program locally. There are three
endpoints that are used to interact with the backend.

`/geometry/<sessionId>` : PUT
    Upload a `WRL` geometry file of the spacecraft, associated with the
    given `<sessionId>`.

`/singlepoint` : POST
    Receives the json data from the frontend website and makes
    the call to the VECTOR model to produce the output results.
    It returns a json dictionary of the calculated values.

`/image/<sessionId>` : GET
    Returns the image that was produced by the geometry file uploaded and
    the orientation input during the last singlepoint request. It
    must have an associated `<sessionId>` which returns the saved image file
    for that user.

## Model Inputs

The following model inputs can be used to modify the vehicle and environment
settings for the model runs. The type and description of each input follows.

**objectType**: string

`cylinder, sphere, plate, cubesat1u, deployable3u, sorce, custom`

![Objects](https://raw.githubusercontent.com/SWxTREC/vector-code/master/docs/vector_objects.png)

The named satellites available are:

- `sorce`, the SORCE satellite
- `cubesat1u`, a 1U CubeSat
- `deployable3u`, a 3U CubeSat with solar panels

**diameter**: float

`The diameter of the object [m], must be positive`

**length**: float

`The length of the object [m], must be positive`

**area**: float

`The area of the object [m^2], must be positive`

**pitch**: float

`Pitch angle of the object [deg], must be between -90 and 90`

**sideslip**: float

`Sideslip angle of the object [deg], must be between -180 and 180`

**temperature**: float

`Ambient temperature of the atmosphere [K], must be positive`

**speed**: float

`Speed of the object [m/s], must be positive`

**composition**: dictionary

```text
Number density composition of atmospheric constituents [/m3], must be positive


O: float

O2: float

N2: float

He: float

H: float
```

**accommodationModel**: string

`SESAM, Goodman, Fixed`

**surfaceMass**: float

`Surface mass of the object [amu], must be 1 or greater`

**energyAccommodation**: float

`Energy accommodation value for the object [-], must be between 0 and 1`

**sessionId**: string

`A random session id to use for each unique user, must start with "id-"`

### Example Input Payload

```json
{
"objectType": "sphere",
"diameter": 1.212,
"length": 2.5,
"area": 0,
"pitch": 30,
"sideslip": 0,
"temperature": 1200.5,
"speed": 7800.45,
"composition": {"o": 1e11,
                "o2": 1e6,
                "n2": 1e6,
                "he": 1e6,
                "h": 1e4},
"accommodationModel": "SESAM",
"energyAccommodation": 0.93,
"surfaceMass": 65,
"sessionId": "id-1696259637843"
}
```

## Model Outputs

There are 4 model outputs, the drag coefficient, projected area, force coefficient, and energy accomodation coefficient.

**dragCoefficient**: float

`The coefficient of drag of the object [-]`

**projectedArea**: float

`The projected area of the object [m2]`

**forceCoefficent**: float

`The force coefficient of the object [m2]`

**energyAccomodation**: float

`The energy accomodation of the object [-]`

### Example Output Payload

```json
{
"dragCoefficient": 2.7965,
"projectedArea": 1.1537,
"forceCoefficient": 3.2264,
"energyAccommodation": 0.3895
}
```

## References

```bibtex
Pilinski, M. D. (2011). Dynamic Gas-Surface Interaction Modeling for Satellite Aerodynamic Computations.
https://api.semanticscholar.org/CorpusID:111622277
```

## Credits

Marcin Pilisnki: author of VECTOR

Jennifer Knuth: front-end and visualization

Greg Lucas: backend model support and cloud solutions

## Contacts

Please contact Marcin Pilinski <marcin.pilinski@lasp.colorado.edu> for any questions.
