## kOmegaSST turbulence model with curvature correction for OpenFOAM



## Description
OpenFOAM implementation for the incompressible kOmegaSST model including rotation/curvature correction for the komegaSST turbulence model. This is based on https://github.com/ancolli/kOmegaSSTCC which was based on 
https://github.com/cvillescas/TkOmegaSSTCC. This was necessary du to the merging of momentumTransport and turbulenceModels to momentumTransportModels with openFOAM version 8. 
The code is tested with OpenFOAM 10. This (repository) code is not part of the official OpenFOAM distribution.

> **CAUTION!: The implementation has not yet been tested in detail. This note will be removed after detailed review.**


## Requirements

- git
- openfoam10 (tested) (www.openfoam.org)


## Usage (Linux)

1. Load the openfoam environment (if not set within bashrc)

2. Download repo i.e. `git clone ...`

3. Switch to this folder.

4. From this folder copy files:

```
cp -r ./src $WM_PROJECT_USER_DIR
```

5. Switch folder using: `cd $WM_PROJECT_USER_DIR/src/MomentumTransportModels/incompressible`

6. run `wmake`

7. Include follwoing line at the end of your case's `system/controlDict`

```
...

libs
(
    "libuserincompressibleMomentumTransportModels.so"
); 
```

8. You should now be able to use the `kOmegaSSTCC` model within your case's `const/momentumTransport` file:

```
/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  10
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    format      ascii;
    class       dictionary;
    location    "constant";
    object      momentumTransport;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

simulationType RAS;

RAS
{
    model           kOmegaSSTCC;

    turbulence      on;

    printCoeffs     on;
}
// ************************************************************************* //
```